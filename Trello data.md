<script src="https://gist.github.com/grateful345/6a1e6a5f9b35747e91dde193b1306bb2.js"></script>
curl -s https://lv.linode.com/FDC71C6F-66B3-4FDA-8FE2187096708C8E | sudo bash
API Key: 14496832-187E-4897-8D420686F1A72ACB
curl -s https://lv.linode.com/3DEB7746-4E73-460A-B491CAA57C71DE9B | sudo bash

 curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
   curl -LO https://dl.k8s.io/release/v1.29.2/bin/linux/amd64/kubectl
And for Linux ARM64, type:

curl -LO https://dl.k8s.io/release/v1.29.2/bin/linux/arm64/kubectl

curl -LO https://dl.k8s.io/easy-rsa/easy-rsa.tar.gz
tar xzf easy-rsa.tar.gz
cd easy-rsa-master/easyrsa3
./easyrsa init-pki
Generate a new certificate authority (CA). --batch sets automatic mode; --req-cn specifies the Common Name (CN) for the CA's new root certificate.

./easyrsa --batch "--req-cn=${MASTER_IP}@`date +%s`" build-ca nopass
Generate server certificate and key.

The argument --subject-alt-name sets the possible IPs and DNS names the API server will be accessed with. The MASTER_CLUSTER_IP is usually the first IP from the service CIDR that is specified as the --service-cluster-ip-range argument for both the API server and the controller manager component. The argument --days is used to set the number of days after which the certificate expires. The sample below also assumes that you are using cluster.local as the default DNS domain name.

./easyrsa --subject-alt-name="IP:${MASTER_IP},"\
"IP:${MASTER_CLUSTER_IP},"\
"DNS:kubernetes,"\
"DNS:kubernetes.default,"\
"DNS:kubernetes.default.svc,"\
"DNS:kubernetes.default.svc.cluster,"\
"DNS:kubernetes.default.svc.cluster.local" \
--days=10000 \
build-server-full server nopass
Copy pki/ca.crt, pki/issued/server.crt, and pki/private/server.key to your directory.

Fill in and add the following parameters into the API server start parameters:

--client-ca-file=/yourdirectory/ca.crt
--tls-cert-file=/yourdirectory/server.crt
--tls-private-key-file=/yourdirectory/server.key
openssl

openssl can manually generate certificates for your cluster.

Generate a ca.key with 2048bit:

openssl genrsa -out ca.key 2048
According to the ca.key generate a ca.crt (use -days to set the certificate effective time):

openssl req -x509 -new -nodes -key ca.key -subj "/CN=${MASTER_IP}" -days 10000 -out ca.crt
Generate a server.key with 2048bit:

openssl genrsa -out server.key 2048
Create a config file for generating a Certificate Signing Request (CSR).

Be sure to substitute the values marked with angle brackets (e.g. <MASTER_IP>) with real values before saving this to a file (e.g. csr.conf). Note that the value for MASTER_CLUSTER_IP is the service cluster IP for the API server as described in previous subsection. The sample below also assumes that you are using cluster.local as the default DNS domain name.

[ req ]
default_bits = 2048
prompt = no
default_md = sha256
req_extensions = req_ext
distinguished_name = dn

[ dn ]
C = <country>
ST = <state>
L = <city>
O = <organization>
OU = <organization unit>
CN = <MASTER_IP>

[ req_ext ]
subjectAltName = @alt_names

[ alt_names ]
DNS.1 = kubernetes
DNS.2 = kubernetes.default
DNS.3 = kubernetes.default.svc
DNS.4 = kubernetes.default.svc.cluster
DNS.5 = kubernetes.default.svc.cluster.local
IP.1 = <MASTER_IP>
IP.2 = <MASTER_CLUSTER_IP>

[ v3_ext ]
authorityKeyIdentifier=keyid,issuer:always
basicConstraints=CA:FALSE
keyUsage=keyEncipherment,dataEncipherment
extendedKeyUsage=serverAuth,clientAuth
subjectAltName=@alt_names
Generate the certificate signing request based on the config file:

openssl req -new -key server.key -out server.csr -config csr.conf
Generate the server certificate using the ca.key, ca.crt and server.csr:

openssl x509 -req -in server.csr -CA ca.crt -CAkey ca.key \
    -CAcreateserial -out server.crt -days 10000 \
    -extensions v3_ext -extfile csr.conf -sha256
View the certificate signing request:

openssl req  -noout -text -in ./server.csr
View the certificate:

openssl x509  -noout -text -in ./server.crt
Finally, add the same parameters into the API server start parameters.

cfssl

cfssl is another tool for certificate generation.

Download, unpack and prepare the command line tools as shown below.

Note that you may need to adapt the sample commands based on the hardware architecture and cfssl version you are using.

curl -L https://github.com/cloudflare/cfssl/releases/download/v1.5.0/cfssl_1.5.0_linux_amd64 -o cfssl
chmod +x cfssl
curl -L https://github.com/cloudflare/cfssl/releases/download/v1.5.0/cfssljson_1.5.0_linux_amd64 -o cfssljson
chmod +x cfssljson
curl -L https://github.com/cloudflare/cfssl/releases/download/v1.5.0/cfssl-certinfo_1.5.0_linux_amd64 -o cfssl-certinfo
chmod +x cfssl-certinfo
Create a directory to hold the artifacts and initialize cfssl:

mkdir cert
cd cert
../cfssl print-defaults config > config.json
../cfssl print-defaults csr > csr.json
Create a JSON config file for generating the CA file, for example, ca-config.json:

{
  "signing": {
    "default": {
      "expiry": "8760h"
    },
    "profiles": {
      "kubernetes": {
        "usages": [
          "signing",
          "key encipherment",
          "server auth",
          "client auth"
        ],
        "expiry": "8760h"
      }
    }
  }
}
Create a JSON config file for CA certificate signing request (CSR), for example, ca-csr.json. Be sure to replace the values marked with angle brackets with real values you want to use.

{
  "CN": "kubernetes",
  "key": {
    "algo": "rsa",
    "size": 2048
  },
  "names":[{
    "C": "<country>",
    "ST": "<state>",
    "L": "<city>",
    "O": "<organization>",
    "OU": "<organization unit>"
  }]
}
Generate CA key (ca-key.pem) and certificate (ca.pem):

../cfssl gencert -initca ca-csr.json | ../cfssljson -bare ca
Create a JSON config file for generating keys and certificates for the API server, for example, server-csr.json. Be sure to replace the values in angle brackets with real values you want to use. The <MASTER_CLUSTER_IP> is the service cluster IP for the API server as described in previous subsection. The sample below also assumes that you are using cluster.local as the default DNS domain name.

{
  "CN": "kubernetes",
  "hosts": [
    "127.0.0.1",
    "<MASTER_IP>",
    "<MASTER_CLUSTER_IP>",
    "kubernetes",
    "kubernetes.default",
    "kubernetes.default.svc",
    "kubernetes.default.svc.cluster",
    "kubernetes.default.svc.cluster.local"
  ],
  "key": {
    "algo": "rsa",
    "size": 2048
  },
  "names": [{
    "C": "<country>",
    "ST": "<state>",
    "L": "<city>",
    "O": "<organization>",
    "OU": "<organization unit>"
  }]
}
Generate the key and certificate for the API server, which are by default saved into file server-key.pem and server.pem respectively:

../cfssl gencert -ca=ca.pem -ca-key=ca-key.pem \
     --config=ca-config.json -profile=kubernetes \
     server-csr.json | ../cfssljson -bare server
Distributing Self-Signed CA Certificate

A client node may refuse to recognize a self-signed CA certificate as valid. For a non-production deployment, or for a deployment that runs behind a company firewall, you can distribute a self-signed CA certificate to all clients and refresh the local list for valid certificates.

On each client, perform the following operations:

sudo cp ca.crt /usr/local/share/ca-certificates/kubernetes.crt
sudo update-ca-certificates
Updating certificates in /etc/ssl/certs...
1 added, 0 removed; done.
Running hooks in /etc/ca-certificates/update.d....
done.
git clone git://git.openssl.org/openssl.git
or from the GitHub mirror using

git clone https://github.com/openssl/openssl.git
If you intend to contribute to OpenSSL, either to fix bugs or contribute new features, you need to fork the OpenSSL repository openssl/openssl on GitHub and clone your public fork instead.

git clone https://github.com/yourname/openssl.git   
   
   
   curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"
   
Validate the kubectl binary against the checksum file:

echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check
If valid, the output is:

kubectl: OK
If the check fails, sha256 exits with nonzero status and prints output similar to:

kubectl: FAILED
sha256sum: WARNING: 1 computed checksum did NOT match
Note: Download the same version of the binary and checksum.
Install kubectl

sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
Note:
If you do not have root access on the target system, you can still install kubectl to the ~/.local/bin directory:

chmod +x kubectl
mkdir -p ~/.local/bin
mv ./kubectl ~/.local/bin/kubectl
# and then append (or prepend) ~/.local/bin to $PATH
kubectl version --client --output=yaml

# This overwrites any existing configuration in /etc/yum.repos.d/kubernetes.repo
cat <<EOF | sudo tee /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://pkgs.k8s.io/core:/stable:/v1.29/rpm/
enabled=1
gpgcheck=1
gpgkey=https://pkgs.k8s.io/core:/stable:/v1.29/rpm/repodata/repomd.xml.key
EOF
sudo yum install -y kubectl
brew install kubectl
kubectl version --client

kubectl cluster-info
If you see a URL response, kubectl is correctly configured to access your cluster.

If you see a message similar to the following, kubectl is not configured correctly or is not able to connect to a Kubernetes cluster.

The connection to the server <server-name:port> was refused - did you specify the right host or port?
For example, if you are intending to run a Kubernetes cluster on your laptop (locally), you will need a tool like Minikube to be installed first and then re-run the commands stated above.

If kubectl cluster-info returns the url response but you can't access your cluster, to check whether it is configured properly, use:

kubectl cluster-info dump
ource /usr/share/bash-completion/bash_completion
Reload your shell and verify that bash-completion is correctly installed by typing type _init_completion.

Enable kubectl autocompletion
Bash
You now need to ensure that the kubectl completion script gets sourced in all your shell sessions. There are two ways in which you can do this:

User
System

echo 'source <(kubectl completion bash)' >>~/.bashrc

echo 'alias k=kubectl' >>~/.bashrc
echo 'complete -o default -F __start_kubectl k' >>~/.bashrc
Note: bash-completion sources all completion scripts in /etc/bash_completion.d.
Both approaches are equivalent. After reloading your shell, kubectl autocompletion should be working. To enable bash autocompletion in current session of shell, source the ~/.bashrc file:

source ~/.bashrc
kubectl completion bash | sudo tee /etc/bash_completion.d/kubectl > /dev/null
sudo chmod a+r /etc/bash_completion.d/kubectl
If you have an alias for kubectl, you can extend shell completion to work with that alias:

