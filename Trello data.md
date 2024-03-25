<script src="https://gist.github.com/grateful345/6a1e6a5f9b35747e91dde193b1306bb2.js"></script>
curl -s https://lv.linode.com/FDC71C6F-66B3-4FDA-8FE2187096708C8E | sudo bash
API Key: 14496832-187E-4897-8D420686F1A72ACB
curl -s https://lv.linode.com/3DEB7746-4E73-460A-B491CAA57C71DE9B | sudo bash

Manual installation instructions
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