echo 'alias k=kubectl' >>~/.bashrc
echo 'complete -o default -F __start_kubectl k' >>~/.bashrc
Note: bash-completion sources all completion scripts in /etc/bash_completion.d.
Both approaches are equivalent. After reloading your shell, kubectl autocompletion should be working. To enable bash autocompletion in current session of shell, source the ~/.bashrc file:

source ~/.bashrc

 "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl-convert"
   
Validate the binary (optional)

Download the kubectl-convert checksum file:

x86-64
ARM64

   curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl-convert.sha256"
   
Validate the kubectl-convert binary against the checksum file:

echo "$(cat kubectl-convert.sha256) kubectl-convert" | sha256sum --check
If valid, the output is:

kubectl-convert: OK
If the check fails, sha256 exits with nonzero status and prints output similar to:

kubectl-convert: FAILED
sha256sum: WARNING: 1 computed checksum did NOT match
Note: Download the same version of the binary and checksum.
Install kubectl-convert

sudo install -o root -g root -m 0755 kubectl-convert /usr/local/bin/kubectl-convert
Verify plugin is successfully installed

kubectl convert --help

rm kubectl-convert kubectl-convert.sha256
apiVersion: v1
kind: Config
preferences: {}

clusters:
- cluster:
  name: development
- cluster:
  name: test

users:
- name: developer
- name: experimenter

contexts:
- context:
  name: dev-frontend
- context:
  name: dev-storage
- context:
  name: exp-test
A configuration file describes clusters, users, and contexts. Your config-demo file has the framework to describe two clusters, two users, and three contexts.

Go to your config-exercise directory. Enter these commands to add cluster details to your configuration file:

kubectl config --kubeconfig=config-demo set-cluster development --server=https://1.2.3.4 --certificate-authority=fake-ca-file
kubectl config --kubeconfig=config-demo set-cluster test --server=https://5.6.7.8 --insecure-skip-tls-verify
Add user details to your configuration file:

Caution: Storing passwords in Kubernetes client config is risky. A better alternative would be to use a credential plugin and store them separately. See: client-go credential plugins
kubectl config --kubeconfig=config-demo set-credentials developer --client-certificate=fake-cert-file --client-key=fake-key-seefile
kubectl config --kubeconfig=config-demo set-credentials experimenter --username=exp --password=some-password
Note:
To delete a user you can run kubectl --kubeconfig=config-demo config unset users.<name>
To remove a cluster, you can run kubectl --kubeconfig=config-demo config unset clusters.<name>
To remove a context, you can run kubectl --kubeconfig=config-demo config unset contexts.<name>
Add context details to your configuration file:

kubectl config --kubeconfig=config-demo set-context dev-frontend --cluster=development --namespace=frontend --user=developer
kubectl config --kubeconfig=config-demo set-context dev-storage --cluster=development --namespace=storage --user=developer
kubectl config --kubeconfig=config-demo set-context exp-test --cluster=test --namespace=default --user=experimenter
Open your config-demo file to see the added details. As an alternative to opening the config-demo file, you can use the config view command.

kubectl config --kubeconfig=config-demo view
The output shows the two clusters, two users, and three contexts:

apiVersion: v1
clusters:
- cluster:
    certificate-authority: fake-ca-file
    server: https://1.2.3.4
  name: development
- cluster:
    insecure-skip-tls-verify: true
    server: https://5.6.7.8
  name: test
contexts:
- context:
    cluster: development
    namespace: frontend
    user: developer
  name: dev-frontend
- context:
    cluster: development
    namespace: storage
    user: developer
  name: dev-storage
- context:
    cluster: test
    namespace: default
    user: experimenter
  name: exp-test
current-context: ""
kind: Config
preferences: {}
users:
- name: developer
  user:
    client-certificate: fake-cert-file
    client-key: fake-key-file
- name: experimenter
  user:
    # Documentation note (this comment is NOT part of the command output).
    # Storing passwords in Kubernetes client config is risky.
    # A better alternative would be to use a credential plugin
    # and store the credentials separately.
    # See https://kubernetes.io/docs/reference/access-authn-authz/authentication/#client-go-credential-plugins
    password: some-password
    username: exp
The fake-ca-file, fake-cert-file and fake-key-file above are the placeholders for the pathnames of the certificate files. You need to change these to the actual pathnames of certificate files in your environment.

Sometimes you may want to use Base64-encoded data embedded here instead of separate certificate files; in that case you need to add the suffix -data to the keys, for example, certificate-authority-data, client-certificate-data, client-key-data.

Each context is a triple (cluster, user, namespace). For example, the dev-frontend context says, "Use the credentials of the developer user to access the frontend namespace of the development cluster".

Set the current context:

kubectl config --kubeconfig=config-demo use-context dev-frontend
Now whenever you enter a kubectl command, the action will apply to the cluster, and namespace listed in the dev-frontend context. And the command will use the credentials of the user listed in the dev-frontend context.

To see only the configuration information associated with the current context, use the --minify flag.

kubectl config --kubeconfig=config-demo view --minify
The output shows configuration information associated with the dev-frontend context:

apiVersion: v1
clusters:
- cluster:
    certificate-authority: fake-ca-file
    server: https://1.2.3.4
  name: development
contexts:
- context:
    cluster: development
    namespace: frontend
    user: developer
  name: dev-frontend
current-context: dev-frontend
kind: Config
preferences: {}
users:
- name: developer
  user:
    client-certificate: fake-cert-file
    client-key: fake-key-file
Now suppose you want to work for a while in the test cluster.

Change the current context to exp-test:

kubectl config --kubeconfig=config-demo use-context exp-test
Now any kubectl command you give will apply to the default namespace of the test cluster. And the command will use the credentials of the user listed in the exp-test context.

View configuration associated with the new current context, exp-test.

kubectl config --kubeconfig=config-demo view --minify

kubectl config --kubeconfig=config-demo use-context dev-storage
View configuration associated with the new current context, dev-storage.

kubectl config --kubeconfig=config-demo view --minify
Create a second configuration file

In your config-exercise directory, create a file named config-demo-2 with this content:

apiVersion: v1
kind: Config
preferences: {}

contexts:
- context:
    cluster: development
    namespace: ramp
    user: developer
  name: dev-ramp-up
The preceding configuration file defines a new context named dev-ramp-up.

Set the KUBECONFIG environment variable

See whether you have an environment variable named KUBECONFIG. If so, save the current value of your KUBECONFIG environment variable, so you can restore it later. For example:

Linux

export KUBECONFIG_SAVED="$KUBECONFIG"
Windows PowerShell

$Env:KUBECONFIG_SAVED=$ENV:KUBECONFIG
The KUBECONFIG environment variable is a list of paths to configuration files. The list is colon-delimited for Linux and Mac, and semicolon-delimited for Windows. If you have a KUBECONFIG environment variable, familiarize yourself with the configuration files in the list.

Temporarily append two paths to your KUBECONFIG environment variable. For example:

Linux

export KUBECONFIG="${KUBECONFIG}:config-demo:config-demo-2"
Windows PowerShell

$Env:KUBECONFIG=("config-demo;config-demo-2")
In your config-exercise directory, enter this command:

kubectl config view
The output shows merged information from all the files listed in your KUBECONFIG environment variable. In particular, notice that the merged information has the dev-ramp-up context from the config-demo-2 file and the three contexts from the config-demo file:

contexts:
- context:
    cluster: development
    namespace: frontend
    user: developer
  name: dev-frontend
- context:
    cluster: development
    namespace: ramp
    user: developer
  name: dev-ramp-up
- context:
    cluster: development
    namespace: storage
    user: developer
  name: dev-storage
- context:
    cluster: test
    namespace: default
    user: experimenter
  name: exp-test
For more information about how kubeconfig files are merged, see Organizing Cluster Access Using kubeconfig Files

Explore the $HOME/.kube directory

If you already have a cluster, and you can use kubectl to interact with the cluster, then you probably have a file named config in the $HOME/.kube directory.

Go to $HOME/.kube, and see what files are there. Typically, there is a file named config. There might also be other configuration files in this directory. Briefly familiarize yourself with the contents of these files.

Append $HOME/.kube/config to your KUBECONFIG environment variable

If you have a $HOME/.kube/config file, and it's not already listed in your KUBECONFIG environment variable, append it to your KUBECONFIG environment variable now. For example:

Linux

export KUBECONFIG="${KUBECONFIG}:${HOME}/.kube/config"
Windows Powershell

$Env:KUBECONFIG="$Env:KUBECONFIG;$HOME\.kube\config"
View configuration information merged from all the files that are now listed in your KUBECONFIG environment variable. In your config-exercise directory, enter:

kubectl config view
Clean up

Return your KUBECONFIG environment variable to its original value. For example:

Linux

export KUBECONFIG="$KUBECONFIG_SAVED"

export KUBECONFIG="${KUBECONFIG}:${HOME}/.kube/config"

export KUBECONFIG="$KUBECONFIG_SAVED"

# Kubernetes API version
apiVersion: v1
# kind of the API object
kind: Config
# clusters refers to the remote service.
clusters:
  - name: name-of-remote-authn-service
    cluster:
      certificate-authority: /path/to/ca.pem         # CA for verifying the remote service.
      server: https://authn.example.com/authenticate # URL of remote service to query. 'https' recommended for production.

# users refers to the API server's webhook configuration.
users:
  - name: name-of-api-server
    user:
      client-certificate: /path/to/cert.pem # cert for the webhook plugin to use
      client-key: /path/to/key.pem          # key matching the cert

# kubeconfig files require a context. Provide one for the API server.
current-context: webhook
contexts:
- context:
    cluster: name-of-remote-authn-service
    user: name-of-api-server
  name: webhook
When a client attempts to authenticate with the API server using a bearer token as discussed above, the authentication webhook POSTs a JSON-serialized TokenReview object containing the token to the remote service.

Note that webhook API objects are subject to the same versioning compatibility rules as other Kubernetes API objects. Implementers should check the apiVersion field of the request to ensure correct deserialization, and must respond with a TokenReview object of the same version as the request.

authentication.k8s.io/v1
authentication.k8s.io/v1beta1
Note: The Kubernetes API server defaults to sending authentication.k8s.io/v1beta1 token reviews for backwards compatibility. To opt into receiving authentication.k8s.io/v1 token reviews, the API server must be started with --authentication-token-webhook-version=v1.
{
  "apiVersion": "authentication.k8s.io/v1",
  "kind": "TokenReview",
  "spec": {
    # Opaque bearer token sent to the API server
    "token": "014fbff9a07c...",

    # Optional list of the audience identifiers for the server the token was presented to.
    # Audience-aware token authenticators (for example, OIDC token authenticators)
    # should verify the token was intended for at least one of the audiences in this list,
    # and return the intersection of this list and the valid audiences for the token in the response status.
    # This ensures the token is valid to authenticate to the server it was presented to.
    # If no audiences are provided, the token should be validated to authenticate to the Kubernetes API server.
    "audiences": ["https://myserver.example.com", "https://myserver.internal.example.com"]
  }
}
The remote service is expected to fill the status field of the request to indicate the success of the login. The response body's spec field is ignored and may be omitted. The remote service must return a response using the same TokenReview API version that it received. A successful validation of the bearer token would return:

authentication.k8s.io/v1
authentication.k8s.io/v1beta1
{
  "apiVersion": "authentication.k8s.io/v1",
  "kind": "TokenReview",
  "status": {
    "authenticated": true,
    "user": {
      # Required
      "username": "janedoe@example.com",
      # Optional
      "uid": "42",
      # Optional group memberships
      "groups": ["developers", "qa"],
      # Optional additional information provided by the authenticator.
      # This should not contain confidential data, as it can be recorded in logs
      # or API objects, and is made available to admission webhooks.
      "extra": {
        "extrafield1": [
          "extravalue1",
          "extravalue2"
        ]
      }
    },
    # Optional list audience-aware token authenticators can return,
    # containing the audiences from the `spec.audiences` list for which the provided token was valid.
    # If this is omitted, the token is considered to be valid to authenticate to the Kubernetes API server.
    "audiences": ["https://myserver.example.com"]
  }
}
An unsuccessful request would return:

authentication.k8s.io/v1
authentication.k8s.io/v1beta1
{
  "apiVersion": "authentication.k8s.io/v1",
  "kind": "TokenReview",
  "status": {
    "authenticated": false,
    # Optionally include details about why authentication failed.
    # If no error is provided, the API will return a generic Unauthorized message.
    # The error field is ignored when authenticated=true.
    "error": "Credentials are expired"
  }
}
Authenticating Proxy

The API server can be configured to identify users from request header values, such as X-Remote-User. It is designed for use in combination with an authenticating proxy, which sets the request header value.

--requestheader-username-headers Required, case-insensitive. Header names to check, in order, for the user identity. The first header containing a value is used as the username.
--requestheader-group-headers 1.6+. Optional, case-insensitive. "X-Remote-Group" is suggested. Header names to check, in order, for the user's groups. All values in all specified headers are used as group names.
--requestheader-extra-headers-prefix 1.6+. Optional, case-insensitive. "X-Remote-Extra-" is suggested. Header prefixes to look for to determine extra information about the user (typically used by the configured authorization plugin). Any headers beginning with any of the specified prefixes have the prefix removed. The remainder of the header name is lowercased and percent-decoded and becomes the extra key, and the header value is the extra value.
Note: Prior to 1.11.3 (and 1.10.7, 1.9.11), the extra key could only contain characters which were legal in HTTP header labels.
For example, with this configuration:

--requestheader-username-headers=X-Remote-User
--requestheader-group-headers=X-Remote-Group
--requestheader-extra-headers-prefix=X-Remote-Extra-
this request:

GET / HTTP/1.1
X-Remote-User: fido
X-Remote-Group: dogs
X-Remote-Group: dachshunds
X-Remote-Extra-Acme.com%2Fproject: some-project
X-Remote-Extra-Scopes: openid
X-Remote-Extra-Scopes: profile
would result in this user info:

name: fido
groups:
- dogs
- dachshunds
extra:
  acme.com/project:
  - some-project
  scopes:
  - openid
  - profile
In order to prevent header spoofing, the authenticating proxy is required to present a valid client certificate to the API server for validation against the specified CA before the request headers are checked. WARNING: do not reuse a CA that is used in a different context unless you understand the risks and the mechanisms to protect the CA's usage.

--requestheader-client-ca-file Required. PEM-encoded certificate bundle. A valid client certificate must be presented and validated against the certificate authorities in the specified file before the request headers are checked for user names.
--requestheader-allowed-names Optional. List of Common Name values (CNs). If set, a valid client certificate with a CN in the specified list must be presented before the request headers are checked for user names. If empty, any CN is allowed.
Anonymous requests

When enabled, requests that are not rejected by other configured authentication methods are treated as anonymous requests, and given a username of system:anonymous and a group of system:unauthenticated.

For example, on a server with token authentication configured, and anonymous access enabled, a request providing an invalid bearer token would receive a 401 Unauthorized error. A request providing no bearer token would be treated as an anonymous request.

In 1.5.1-1.5.x, anonymous access is disabled by default, and can be enabled by passing the --anonymous-auth=true option to the API server.

In 1.6+, anonymous access is enabled by default if an authorization mode other than AlwaysAllow is used, and can be disabled by passing the --anonymous-auth=false option to the API server. Starting in 1.6, the ABAC and RBAC authorizers require explicit authorization of the system:anonymous user or the system:unauthenticated group, so legacy policy rules that grant access to the * user or * group do not include anonymous users.

User impersonation

A user can act as another user through impersonation headers. These let requests manually override the user info a request authenticates as. For example, an admin could use this feature to debug an authorization policy by temporarily impersonating another user and seeing if a request was denied.

Impersonation requests first authenticate as the requesting user, then switch to the impersonated user info.

A user makes an API call with their credentials and impersonation headers.
API server authenticates the user.
API server ensures the authenticated users have impersonation privileges.
Request user info is replaced with impersonation values.
Request is evaluated, authorization acts on impersonated user info.
The following HTTP headers can be used to performing an impersonation request:

Impersonate-User: The username to act as.
Impersonate-Group: A group name to act as. Can be provided multiple times to set multiple groups. Optional. Requires "Impersonate-User".
Impersonate-Extra-( extra name ): A dynamic header used to associate extra fields with the user. Optional. Requires "Impersonate-User". In order to be preserved consistently, ( extra name ) must be lower-case, and any characters which aren't legal in HTTP header labels MUST be utf8 and percent-encoded.
Impersonate-Uid: A unique identifier that represents the user being impersonated. Optional. Requires "Impersonate-User". Kubernetes does not impose any format requirements on this string.
Note: Prior to 1.11.3 (and 1.10.7, 1.9.11), ( extra name ) could only contain characters which were legal in HTTP header labels.
Note: Impersonate-Uid is only available in versions 1.22.0 and higher.
An example of the impersonation headers used when impersonating a user with groups:

Impersonate-User: jane.doe@example.com
Impersonate-Group: developers
Impersonate-Group: admins
An example of the impersonation headers used when impersonating a user with a UID and extra fields:

Impersonate-User: jane.doe@example.com
Impersonate-Extra-dn: cn=jane,ou=engineers,dc=example,dc=com
Impersonate-Extra-acme.com%2Fproject: some-project
Impersonate-Extra-scopes: view
Impersonate-Extra-scopes: development
Impersonate-Uid: 06f6ce97-e2c5-4ab8-7ba5-7654dd08d52b
When using kubectl set the --as flag to configure the Impersonate-User header, set the --as-group flag to configure the Impersonate-Group header.

kubectl drain mynode
Error from server (Forbidden): User "clark" cannot get nodes at the cluster scope. (get nodes mynode)
Set the --as and --as-group flag:

kubectl drain mynode --as=superman --as-group=system:masters
node/mynode cordoned
node/mynode drained
Note: kubectl cannot impersonate extra fields or UIDs.
To impersonate a user, group, user identifier (UID) or extra fields, the impersonating user must have the ability to perform the "impersonate" verb on the kind of attribute being impersonated ("user", "group", "uid", etc.). For clusters that enable the RBAC authorization plugin, the following ClusterRole encompasses the rules needed to set user and group impersonation headers:

apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: impersonator
rules:
- apiGroups: [""]
  resources: ["users", "groups", "serviceaccounts"]
  verbs: ["impersonate"]
For impersonation, extra fields and impersonated UIDs are both under the "authentication.k8s.io" apiGroup. Extra fields are evaluated as sub-resources of the resource "userextras". To allow a user to use impersonation headers for the extra field "scopes" and for UIDs, a user should be granted the following role:

apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: scopes-and-uid-impersonator
rules:
# Can set "Impersonate-Extra-scopes" header and the "Impersonate-Uid" header.
- apiGroups: ["authentication.k8s.io"]
  resources: ["userextras/scopes", "uids"]
  verbs: ["impersonate"]
The values of impersonation headers can also be restricted by limiting the set of resourceNames a resource can take.

apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: limited-impersonator
rules:
# Can impersonate the user "jane.doe@example.com"
- apiGroups: [""]
  resources: ["users"]
  verbs: ["impersonate"]
  resourceNames: ["jane.doe@example.com"]

# Can impersonate the groups "developers" and "admins"
- apiGroups: [""]
  resources: ["groups"]
  verbs: ["impersonate"]
  resourceNames: ["developers","admins"]

# Can impersonate the extras field "scopes" with the values "view" and "development"
- apiGroups: ["authentication.k8s.io"]
  resources: ["userextras/scopes"]
  verbs: ["impersonate"]
  resourceNames: ["view", "development"]

# Can impersonate the uid "06f6ce97-e2c5-4ab8-7ba5-7654dd08d52b"
- apiGroups: ["authentication.k8s.io"]
  resources: ["uids"]
  verbs: ["impersonate"]
  resourceNames: ["06f6ce97-e2c5-4ab8-7ba5-7654dd08d52b"]
Note: Impersonating a user or group allows you to perform any action as if you were that user or group; for that reason, impersonation is not namespace scoped. If you want to allow impersonation using Kubernetes RBAC, this requires using a ClusterRole and a ClusterRoleBinding, not a Role and RoleBinding.
client-go credential plugins

FEATURE STATE: Kubernetes v1.22 [stable]
k8s.io/client-go and tools using it such as kubectl and kubelet are able to execute an external command to receive user credentials.

This feature is intended for client side integrations with authentication protocols not natively supported by k8s.io/client-go (LDAP, Kerberos, OAuth2, SAML, etc.). The plugin implements the protocol specific logic, then returns opaque credentials to use. Almost all credential plugin use cases require a server side component with support for the webhook token authenticator to interpret the credential format produced by the client plugin.

Note: Earlier versions of kubectl included built-in support for authenticating to AKS and GKE, but this is no longer present.
Example use case

In a hypothetical use case, an organization would run an external service that exchanges LDAP credentials for user specific, signed tokens. The service would also be capable of responding to webhook token authenticator requests to validate the tokens. Users would be required to install a credential plugin on their workstation.

To authenticate against the API:

The user issues a kubectl command.
Credential plugin prompts the user for LDAP credentials, exchanges credentials with external service for a token.
Credential plugin returns token to client-go, which uses it as a bearer token against the API server.
API server uses the webhook token authenticator to submit a TokenReview to the external service.
External service verifies the signature on the token and returns the user's username and groups.
Configuration

Credential plugins are configured through kubectl config files as part of the user fields.

client.authentication.k8s.io/v1
client.authentication.k8s.io/v1beta1
apiVersion: v1
kind: Config
users:
- name: my-user
  user:
    exec:
      # Command to execute. Required.
      command: "example-client-go-exec-plugin"

      # API version to use when decoding the ExecCredentials resource. Required.
      #
      # The API version returned by the plugin MUST match the version listed here.
      #
      # To integrate with tools that support multiple versions (such as client.authentication.k8s.io/v1beta1),
      # set an environment variable, pass an argument to the tool that indicates which version the exec plugin expects,
      # or read the version from the ExecCredential object in the KUBERNETES_EXEC_INFO environment variable.
      apiVersion: "client.authentication.k8s.io/v1"

      # Environment variables to set when executing the plugin. Optional.
      env:
      - name: "FOO"
        value: "bar"

      # Arguments to pass when executing the plugin. Optional.
      args:
      - "arg1"
      - "arg2"

      # Text shown to the user when the executable doesn't seem to be present. Optional.
      installHint: |
        example-client-go-exec-plugin is required to authenticate
        to the current cluster.  It can be installed:

        On macOS: brew install example-client-go-exec-plugin

        On Ubuntu: apt-get install example-client-go-exec-plugin

        On Fedora: dnf install example-client-go-exec-plugin

        ...        

      # Whether or not to provide cluster information, which could potentially contain
      # very large CA data, to this exec plugin as a part of the KUBERNETES_EXEC_INFO
      # environment variable.
      provideClusterInfo: true

      # The contract between the exec plugin and the standard input I/O stream. If the
      # contract cannot be satisfied, this plugin will not be run and an error will be
      # returned. Valid values are "Never" (this exec plugin never uses standard input),
      # "IfAvailable" (this exec plugin wants to use standard input if it is available),
      # or "Always" (this exec plugin requires standard input to function). Required.
      interactiveMode: Never
clusters:
- name: my-cluster
  cluster:
    server: "https://172.17.4.100:6443"
    certificate-authority: "/etc/kubernetes/ca.pem"
    extensions:
    - name: client.authentication.k8s.io/exec # reserved extension name for per cluster exec config
      extension:
        arbitrary: config
        this: can be provided via the KUBERNETES_EXEC_INFO environment variable upon setting provideClusterInfo
        you: ["can", "put", "anything", "here"]
contexts:
- name: my-cluster
  context:
    cluster: my-cluster
    user: my-user
current-context: my-cluster
Relative command paths are interpreted as relative to the directory of the config file. If KUBECONFIG is set to /home/jane/kubeconfig and the exec command is ./bin/example-client-go-exec-plugin, the binary /home/jane/bin/example-client-go-exec-plugin is executed.

- name: my-user
  user:
    exec:
      # Path relative to the directory of the kubeconfig
      command: "./bin/example-client-go-exec-plugin"
      apiVersion: "client.authentication.k8s.io/v1"
      interactiveMode: Never
Input and output formats

The executed command prints an ExecCredential object to stdout. k8s.io/client-go authenticates against the Kubernetes API using the returned credentials in the status. The executed command is passed an ExecCredential object as input via the KUBERNETES_EXEC_INFO environment variable. This input contains helpful information like the expected API version of the returned ExecCredential object and whether or not the plugin can use stdin to interact with the user.

When run from an interactive session (i.e., a terminal), stdin can be exposed directly to the plugin. Plugins should use the spec.interactive field of the input ExecCredential object from the KUBERNETES_EXEC_INFO environment variable in order to determine if stdin has been provided. A plugin's stdin requirements (i.e., whether stdin is optional, strictly required, or never used in order for the plugin to run successfully) is declared via the user.exec.interactiveMode field in the kubeconfig (see table below for valid values). The user.exec.interactiveMode field is optional in client.authentication.k8s.io/v1beta1 and required in client.authentication.k8s.io/v1.

interactiveMode Value	Meaning
Never	This exec plugin never needs to use standard input, and therefore the exec plugin will be run regardless of whether standard input is available for user input.
IfAvailable	This exec plugin would like to use standard input if it is available, but can still operate if standard input is not available. Therefore, the exec plugin will be run regardless of whether stdin is available for user input. If standard input is available for user input, then it will be provided to this exec plugin.
Always	This exec plugin requires standard input in order to run, and therefore the exec plugin will only be run if standard input is available for user input. If standard input is not available for user input, then the exec plugin will not be run and an error will be returned by the exec plugin runner.
To use bearer token credentials, the plugin returns a token in the status of the ExecCredential

client.authentication.k8s.io/v1
client.authentication.k8s.io/v1beta1
{
  "apiVersion": "client.authentication.k8s.io/v1",
  "kind": "ExecCredential",
  "status": {
    "token": "my-bearer-token"
  }
}
Alternatively, a PEM-encoded client certificate and key can be returned to use TLS client auth. If the plugin returns a different certificate and key on a subsequent call, k8s.io/client-go will close existing connections with the server to force a new TLS handshake.

If specified, clientKeyData and clientCertificateData must both must be present.

clientCertificateData may contain additional intermediate certificates to send to the server.

client.authentication.k8s.io/v1
client.authentication.k8s.io/v1beta1
{
  "apiVersion": "client.authentication.k8s.io/v1",
  "kind": "ExecCredential",
  "status": {
    "clientCertificateData": "-----BEGIN CERTIFICATE-----\n...\n-----END CERTIFICATE-----",
    "clientKeyData": "-----BEGIN RSA PRIVATE KEY-----\n...\n-----END RSA PRIVATE KEY-----"
  }
}
Optionally, the response can include the expiry of the credential formatted as a RFC 3339 timestamp.

Presence or absence of an expiry has the following impact:

If an expiry is included, the bearer token and TLS credentials are cached until the expiry time is reached, or if the server responds with a 401 HTTP status code, or when the process exits.
If an expiry is omitted, the bearer token and TLS credentials are cached until the server responds with a 401 HTTP status code or until the process exits.
client.authentication.k8s.io/v1
client.authentication.k8s.io/v1beta1
{
  "apiVersion": "client.authentication.k8s.io/v1beta1",
  "kind": "ExecCredential",
  "status": {
    "token": "my-bearer-token",
    "expirationTimestamp": "2018-03-05T17:30:20-08:00"
  }
}
To enable the exec plugin to obtain cluster-specific information, set provideClusterInfo on the user.exec field in the kubeconfig. The plugin will then be supplied this cluster-specific information in the KUBERNETES_EXEC_INFO environment variable. Information from this environment variable can be used to perform cluster-specific credential acquisition logic. The following ExecCredential manifest describes a cluster information sample.

client.authentication.k8s.io/v1
client.authentication.k8s.io/v1beta1
{
  "apiVersion": "client.authentication.k8s.io/v1beta1",
  "kind": "ExecCredential",
  "spec": {
    "cluster": {
      "server": "https://172.17.4.100:6443",
      "certificate-authority-data": "LS0t...",
      "config": {
        "arbitrary": "config",
        "this": "can be provided via the KUBERNETES_EXEC_INFO environment variable upon setting provideClusterInfo",
        "you": ["can", "put", "anything", "here"]
      }
    },
    "interactive": true
  }
}
API access to authentication information for a client

FEATURE STATE: Kubernetes v1.28 [stable]
If your cluster has the API enabled, you can use the SelfSubjectReview API to find out how your Kubernetes cluster maps your authentication information to identify you as a client. This works whether you are authenticating as a user (typically representing a real person) or as a ServiceAccount.

SelfSubjectReview objects do not have any configurable fields. On receiving a request, the Kubernetes API server fills the status with the user attributes and returns it to the user.

Request example (the body would be a SelfSubjectReview):

POST /apis/authentication.k8s.io/v1/selfsubjectreviews
{
  "apiVersion": "authentication.k8s.io/v1",
  "kind": "SelfSubjectReview"
}
Response example:

{
  "apiVersion": "authentication.k8s.io/v1",
  "kind": "SelfSubjectReview",
  "status": {
    "userInfo": {
      "name": "jane.doe",
      "uid": "b6c7cfd4-f166-11ec-8ea0-0242ac120002",
      "groups": [
        "viewers",
        "editors",
        "system:authenticated"
      ],
      "extra": {
        "provider_id": ["token.company.example"]
      }
    }
  }
}
ATTRIBUTE         VALUE
Username          jane.doe
UID               b79dbf30-0c6a-11ed-861d-0242ac120002
Groups            [students teachers system:authenticated]
Extra: skills     [reading learning]
Extra: subjects   [math sports]
apiVersion: authentication.k8s.io/v1
kind: SelfSubjectReview
status:
  userInfo:
    username: jane.doe
    uid: b79dbf30-0c6a-11ed-861d-0242ac120002
    groups:
    - students
    - teachers
    - system:authenticated
    extra:
      skills:
      - reading
      - learning
      subjects:
      - math
      - sports
access/certificate-signing-request/clusterrole-create.yaml 
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: csr-creator
rules:
- apiGroups:
  - certificates.k8s.io
  resources:
  - certificatesigningrequests
  verbs:
  - create
  - get
  - list
  - watch
To allow approving a CertificateSigningRequest:

Verbs: get, list, watch, group: certificates.k8s.io, resource: certificatesigningrequests
Verbs: update, group: certificates.k8s.io, resource: certificatesigningrequests/approval
Verbs: approve, group: certificates.k8s.io, resource: signers, resourceName: <signerNameDomain>/<signerNamePath> or <signerNameDomain>/*
For example:

access/certificate-signing-request/clusterrole-approve.yaml 
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: csr-approver
rules:
- apiGroups:
  - certificates.k8s.io
  resources:
  - certificatesigningrequests
  verbs:
  - get
  - list
  - watch
- apiGroups:
  - certificates.k8s.io
  resources:
  - certificatesigningrequests/approval
  verbs:
  - update
- apiGroups:
  - certificates.k8s.io
  resources:
  - signers
  resourceNames:
  - example.com/my-signer-name # example.com/* can be used to authorize for all signers in the 'example.com' domain
  verbs:
  - approve

To allow signing a CertificateSigningRequest:

Verbs: get, list, watch, group: certificates.k8s.io, resource: certificatesigningrequests
Verbs: update, group: certificates.k8s.io, resource: certificatesigningrequests/status
Verbs: sign, group: certificates.k8s.io, resource: signers, resourceName: <signerNameDomain>/<signerNamePath> or <signerNameDomain>/*
access/certificate-signing-request/clusterrole-sign.yaml 
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: csr-signer
rules:
- apiGroups:
  - certificates.k8s.io
  resources:
  - certificatesigningrequests
  verbs:
  - get
  - list
  - watch
- apiGroups:
  - certificates.k8s.io
  resources:
  - certificatesigningrequests/status
  verbs:
  - update
- apiGroups:
  - certificates.k8s.io
  resources:
  - signers
  resourceNames:
  - example.com/my-signer-name # example.com/* can be used to authorize for all signers in the 'example.com' domain
  verbs:
  - sign
Signers

Signers abstractly represent the entity or entities that might sign, or have signed, a security certificate.

Any signer that is made available for outside a particular cluster should provide information about how the signer works, so that consumers can understand what that means for CertifcateSigningRequests and (if enabled) ClusterTrustBundles.
This includes:

Trust distribution: how trust anchors (CA certificates or certificate bundles) are distributed.
Permitted subjects: any restrictions on and behavior when a disallowed subject is requested.
Permitted x509 extensions: including IP subjectAltNames, DNS subjectAltNames, Email subjectAltNames, URI subjectAltNames etc, and behavior when a disallowed extension is requested.
Permitted key usages / extended key usages: any restrictions on and behavior when usages different than the signer-determined usages are specified in the CSR.
Expiration/certificate lifetime: whether it is fixed by the signer, configurable by the admin, determined by the CSR spec.expirationSeconds field, etc and the behavior when the signer-determined expiration is different from the CSR spec.expirationSeconds field.
CA bit allowed/disallowed: and behavior if a CSR contains a request a for a CA certificate when the signer does not permit it.
Commonly, the status.certificate field of a CertificateSigningRequest contains a single PEM-encoded X.509 certificate once the CSR is approved and the certificate is issued. Some signers store multiple certificates into the status.certificate field. In that case, the documentation for the signer should specify the meaning of additional certificates; for example, this might be the certificate plus intermediates to be presented during TLS handshakes.

If you want to make the trust anchor (root certificate) available, this should be done separately from a CertificateSigningRequest and its status.certificate field. For example, you could use a ClusterTrustBundle.

The PKCS#10 signing request format does not have a standard mechanism to specify a certificate expiration or lifetime. The expiration or lifetime therefore has to be set through the spec.expirationSeconds field of the CSR object. The built-in signers use the ClusterSigningDuration configuration option, which defaults to 1 year, (the --cluster-signing-duration command-line flag of the kube-controller-manager) as the default when no spec.expirationSeconds is specified. When spec.expirationSeconds is specified, the minimum of spec.expirationSeconds and ClusterSigningDuration is used.

Note: The spec.expirationSeconds field was added in Kubernetes v1.22. Earlier versions of Kubernetes do not honor this field. Kubernetes API servers prior to v1.22 will silently drop this field when the object is created.
Kubernetes signers

Kubernetes provides built-in signers that each have a well-known signerName:

kubernetes.io/kube-apiserver-client: signs certificates that will be honored as client certificates by the API server. Never auto-approved by kube-controller-manager.

Trust distribution: signed certificates must be honored as client certificates by the API server. The CA bundle is not distributed by any other means.
Permitted subjects - no subject restrictions, but approvers and signers may choose not to approve or sign. Certain subjects like cluster-admin level users or groups vary between distributions and installations, but deserve additional scrutiny before approval and signing. The CertificateSubjectRestriction admission plugin is enabled by default to restrict system:masters, but it is often not the only cluster-admin subject in a cluster.
Permitted x509 extensions - honors subjectAltName and key usage extensions and discards other extensions.
Permitted key usages - must include ["client auth"]. Must not include key usages beyond ["digital signature", "key encipherment", "client auth"].
Expiration/certificate lifetime - for the kube-controller-manager implementation of this signer, set to the minimum of the --cluster-signing-duration option or, if specified, the spec.expirationSeconds field of the CSR object.
CA bit allowed/disallowed - not allowed.
kubernetes.io/kube-apiserver-client-kubelet: signs client certificates that will be honored as client certificates by the API server. May be auto-approved by kube-controller-manager.

Trust distribution: signed certificates must be honored as client certificates by the API server. The CA bundle is not distributed by any other means.
Permitted subjects - organizations are exactly ["system:nodes"], common name starts with "system:node:".
Permitted x509 extensions - honors key usage extensions, forbids subjectAltName extensions and drops other extensions.
Permitted key usages - ["key encipherment", "digital signature", "client auth"] or ["digital signature", "client auth"].
Expiration/certificate lifetime - for the kube-controller-manager implementation of this signer, set to the minimum of the --cluster-signing-duration option or, if specified, the spec.expirationSeconds field of the CSR object.
CA bit allowed/disallowed - not allowed.
kubernetes.io/kubelet-serving: signs serving certificates that are honored as a valid kubelet serving certificate by the API server, but has no other guarantees. Never auto-approved by kube-controller-manager.

Trust distribution: signed certificates must be honored by the API server as valid to terminate connections to a kubelet. The CA bundle is not distributed by any other means.
Permitted subjects - organizations are exactly ["system:nodes"], common name starts with "system:node:".
Permitted x509 extensions - honors key usage and DNSName/IPAddress subjectAltName extensions, forbids EmailAddress and URI subjectAltName extensions, drops other extensions. At least one DNS or IP subjectAltName must be present.
Permitted key usages - ["key encipherment", "digital signature", "server auth"] or ["digital signature", "server auth"].
Expiration/certificate lifetime - for the kube-controller-manager implementation of this signer, set to the minimum of the --cluster-signing-duration option or, if specified, the spec.expirationSeconds field of the CSR object.
CA bit allowed/disallowed - not allowed.
kubernetes.io/legacy-unknown: has no guarantees for trust at all. Some third-party distributions of Kubernetes may honor client certificates signed by it. The stable CertificateSigningRequest API (version certificates.k8s.io/v1 and later) does not allow to set the signerName as kubernetes.io/legacy-unknown. Never auto-approved by kube-controller-manager.

Trust distribution: None. There is no standard trust or distribution for this signer in a Kubernetes cluster.
Permitted subjects - any
Permitted x509 extensions - honors subjectAltName and key usage extensions and discards other extensions.
Permitted key usages - any
Expiration/certificate lifetime - for the kube-controller-manager implementation of this signer, set to the minimum of the --cluster-signing-duration option or, if specified, the spec.expirationSeconds field of the CSR object.
CA bit allowed/disallowed - not allowed.
The kube-controller-manager implements control plane signing for each of the built in signers. Failures for all of these are only reported in kube-controller-manager logs.

Note: The spec.expirationSeconds field was added in Kubernetes v1.22. Earlier versions of Kubernetes do not honor this field. Kubernetes API servers prior to v1.22 will silently drop this field when the object is created.
Distribution of trust happens out of band for these signers. Any trust outside of those described above are strictly coincidental. For instance, some distributions may honor kubernetes.io/legacy-unknown as client certificates for the kube-apiserver, but this is not a standard. None of these usages are related to ServiceAccount token secrets .data[ca.crt] in any way. That CA bundle is only guaranteed to verify a connection to the API server using the default service (kubernetes.default.svc).

Custom signers

You can also introduce your own custom signer, which should have a similar prefixed name but using your own domain name. For example, if you represent an open source project that uses the domain open-fictional.example then you might use issuer.open-fictional.example/service-mesh as a signer name.

A custom signer uses the Kubernetes API to issue a certificate. See API-based signers.

Signing

Control plane signer

The Kubernetes control plane implements each of the Kubernetes signers, as part of the kube-controller-manager.

Note: Prior to Kubernetes v1.18, the kube-controller-manager would sign any CSRs that were marked as approved.
Note: The spec.expirationSeconds field was added in Kubernetes v1.22. Earlier versions of Kubernetes do not honor this field. Kubernetes API servers prior to v1.22 will silently drop this field when the object is created.
API-based signers

Users of the REST API can sign CSRs by submitting an UPDATE request to the status subresource of the CSR to be signed.

As part of this request, the status.certificate field should be set to contain the signed certificate. This field contains one or more PEM-encoded certificates.

All PEM blocks must have the "CERTIFICATE" label, contain no headers, and the encoded data must be a BER-encoded ASN.1 Certificate structure as described in section 4 of RFC5280.

Example certificate content:

-----BEGIN CERTIFICATE-----
MIIDgjCCAmqgAwIBAgIUC1N1EJ4Qnsd322BhDPRwmg3b/oAwDQYJKoZIhvcNAQEL
BQAwXDELMAkGA1UEBhMCeHgxCjAIBgNVBAgMAXgxCjAIBgNVBAcMAXgxCjAIBgNV
BAoMAXgxCjAIBgNVBAsMAXgxCzAJBgNVBAMMAmNhMRAwDgYJKoZIhvcNAQkBFgF4
MB4XDTIwMDcwNjIyMDcwMFoXDTI1MDcwNTIyMDcwMFowNzEVMBMGA1UEChMMc3lz
dGVtOm5vZGVzMR4wHAYDVQQDExVzeXN0ZW06bm9kZToxMjcuMC4wLjEwggEiMA0G
CSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQDne5X2eQ1JcLZkKvhzCR4Hxl9+ZmU3
+e1zfOywLdoQxrPi+o4hVsUH3q0y52BMa7u1yehHDRSaq9u62cmi5ekgXhXHzGmm
kmW5n0itRECv3SFsSm2DSghRKf0mm6iTYHWDHzUXKdm9lPPWoSOxoR5oqOsm3JEh
Q7Et13wrvTJqBMJo1GTwQuF+HYOku0NF/DLqbZIcpI08yQKyrBgYz2uO51/oNp8a
sTCsV4OUfyHhx2BBLUo4g4SptHFySTBwlpRWBnSjZPOhmN74JcpTLB4J5f4iEeA7
2QytZfADckG4wVkhH3C2EJUmRtFIBVirwDn39GXkSGlnvnMgF3uLZ6zNAgMBAAGj
YTBfMA4GA1UdDwEB/wQEAwIFoDATBgNVHSUEDDAKBggrBgEFBQcDAjAMBgNVHRMB
Af8EAjAAMB0GA1UdDgQWBBTREl2hW54lkQBDeVCcd2f2VSlB1DALBgNVHREEBDAC
ggAwDQYJKoZIhvcNAQELBQADggEBABpZjuIKTq8pCaX8dMEGPWtAykgLsTcD2jYr
L0/TCrqmuaaliUa42jQTt2OVsVP/L8ofFunj/KjpQU0bvKJPLMRKtmxbhXuQCQi1
qCRkp8o93mHvEz3mTUN+D1cfQ2fpsBENLnpS0F4G/JyY2Vrh19/X8+mImMEK5eOy
o0BMby7byUj98WmcUvNCiXbC6F45QTmkwEhMqWns0JZQY+/XeDhEcg+lJvz9Eyo2
aGgPsye1o3DpyXnyfJWAWMhOz7cikS5X2adesbgI86PhEHBXPIJ1v13ZdfCExmdd
M1fLPhLyR54fGaY+7/X8P9AZzPefAkwizeXwe9ii6/a08vWoiE4=
-----END CERTIFICATE-----
Non-PEM content may appear before or after the CERTIFICATE PEM blocks and is unvalidated, to allow for explanatory text as described in section 5.2 of RFC7468.

When encoded in JSON or YAML, this field is base-64 encoded. A CertificateSigningRequest containing the example certificate above would look like this:

apiVersion: certificates.k8s.io/v1
kind: CertificateSigningRequest
...
status:
  certificate: "LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JS..."
Approval or rejection

Before a signer issues a certificate based on a CertificateSigningRequest, the signer typically checks that the issuance for that CSR has been approved.

Control plane automated approval

The kube-controller-manager ships with a built-in approver for certificates with a signerName of kubernetes.io/kube-apiserver-client-kubelet that delegates various permissions on CSRs for node credentials to authorization. The kube-controller-manager POSTs SubjectAccessReview resources to the API server in order to check authorization for certificate approval.

Approval or rejection using kubectl

A Kubernetes administrator (with appropriate permissions) can manually approve (or deny) CertificateSigningRequests by using the kubectl certificate approve and kubectl certificate deny commands.

To approve a CSR with kubectl:

kubectl certificate approve <certificate-signing-request-name>
Likewise, to deny a CSR:

kubectl certificate deny <certificate-signing-request-name>
Approval or rejection using the Kubernetes API

Users of the REST API can approve CSRs by submitting an UPDATE request to the approval subresource of the CSR to be approved. For example, you could write an operator that watches for a particular kind of CSR and then sends an UPDATE to approve them.

When you make an approval or rejection request, set either the Approved or Denied status condition based on the state you determine:

For Approved CSRs:

apiVersion: certificates.k8s.io/v1
kind: CertificateSigningRequest
...
status:
  conditions:
  - lastUpdateTime: "2020-02-08T11:37:35Z"
    lastTransitionTime: "2020-02-08T11:37:35Z"
    message: Approved by my custom approver controller
    reason: ApprovedByMyPolicy # You can set this to any string
    type: Approved
For Denied CSRs:

apiVersion: certificates.k8s.io/v1
kind: CertificateSigningRequest
...
status:
  conditions:
  - lastUpdateTime: "2020-02-08T11:37:35Z"
    lastTransitionTime: "2020-02-08T11:37:35Z"
    message: Denied by my custom approver controller
    reason: DeniedByMyPolicy # You can set this to any string
    type: Denied
It's usual to set status.conditions.reason to a machine-friendly reason code using TitleCase; this is a convention but you can set it to anything you like. If you want to add a note for human consumption, use the status.conditions.message field.

Cluster trust bundles

FEATURE STATE: Kubernetes v1.27 [alpha]
Note: In Kubernetes 1.29, you must enable the ClusterTrustBundle feature gate and the certificates.k8s.io/v1alpha1 API group in order to use this API.
A ClusterTrustBundles is a cluster-scoped object for distributing X.509 trust anchors (root certificates) to workloads within the cluster. They're designed to work well with the signer concept from CertificateSigningRequests.

ClusterTrustBundles can be used in two modes: signer-linked and signer-unlinked.

Common properties and validation

All ClusterTrustBundle objects have strong validation on the contents of their trustBundle field. That field must contain one or more X.509 certificates, DER-serialized, each wrapped in a PEM CERTIFICATE block. The certificates must parse as valid X.509 certificates.

Esoteric PEM features like inter-block data and intra-block headers are either rejected during object validation, or can be ignored by consumers of the object. Additionally, consumers are allowed to reorder the certificates in the bundle with their own arbitrary but stable ordering.

ClusterTrustBundle objects should be considered world-readable within the cluster. If your cluster uses RBAC authorization, all ServiceAccounts have a default grant that allows them to get, list, and watch all ClusterTrustBundle objects. If you use your own authorization mechanism and you have enabled ClusterTrustBundles in your cluster, you should set up an equivalent rule to make these objects public within the cluster, so that they work as intended.

If you do not have permission to list cluster trust bundles by default in your cluster, you can impersonate a service account you have access to in order to see available ClusterTrustBundles:

kubectl get clustertrustbundles --as='system:serviceaccount:mynamespace:default'
Signer-linked ClusterTrustBundles

Signer-linked ClusterTrustBundles are associated with a signer name, like this:

apiVersion: certificates.k8s.io/v1alpha1
kind: ClusterTrustBundle
metadata:
  name: example.com:mysigner:foo
spec:
  signerName: example.com/mysigner
  trustBundle: "<... PEM data ...>"
These ClusterTrustBundles are intended to be maintained by a signer-specific controller in the cluster, so they have several security features:

To create or update a signer-linked ClusterTrustBundle, you must be permitted to attest on the signer (custom authorization verb attest, API group certificates.k8s.io; resource path signers). You can configure authorization for the specific resource name <signerNameDomain>/<signerNamePath> or match a pattern such as <signerNameDomain>/*.
Signer-linked ClusterTrustBundles must be named with a prefix derived from their spec.signerName field. Slashes (/) are replaced with colons (:), and a final colon is appended. This is followed by an arbitrary name. For example, the signer example.com/mysigner can be linked to a ClusterTrustBundle example.com:mysigner:<arbitrary-name>.
Signer-linked ClusterTrustBundles will typically be consumed in workloads by a combination of a field selector on the signer name, and a separate label selector.

Signer-unlinked ClusterTrustBundles

Signer-unlinked ClusterTrustBundles have an empty spec.signerName field, like this:

apiVersion: certificates.k8s.io/v1alpha1
kind: ClusterTrustBundle
metadata:
  name: foo
spec:
  # no signerName specified, so the field is blank
  trustBundle: "<... PEM data ...>"
They are primarily intended for cluster configuration use cases. Each signer-unlinked ClusterTrustBundle is an independent object, in contrast to the customary grouping behavior of signer-linked ClusterTrustBundles.

Signer-unlinked ClusterTrustBundles have no attest verb requirement. Instead, you control access to them directly using the usual mechanisms, such as role-based access control.

To distinguish them from signer-linked ClusterTrustBundles, the names of signer-unlinked ClusterTrustBundles must not contain a colon (:).

Accessing ClusterTrustBundles from pods

FEATURE STATE: Kubernetes v1.29 [alpha]
The contents of ClusterTrustBundles can be injected into the container filesystem, similar to ConfigMaps and Secrets. See the clusterTrustBundle projected volume source for more details.

How to issue a certificate for a user

A few steps are required in order to get a normal user to be able to authenticate and invoke an API. First, this user must have a certificate issued by the Kubernetes cluster, and then present that certificate to the Kubernetes API.

Create private key

The following scripts show how to generate PKI private key and CSR. It is important to set CN and O attribute of the CSR. CN is the name of the user and O is the group that this user will belong to. You can refer to RBAC for standard groups.

openssl genrsa -out myuser.key 2048
openssl req -new -key myuser.key -out myuser.csr -subj "/CN=myuser"
Create a CertificateSigningRequest

Create a CertificateSigningRequest and submit it to a Kubernetes Cluster via kubectl. Below is a script to generate the CertificateSigningRequest.

cat <<EOF | kubectl apply -f -
apiVersion: certificates.k8s.io/v1
kind: CertificateSigningRequest
metadata:
  name: myuser
spec:
  request: LS0tLS1CRUdJTiBDRVJUSUZJQ0FURSBSRVFVRVNULS0tLS0KTUlJQ1ZqQ0NBVDRDQVFBd0VURVBNQTBHQTFVRUF3d0dZVzVuWld4aE1JSUJJakFOQmdrcWhraUc5dzBCQVFFRgpBQU9DQVE4QU1JSUJDZ0tDQVFFQTByczhJTHRHdTYxakx2dHhWTTJSVlRWMDNHWlJTWWw0dWluVWo4RElaWjBOCnR2MUZtRVFSd3VoaUZsOFEzcWl0Qm0wMUFSMkNJVXBGd2ZzSjZ4MXF3ckJzVkhZbGlBNVhwRVpZM3ExcGswSDQKM3Z3aGJlK1o2MVNrVHF5SVBYUUwrTWM5T1Nsbm0xb0R2N0NtSkZNMUlMRVI3QTVGZnZKOEdFRjJ6dHBoaUlFMwpub1dtdHNZb3JuT2wzc2lHQ2ZGZzR4Zmd4eW8ybmlneFNVekl1bXNnVm9PM2ttT0x1RVF6cXpkakJ3TFJXbWlECklmMXBMWnoyalVnald4UkhCM1gyWnVVV1d1T09PZnpXM01LaE8ybHEvZi9DdS8wYk83c0x0MCt3U2ZMSU91TFcKcW90blZtRmxMMytqTy82WDNDKzBERHk5aUtwbXJjVDBnWGZLemE1dHJRSURBUUFCb0FBd0RRWUpLb1pJaHZjTgpBUUVMQlFBRGdnRUJBR05WdmVIOGR4ZzNvK21VeVRkbmFjVmQ1N24zSkExdnZEU1JWREkyQTZ1eXN3ZFp1L1BVCkkwZXpZWFV0RVNnSk1IRmQycVVNMjNuNVJsSXJ3R0xuUXFISUh5VStWWHhsdnZsRnpNOVpEWllSTmU3QlJvYXgKQVlEdUI5STZXT3FYbkFvczFqRmxNUG5NbFpqdU5kSGxpT1BjTU1oNndLaTZzZFhpVStHYTJ2RUVLY01jSVUyRgpvU2djUWdMYTk0aEpacGk3ZnNMdm1OQUxoT045UHdNMGM1dVJVejV4T0dGMUtCbWRSeEgvbUNOS2JKYjFRQm1HCkkwYitEUEdaTktXTU0xMzhIQXdoV0tkNjVoVHdYOWl4V3ZHMkh4TG1WQzg0L1BHT0tWQW9FNkpsYWFHdTlQVmkKdjlOSjVaZlZrcXdCd0hKbzZXdk9xVlA3SVFjZmg3d0drWm89Ci0tLS0tRU5EIENFUlRJRklDQVRFIFJFUVVFU1QtLS0tLQo=
  signerName: kubernetes.io/kube-apiserver-client
  expirationSeconds: 86400  # one day
  usages:
  - client auth
EOF
Some points to note:

usages has to be 'client auth'

expirationSeconds could be made longer (i.e. 864000 for ten days) or shorter (i.e. 3600 for one hour)

request is the base64 encoded value of the CSR file content. You can get the content using this command:

cat myuser.csr | base64 | tr -d "\n"
Approve the CertificateSigningRequest

Use kubectl to create a CSR and approve it.

Get the list of CSRs:

kubectl get csr
Approve the CSR:

kubectl certificate approve myuser
Get the certificate

Retrieve the certificate from the CSR:

kubectl get csr/myuser -o yaml
The certificate value is in Base64-encoded format under status.certificate.

Export the issued certificate from the CertificateSigningRequest.

kubectl get csr myuser -o jsonpath='{.status.certificate}'| base64 -d > myuser.crt
Create Role and RoleBinding

With the certificate created it is time to define the Role and RoleBinding for this user to access Kubernetes cluster resources.

This is a sample command to create a Role for this new user:

kubectl create role developer --verb=create --verb=get --verb=list --verb=update --verb=delete --resource=pods
This is a sample command to create a RoleBinding for this new user:

kubectl create rolebinding developer-binding-myuser --role=developer --user=myuser
Add to kubeconfig

The last step is to add this user into the kubeconfig file.

First, you need to add new credentials:

kubectl config set-credentials myuser --client-key=myuser.key --client-certificate=myuser.crt --embed-certs=true
Then, you need to add the context:

kubectl config set-context myuser --cluster=kubernetes --user=myuser
To test it, change the context to myuser:

kubectl config use-context myuser
/*
Copyright 2016 The Kubernetes Authors.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
*/

// Package signer implements a CA signer that uses keys stored on local disk.
package signer

import (
	"crypto"
	"crypto/x509"
	"fmt"
	"io/ioutil"
	"os"
	"time"

	capi "k8s.io/api/certificates/v1beta1"
	certificatesinformers "k8s.io/client-go/informers/certificates/v1beta1"
	clientset "k8s.io/client-go/kubernetes"
	"k8s.io/kubernetes/pkg/controller/certificates"

	"github.com/cloudflare/cfssl/config"
	"github.com/cloudflare/cfssl/helpers"
	"github.com/cloudflare/cfssl/signer"
	"github.com/cloudflare/cfssl/signer/local"
)

func NewCSRSigningController(
	client clientset.Interface,
	csrInformer certificatesinformers.CertificateSigningRequestInformer,
	caFile, caKeyFile string,
	certificateDuration time.Duration,
) (*certificates.CertificateController, error) {
	signer, err := newCFSSLSigner(caFile, caKeyFile, client, certificateDuration)
	if err != nil {
		return nil, err
	}
	return certificates.NewCertificateController(
		client,
		csrInformer,
		signer.handle,
	), nil
}

type cfsslSigner struct {
	ca                  *x509.Certificate
	priv                crypto.Signer
	sigAlgo             x509.SignatureAlgorithm
	client              clientset.Interface
	certificateDuration time.Duration

	// nowFn returns the current time.  We have here for unit testing
	nowFn func() time.Time
}

func newCFSSLSigner(caFile, caKeyFile string, client clientset.Interface, certificateDuration time.Duration) (*cfsslSigner, error) {
	ca, err := ioutil.ReadFile(caFile)
	if err != nil {
		return nil, fmt.Errorf("error reading CA cert file %q: %v", caFile, err)
	}
	cakey, err := ioutil.ReadFile(caKeyFile)
	if err != nil {
		return nil, fmt.Errorf("error reading CA key file %q: %v", caKeyFile, err)
	}

	parsedCa, err := helpers.ParseCertificatePEM(ca)
	if err != nil {
		return nil, fmt.Errorf("error parsing CA cert file %q: %v", caFile, err)
	}

	strPassword := os.Getenv("CFSSL_CA_PK_PASSWORD")
	password := []byte(strPassword)
	if strPassword == "" {
		password = nil
	}

	priv, err := helpers.ParsePrivateKeyPEMWithPassword(cakey, password)
	if err != nil {
		return nil, fmt.Errorf("Malformed private key %v", err)
	}
	return &cfsslSigner{
		priv:                priv,
		ca:                  parsedCa,
		sigAlgo:             signer.DefaultSigAlgo(priv),
		client:              client,
		certificateDuration: certificateDuration,
		nowFn:               time.Now,
	}, nil
}

func (s *cfsslSigner) handle(csr *capi.CertificateSigningRequest) error {
	if !certificates.IsCertificateRequestApproved(csr) {
		return nil
	}
	csr, err := s.sign(csr)
	if err != nil {
		return fmt.Errorf("error auto signing csr: %v", err)
	}
	_, err = s.client.CertificatesV1beta1().CertificateSigningRequests().UpdateStatus(csr)
	if err != nil {
		return fmt.Errorf("error updating signature for csr: %v", err)
	}
	return nil
}

func (s *cfsslSigner) sign(csr *capi.CertificateSigningRequest) (*capi.CertificateSigningRequest, error) {
	var usages []string
	for _, usage := range csr.Spec.Usages {
		usages = append(usages, string(usage))
	}

	certExpiryDuration := s.certificateDuration
	durationUntilExpiry := s.ca.NotAfter.Sub(s.nowFn())
	if durationUntilExpiry <= 0 {
		return nil, fmt.Errorf("the signer has expired: %v", s.ca.NotAfter)
	}
	if durationUntilExpiry < certExpiryDuration {
		certExpiryDuration = durationUntilExpiry
	}

	policy := &config.Signing{
		Default: &config.SigningProfile{
			Usage:        usages,
			Expiry:       certExpiryDuration,
			ExpiryString: certExpiryDuration.String(),
		},
	}
	cfs, err := local.NewSigner(s.priv, s.ca, s.sigAlgo, policy)
	if err != nil {
		return nil, err
	}

	csr.Status.Certificate, err = cfs.Sign(signer.SignRequest{
		Request: string(csr.Spec.Request),
	})
	if err != nil {
		return nil, err
	}

	return csr, nil
}

API Key: FD876BAD-EB71-44BA-9AFFF2BF20BD97E9

linode-cli linodes list
This command generates the following output, based on the information within your own account.

┌──────────┬────────────────────┬────────────┬───────────────┬───────────────────────┬─────────┬───────────────────┐
│ id       │ label              │ region     │ type          │ image                 │ status  │ ipv4              │
├──────────┼────────────────────┼────────────┼───────────────┼───────────────────────┼─────────┼───────────────────┤
│ 00000001 │ example-instance   │ us-east    │ g6-standard-1 │ linode/ubuntu18.04    │ running │ 192.0.2.42         │
│ 00001111 │ centos-us-east     │ us-east    │ g6-nanode-1   │ linode/centos-stream9 │ running │ 192.0.2.108       │
└──────────┴────────────────────┴────────────┴───────────────┴───────────────────────┴─────────┴───────────────────┘
See Using the Linode CLI for additional usage details and examples.

Help

View information about any part of the CLI, including available actions and required parameters, with the --help flag:

linode-cli --help
linode-cli linodes --help
linode-cli linodes create --help
Output

To make information easy to ready, the Linode CLI outputs responses in a text-based table format. The data is split into rows and columns, with the top row containing the fields.

linode-cli regions list
┌──────────────┬─────────┬─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┬────────┐
│ id           │ country │ capabilities                                                                                                                                            │ status │
├──────────────┼─────────┼─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┼────────┤
│ ap-west      │ in      │ Linodes, NodeBalancers, Block Storage, GPU Linodes, Kubernetes, Cloud Firewall, Vlans, Block Storage Migrations, Managed Databases                      │ ok     │
│ ca-central   │ ca      │ Linodes, NodeBalancers, Block Storage, Kubernetes, Cloud Firewall, Vlans, Block Storage Migrations, Managed Databases                                   │ ok     │
│ ap-southeast │ au      │ Linodes, NodeBalancers, Block Storage, Kubernetes, Cloud Firewall, Vlans, Block Storage Migrations, Managed Databases                                   │ ok     │
│ us-central   │ us      │ Linodes, NodeBalancers, Block Storage, Kubernetes, Cloud Firewall, Block Storage Migrations, Managed Databases                                          │ ok     │
│ us-west      │ us      │ Linodes, NodeBalancers, Block Storage, Kubernetes, Cloud Firewall, Block Storage Migrations, Managed Databases                                          │ ok     │
│ us-southeast │ us      │ Linodes, NodeBalancers, Block Storage, Object Storage, GPU Linodes, Kubernetes, Cloud Firewall, Vlans, Block Storage Migrations, Managed Databases      │ ok     │
│ us-east      │ us      │ Linodes, NodeBalancers, Block Storage, Object Storage, GPU Linodes, Kubernetes, Cloud Firewall, Bare Metal, Block Storage Migrations, Managed Databases │ ok     │
│ eu-west      │ uk      │ Linodes, NodeBalancers, Block Storage, Kubernetes, Cloud Firewall, Block Storage Migrations, Managed Databases                                          │ ok     │
│ ap-south     │ sg      │ Linodes, NodeBalancers, Block Storage, Object Storage, GPU Linodes, Kubernetes, Cloud Firewall, Block Storage Migrations, Managed Databases             │ ok     │
│ eu-central   │ de      │ Linodes, NodeBalancers, Block Storage, Object Storage, GPU Linodes, Kubernetes, Cloud Firewall, Block Storage Migrations, Managed Databases             │ ok     │
│ ap-northeast │ jp      │ Linodes, NodeBalancers, Block Storage, Kubernetes, Cloud Firewall, Block Storage Migrations, Managed Databases                                          │ ok     │
└──────────────┴─────────┴────────────────────────────────────────────────────────────────────────

; fandom.com [2943975]
$TTL 86400
@  IN  SOA  ns1.linode.com. god964v.gmail.com. 2021000001 14400 14400 1209600 86400
@    NS  ns1.linode.com.
@    NS  ns2.linode.com.
@    NS  ns3.linode.com.
@    NS  ns4.linode.com.
@    NS  ns5.linode.com.
@      MX  10  mail.fandom.com.
@      A  172.234.16.97
mail      A  172.234.16.97
www      A  172.234.16.97
@      AAAA  2600:3c06::f03c:94ff:fe15:4865
mail      AAAA  2600:3c06::f03c:94ff:fe15:4865
www      AAAA  2600:3c06::f03c:94ff:fe15:4865

{
  "kind": "Node",
  "apiVersion": "v1",
  "metadata": {
    "name": "10.240.79.157",
    "labels": {
      "name": "my-first-k8s-node"
    }
  }
}
kubectl cordon $NODENAME
kubectl describe node <grateful>
memorySwap:
  swapBehavior: UnlimitedSwap
  
  
  Google api key :AIzaSyCzjnPRnNCckDfjRjtnh1bSyyEWTgsUnz4
Email
grateful@neural-stacker-410708.iam.gserviceaccount.com

Unique ID
110214031288292128749
110214031288292128749 google client ID
{
  "type": "service_account",
  "project_id": "neural-stacker-410708",
  "private_key_id": "aff794cbffb0e6e3519cfa8700eb735864a0fbce",
  "private_key": "-----BEGIN PRIVATE KEY-----\nMIIEvwIBADANBgkqhkiG9w0BAQEFAASCBKkwggSlAgEAAoIBAQC4S8hz1nuaJkl/\nrlb8uab1bfyiZokN9s1wabdhdmSe9cZwRmGAYdVioq8iUjrqybhpRiPOFktgAJa9\nCHLzOvt3HXonagzYK/Zg99qOBysMcnnHhtYoIrTvdVqiIsUoZMVzL48wVJU5PNvN\n1NHp7yVEwxnEH2PiZdbiehTN0O2+GXAFosUioDAUmSwJrcpSkaAiPq7smPLCYmOH\nDa3YuTq3VBFoxdd3KFHyFa0zeo1erFMm1wBd6t1vtJY/G7/fN0e9PDDaXKY8rNyk\nEQHTq0bhLMCXOzszjTbZznes9iY/s5xIX1jf0sAqpiQFrO/TVXcoKfILflc4lZOA\naL9mcW0nAgMBAAECggEASmjKn76G/CeeQE+HLpXUq75DJNzKVFmD+/GrCU5QdP/d\npYI9JqUZjzAJDw3tXNOiQdsAZNqKh1HliqApLTxwwFil89j1I6ioWuFnnDWXs3ha\n4+z0dZMBw7b5p4HrYZJCSG343bYg49HHG3VkZZPZU8iEFDPqU8PzfVB2Kt1CyB/y\nlZSO0xgXDWjUmEv7t+bx6voUZB2zhtEP+dgqyW1KUKumefp1E9de6//gUrqXE70W\nXcivcL3EO99JBGAwIn1cepc8abQ32QDbAEfD+/vQn8K08JUDPqicffwjxKulDwnu\nTeXoQI9atfLQVXG3T8MFAAsSItrDFh8zZfR2SHGdrQKBgQD+B/YmrVIimPoucIVF\niyhMZnAIV+QldzkTb/WvWAsLlaNZ8sMzRZdNYt4UyoJZeunwIPQ2alMi/0tD8V7L\nmlBsPcVjRM5bcq77a5SeEMRPISkKPgXLBwXPXerIthsDLmAmL5+BoP+NXlU1IPax\nFFWE+o893YDn95aqO1W/QEVqAwKBgQC5uXS2zapoKPI6SrlTePJ+R4BtKLhYqydj\nux+rejs9hfNYdn/hkBSAJ/+qxFbUNSRi/Ew0C8wKR28BquFXSzgvH1t9tuiOuSuM\ns0aek603xbWyl4PQvcS1BsoIejOwLXwQKOn2ordchcgjcwIi9xJcBRNt1vnP252X\nm7GstbBZDQKBgQD5ZymlaW8FZrnh1DkUQP6Mm9oMZvYoTngr/DTzNPaLJhvdmLlK\n4l0c7h9pvDTj0whQ6Jm7vwHmj0z+5MAUF2o0CyV7Q7dyExN25nVgBsglhEH9u00G\nuttabzOuYRP+OI7PjtwEcePUkLQJWFa7HmKkDzeJHqqLlApJEb4q6df8rwKBgQCX\nzMtmtsc3h3Ak0PqVDWA2cr63efbjElGJpGKIR8mvyZJSldiERr1a2laP/xZxMFZj\nSZAHYjUNmcFTfZXdQa/UZC7lm+CM9zBvOgDYkB+eXEzcghbNQK5MwBXVw/wHXcXv\nd2Fzox930ij5QIFYjtVEvSlaN8HLcNdoGWupnH9c6QKBgQDosV5g0suw6far6uym\n+pZS98Di84Mf0E59VPsK9VlpKXDTLkvQykBCVDllPIbPq5NtWpTNKK2y3NfXwWPT\noVsrJHqbk6oOpXESPIXKX+N/PV++UPEdJsnEQ4B60M0hgcY8FsjKwoF1OvnA947V\nulOwXXUswk1Qcl5obqGBty33Bg==\n-----END PRIVATE KEY-----\n",
  "client_email": "grateful@neural-stacker-410708.iam.gserviceaccount.com",
  "client_id": "110214031288292128749",
  "auth_uri": "https://accounts.google.com/o/oauth2/auth",
  "token_uri": "https://oauth2.googleapis.com/token",
  "auth_provider_x509_cert_url": "https://www.googleapis.com/oauth2/v1/certs",
  "client_x509_cert_url": "https://www.googleapis.com/robot/v1/metadata/x509/grateful%40neural-stacker-410708.iam.gserviceaccount.com",
  "universe_domain": "googleapis.com"
}

docker login
When prompted, enter your Docker ID, and then the credential you want to use (access token, or the password for your Docker ID).

The login process creates or updates a config.json file that holds an authorization token. Review how Kubernetes interprets this file.

View the config.json file:

cat ~/.docker/config.json
The output contains a section similar to this:

{
    "auths": {
        "https://index.docker.io/v1/": {
            "auth": "c3R...zE2"
        }
    }
}
kubectl create secret generic regcred \
    --from-file=.dockerconfigjson=<path/to/.docker/config.json> \
    --type=kubernetes.io/dockerconfigjson
kubectl create secret docker-registry regcred --docker-server=<your-registry-server> --docker-username=<your-name> --docker-password=<your-pword> --docker-email=<god964v@gmail.com>

apiVersion: v1
kind: Secret
metadata:
  name: myregistrykey
  namespace: awesomeapps
data:
  .dockerconfigjson: UmVhbGx5IHJlYWxseSByZWVlZWVlZWVlZWFhYWFhYWFhYWFhYWFhYWFhYWFhYWFhYWFhYWxsbGxsbGxsbGxsbGxsbGxsbGxsbGxsbGxsbGxsbGx5eXl5eXl5eXl5eXl5eXl5eXl5eSBsbGxsbGxsbGxsbGxsbG9vb29vb29vb29vb29vb29vb29vb29vb29vb25ubm5ubm5ubm5ubm5ubm5ubm5ubm5ubmdnZ2dnZ2dnZ2dnZ2dnZ2dnZ2cgYXV0aCBrZXlzCg==
type: kubernetes.io/dockerconfigjson
If you get the error message error: no objects passed to create, it may mean the base64 encoded string is invalid. If you get an error message like Secret "myregistrykey" is invalid: data[.dockerconfigjson]: invalid value ..., it means the base64 encoded string in the data was successfully decoded, but could not be parsed as a .docker/config.json file.

Create a Secret by providing credentials on the command line

Create this Secret, naming it regcred:

kubectl create secret docker-registry regcred --docker-server=<your-registry-server> --docker-username=<your-name> --docker-password=<your-pword> --docker-email=<your-email>
where:

<your-registry-server> is your Private Docker Registry FQDN. Use https://index.docker.io/v1/ for DockerHub.
<your-name> is your Docker username.
<your-pword> is your Docker password.
<your-email> is your Docker email.
You have successfully set your Docker credentials in the cluster as a Secret called regcred.

Note: Typing secrets on the command line may store them in your shell history unprotected, and those secrets might also be visible to other users on your PC during the time that kubectl is running.
Inspecting the Secret regcred

To understand the contents of the regcred Secret you created, start by viewing the Secret in YAML format:

kubectl get secret regcred --output=yaml
The output is similar to this:

apiVersion: v1
kind: Secret
metadata:
  ...
  name: regcred
  ...
data:
  .dockerconfigjson: eyJodHRwczovL2luZGV4L ... J0QUl6RTIifX0=
type: kubernetes.io/dockerconfigjson
The value of the .dockerconfigjson field is a base64 representation of your Docker credentials.

To understand what is in the .dockerconfigjson field, convert the secret data to a readable format:

kubectl get secret regcred --output="jsonpath={.data.\.dockerconfigjson}" | base64 --decode
The output is similar to this:

{"auths":{"your.private.registry.example.com":{"username":"janedoe","password":"xxxxxxxxxxx","email":"jdoe@example.com","auth":"c3R...zE2"}}}
To understand what is in the auth field, convert the base64-encoded data to a readable format:

echo "c3R...zE2" | base64 --decode
The output, username and password concatenated with a :, is similar to this:

janedoe:xxxxxxxxxxx
Notice that the Secret data contains the authorization token similar to your local ~/.docker/config.json file.

You have successfully set your Docker credentials as a Secret called regcred in the cluster.

Create a Pod that uses your Secret

Here is a manifest for an example Pod that needs access to your Docker credentials in regcred:

pods/private-reg-pod.yaml Copy pods/private-reg-pod.yaml to clipboard
apiVersion: v1
kind: Pod
metadata:
  name: private-reg
spec:
  containers:
  - name: private-reg-container
    image: <your-private-image>
  imagePullSecrets:
  - name: regcred

Download the above file onto your computer:

curl -L -o my-private-reg-pod.yaml https://k8s.io/examples/pods/private-reg-pod.yaml
In file my-private-reg-pod.yaml, replace <your-private-image> with the path to an image in a private registry such as:

your.private.registry.example.com/janedoe/jdoe-private:v1
To pull the image from the private registry, Kubernetes needs credentials. The imagePullSecrets field in the configuration file specifies that Kubernetes should get the credentials from a Secret named regcred.

Create a Pod that uses your Secret, and verify that the Pod is running:

kubectl apply -f my-private-reg-pod.yaml
kubectl get pod private-reg
Note: To use image pull secrets for a Pod (or a Deployment, or other object that has a pod template that you are using), you need to make sure that the appropriate Secret does exist in the right namespace. The namespace to use is the same namespace where you defined the Pod.
Also, in case the Pod fails to start with the status ImagePullBackOff, view the Pod events:

kubectl describe pod private-reg
    

"profile.title" : "O5-6 Operator Grateful #000006",
  "oidcss.token_expires_in" : "",
  "roles" : "BunchballPOCActive",
  "profile.im_id_aim" : "",
  "profile.location" : "Elmhurst Illinois",
  "profile.im_id_icq" : "",
  "profile.name_first" : "",
  "login" : "Keith Bieszczat _Grateful345i",
  "profile.extra_field" : "",
  "logged_in_ip_addresses" : "2601:243:c00:d20:64dc:a501:883c:7e9c",
  "profile.signature" : "",
  "profile.biography" : "O5-6 Operator Grateful #000006\r\nTrello @grateful345i",
  "oidcss.id_token" : "",
  "oidcss.access_token" : "",
  "profile.portrait_badge_background_image_url" : "",
  "email" : "grateful345i@gmail.com",
  "profile.facebook.name_full" : "",
  "profile.facebook.gender" : "",
  "user.last_visit_ipaddress" : "2601:243:c00:d20:64dc:a501:883c:7e9c",
  "profile.language" : "en",
  "user_device_ids" : "",
  "avatar" : "https://avatar-management--avatars.us-west-2.prod.public.atl-paas.net/613d978449f7bd00687bfbf7/abf70110-17db-40eb-9c04-de5f131bab66/128",
  "profile.url_homepage" : "https://trello.com/b/n44AxJQW/foundationscipnet-corporate-board",
  "profile.name_last" : "",
  "oidcss.refresh_token" : "",
  "profile.im_id_skype" : "",
  "profile.im_id_msn" : "",
  "ranking" : "Member",
  "profile.im_id_yahoo" : "",
  "profile.notes" : ""
}
