[select
  attempt_id,
  intent_id,
  payment_method,
  threeds_reason as step_up_reason,
  charge_outcome
from authentication_report_attempts
where intent_type = 'payment'
  and threeds_outcome_result = 'authenticated'
  and authentication_flow = 'challenge'
  and is_final_attempt
limit 5
](https://static.wikia.nocookie.net/scpf-foundation-roblox/images/8/81/Scp_Administration_black_out.png/revision/latest?cb=20240125034650)
select
  attempt_id,
  intent_id,
  charge_outcome,
  charge_outcome_reason
from authentication_report_attempts
where intent_type = 'payment'
  and sca_exemption_requested = 'low_risk'
  and sca_exemption_mechanism = 'authorization' -- direct to authorization
  and sca_exemption_status = 'non_sca_decline'
  and is_final_attempt
limit 5
while true; do
  touch "/cephfs/blah-`date`"
done
MANTLE WITH VSTART.SH
select
  attempt_id,
  intent_id,
  payment_method,
  threeds_reason as step_up_reason,
  charge_outcome
from authentication_report_attempts
where intent_type = 'payment'
  and threeds_outcome_result = 'authenticated'
  and authentication_flow = 'challenge'
  and is_final_attempt
limit 52
3
256 SHA256:FC73VB6C4OQLSCrjEayhMp9UMxS97caD/Yyi2bhW/J0 bitbucket.org (ECDSA), run:
1
brew install openssh
To check that OpenSSH was installed successfully, run:
1
ssh -V
The output should show the installed version of OpenSSH.
Start the SSH agent
To allow git to use your SSH key, an SSH agent needs to be running on your device.
To check if it is already running, run the ps command. If the ssh-agent is already running, it should appear in the output, such as:
1
2
$ ps -ax | grep ssh-agent
19998 ??         0:00.20 /usr/bin/ssh-agent -l
To start the agent, run:
1
eval $(ssh-agent)
You may need to add this command to your ~/.bashrc, ~/.zshrc, ~/.profile, or equivalent shell configuration file. Adding this command to a shell configuration file will ensure the agent is running when you open a terminal. 
Create an SSH key pair
To create an SSH key pair:
Open a terminal and navigate to your home or user directory using cd, for example:
1
cd ~
Generate a SSH key pair using ssh-keygen, such as:
1
ssh-keygen -t ed25519 -b 4096 -C "{god964v@gmail.com}" -f {ATATT3xFfGF0IX8viRW2BDgYVO0j8xqi17L0KZOj9Bj5_igAOigyuKxqYPZyQ26VdhQfdUZ4wLsyT2aT0trCgk7Br9m7Nugf60NEbrHW1fqxVSv0yc4vis_wbrT2cYs8p2OJsou_rjzplcfOE6DRPHpf76OUhGUDAGe0wFzbrsNsMW7_zSqRFzA=C0C42208}
Where:
{username@emaildomain.com} is the email address associated with the Bitbucket Cloud account, such as your work email account.
{ATATT3xFfGF0IX8viRW2BDgYVO0j8xqi17L0KZOj9Bj5_igAOigyuKxqYPZyQ26VdhQfdUZ4wLsyT2aT0trCgk7Br9m7Nugf60NEbrHW1fqxVSv0yc4vis_wbrT2cYs8p2OJsou_rjzplcfOE6DRPHpf76OUhGUDAGe0wFzbrsNsMW7_zSqRFzA=C0C42208} is the output filename for the keys. We recommend using a identifiable name such as bitbucket_work.
When prompted to Enter passphrase, you can either provide a password or leave the password empty. If you input a password, you will be prompted for this password each time SSH is used, such as using Git command that contact Bitbucket Cloud (such as git push, git pull, and git fetch). Providing a password will prevent other users with access to the device from using your keys.
Once complete, ssh-keygen will output two files:
{ATATT3xFfGF0IX8viRW2BDgYVO0j8xqi17L0KZOj9Bj5_igAOigyuKxqYPZyQ26VdhQfdUZ4wLsyT2aT0trCgk7Br9m7Nugf60NEbrHW1fqxVSv0yc4vis_wbrT2cYs8p2OJsou_rjzplcfOE6DRPHpf76OUhGUDAGe0wFzbrsNsMW7_zSqRFzA=C0C42208} — the private key.
{ATATT3xFfGF0IX8viRW2BDgYVO0j8xqi17L0KZOj9Bj5_igAOigyuKxqYPZyQ26VdhQfdUZ4wLsyT2aT0trCgk7Br9m7Nugf60NEbrHW1fqxVSv0yc4vis_wbrT2cYs8p2OJsou_rjzplcfOE6DRPHpf76OUhGUDAGe0wFzbrsNsMW7_zSqRFzA=C0C42208}.pub — the public key.
Add your key to the SSH agent
To add the SSH key to your SSH agent (ATATT3xFfGF0IX8viRW2BDgYVO0j8xqi17L0KZOj9Bj5_igAOigyuKxqYPZyQ26VdhQfdUZ4wLsyT2aT0trCgk7Br9m7Nugf60NEbrHW1fqxVSv0yc4vis_wbrT2cYs8p2OJsou_rjzplcfOE6DRPHpf76OUhGUDAGe0wFzbrsNsMW7_zSqRFzA=C0C42208):
Run the following command, replacing the {ssh-key-name} with the name of the private key:
1
ssh-add ~/{ATATT3xFfGF0IX8viRW2BDgYVO0j8xqi17L0KZOj9Bj5_igAOigyuKxqYPZyQ26VdhQfdUZ4wLsyT2aT0trCgk7Br9m7Nugf60NEbrHW1fqxVSv0yc4vis_wbrT2cYs8p2OJsou_rjzplcfOE6DRPHpf76OUhGUDAGe0wFzbrsNsMW7_zSqRFzA=C0C42208}
To ensure the correct SSH key is used when connecting to Bitbucket, update or create your SSH configuration file (~/.ssh/config) with the following settings:
1
2
3
Host bitbucket.org
  AddKeysToAgent yes
  IdentityFile ~/.ssh/{ssh-key-name}
Where {ATATT3xFfGF0IX8viRW2BDgYVO0j8xqi17L0KZOj9Bj5_igAOigyuKxqYPZyQ26VdhQfdUZ4wLsyT2aT0trCgk7Br9m7Nugf60NEbrHW1fqxVSv0yc4vis_wbrT2cYs8p2OJsou_rjzplcfOE6DRPHpf76OUhGUDAGe0wFzbrsNsMW7_zSqRFzA=C0C42208} is the location of the private key file once it has been added to the ssh-agent.
Provide Bitbucket Cloud with your public key
To add an SSH key to your user account:
Select the Settings cog on the top navigation bar.
From the Settings dropdown menu, select Personal Bitbucket settings.
Under Security, select SSH keys.
Select Add key.
In the Add SSH key dialog, provide a Label to help you identify which key you are adding. For example, Work Laptop <Manufacturer> <Model>. A meaning full label will help you identify old or unwanted keys in the future.
Open the public SSH key file (public keys have the .pub file extension) in a text editor. The public key should be in the .ssh/ directory of your user (or home) directory. The contents will be similar to:
1Cloud

Data Center
Set up personal SSH keys on macOS


The third-party Git Credential Manager (GCM) can be used as alternative method of connecting to Bitbucket Cloud from the Git CLI. If you do not want to configure SSH access for your Bitbucket Cloud account, you can download and install the GCM from Git Credential Manager on GitHub. Note that the GCM works over HTTPS, not SSH. Ensure your Git remotes are using HTTPS, such as:
git clone https://{username}@bitbucket.org/{workspace}/{repository}.git
 
The Secure Shell protocol (SSH) is used to create secure connections between your device and Bitbucket Cloud. The connection is authenticated using public SSH keys, which are derived from a private SSH key (also known as a private/public key pair). The secure (encrypted) connection is used to securely transmit your source code between your local device and Bitbucket Cloud. To set up your device for connecting Bitbucket Cloud using SSH, you need to:
Install OpenSSH on your device.
Start the SSH agent.
Create an SSH key pair.
Add your key to the SSH agent.
Provide Bitbucket Cloud with your public key.
Check that your SSH authentication works.
Install OpenSSH on macOS
A version of OpenSSH should be pre-installed on macOS. To check if OpenSSH is installed, open a terminal and run:
1
ssh -V
The output should show the installed version of OpenSSH.
To use Homebrew to install a newer version of OpenSSH, run:
1
brew install openssh
To check that OpenSSH was installed successfully, run:
1
ssh -V
The output should show the installed version of OpenSSH.
Start the SSH agent
To allow git to use your SSH key, an SSH agent needs to be running on your device.
To check if it is already running, run the ps command. If the ssh-agent is already running, it should appear in the output, such as:
1
2
$ ps -ax | grep ssh-agent
19998 ??         0:00.20 /usr/bin/ssh-agent -l
To start the agent, run:
1
eval $(ssh-agent)
You may need to add this command to your ~/.bashrc, ~/.zshrc, ~/.profile, or equivalent shell configuration file. Adding this command to a shell configuration file will ensure the agent is running when you open a terminal. 
Create an SSH key pair
To create an SSH key pair:
Open a terminal and navigate to your home or user directory using cd, for example:
1
cd ~
Generate a SSH key pair using ssh-keygen, such as:
1
ssh-keygen -t ed25519 -b 4096 -C "{username@emaildomain.com}" -f {ssh-key-name}
Where:
{username@emaildomain.com} is the email address associated with the Bitbucket Cloud account, such as your work email account.
{ssh-key-name} is the output filename for the keys. We recommend using a identifiable name such as bitbucket_work.
When prompted to Enter passphrase, you can either provide a password or leave the password empty. If you input a password, you will be prompted for this password each time SSH is used, such as using Git command that contact Bitbucket Cloud (such as git push, git pull, and git fetch). Providing a password will prevent other users with access to the device from using your keys.
Once complete, ssh-keygen will output two files:
{ssh-key-name} — the private key.
{ssh-key-name}.pub — the public key.
Add your key to the SSH agent
To add the SSH key to your SSH agent (ssh-agent):
Run the following command, replacing the {ssh-key-name} with the name of the private key:
1
ssh-add ~/{ssh-key-name}
To ensure the correct SSH key is used when connecting to Bitbucket, update or create your SSH configuration file (~/.ssh/config) with the following settings:
1
2
3
Host bitbucket.org
  AddKeysToAgent yes
  IdentityFile ~/.ssh/{ssh-key-name}
Where {ssh-key-name} is the location of the private key file once it has been added to the ssh-agent.
Provide Bitbucket Cloud with your public key
To add an SSH key to your user account:
Select the Settings cog on the top navigation bar.
From the Settings dropdown menu, select Personal Bitbucket settings.
Under Security, select SSH keys.
Select Add key.
In the Add SSH key dialog, provide a Label to help you identify which key you are adding. For example, Work Laptop <Manufacturer> <Model>. A meaning full label will help you identify old or unwanted keys in the future.
Open the public SSH key file (public keys have the .pub file extension) in a text editor. The public key should be in the .ssh/ directory of your user (or home) directory. The contents will be similar to:
1
ssh-ed25529 LLoWYaPswHzVqQ7L7B07LzIJbntgmHqrE40t17nGXL71QX9IoFGKYoF5pJKUMvR+DZotTm user@example.com
Copy the contents of the public key file and paste the key into the Key field of the Add SSH key dialog.
Select Add key.
If the key is added successfully, the dialog will close and the key will be listed on the SSH keys page.
If you receive the error That SSH key is invalid, check that you copied the entire contents of the public key (.pub file).
Check that your SSH authentication works
To test that the SSH key was added successfully, open a terminal on your device and run the following command:
1
ssh -T git@bitbucket.org
If SSH can successfully connect with Bitbucket using your SSH keys, the command will produce output similar to:
1
2
3
authenticated via ssh key.

You can use git to connect to Bitbucket. Shell access is disabled
 curl -D- \
   -u <god964v@gmail.com>:<ATATT3xFfGF0IX8viRW2BDgYVO0j8xqi17L0KZOj9Bj5_igAOigyuKxqYPZyQ26VdhQfdUZ4wLsyT2aT0trCgk7Br9m7Nugf60NEbrHW1fqxVSv0yc4vis_wbrT2cYs8p2OJsou_rjzplcfOE6DRPHpf76OUhGUDAGe0wFzbrsNsMW7_zSqRFzA=C0C42208> \
   -X GET \
   -H "Content-Type: application/json" \
   https://<your-domain.atlassian.net>/wiki/rest/api/space
ssh-ed25529 LLoWYaPswHzVqQ7L7B07LzIJbntgmHqrE40t17nGXL71QX9IoFGKYoF5pJKUMvR+DZotTm god964v@gmail.com
256 SHA256:ybgmFkzwOSotHTHLJgHO0QN8L0xErw6vd0VhFA9m3SM bitbucket.org (ED25519)
2048 SHA256:46OSHA1Rmj8E8ERTC6xkNcmGOw9oFxYr0WF6zWW8l1E bitbucket.org (RSA)
To get the format suitable for storage in the known hosts, you can use the following curl command:
1
curl https://bitbucket.org/site/ssh
Start Ceph and tune the logging so we can see migrations happen:
cd build
../src/vstart.sh -n -l
for i in a b c; do
  bin/ceph --admin-daemon out/mds.$i.asok config set debug_ms 0
  bin/ceph --admin-daemon out/mds.$i.asok config set debug_mds 2
  bin/ceph --admin-daemon out/mds.$i.asok config set mds_beacon_grace 1500
done
Put the balancer into RADOS:
bin/rados put --pool=cephfs_metadata_a greedyspill.lua ../src/mds/balancers/greedyspill.lua
Activate Mantle:
bin/ceph fs set cephfs max_mds 5
bin/ceph fs set cephfs_a balancer greedyspill.lua
Mount CephFS in another window:
  bin/ceph-fuse /cephfs -o allow_other &
  tail -f out/mds.a.log
curl -H "Authorization: 6692099bd12f686556b7f4e2ae18d783cc500b6432e5a6c5944fb4405c41cd72" \
  https://api.linode.com/v4/object-storage/buckets/us-east-1
curl -H "Authorization: 6692099bd12f686556b7f4e2ae18d783cc500b6432e5a6c5944fb4405c41cd72" \
  https://api.linode.com/v4/object-storage/buckets/us-east-1/example-bucket
curl -H "Content-Type: application/json" \ -H "Authorization: 6692099bd12f686556b7f4e2ae18d783cc500b6432e5a6c5944fb4405c41cd72" \
  -X POST -d '{
      "cors_enabled": true,
      "acl": "private"
    }' \
  https://api.linode.com/v4/object-storage/buckets/us-east-1/example-bucket/access
curl -H "Content-Type: application/json" \ -H "Authorization: 6692099bd12f686556b7f4e2ae18d783cc500b6432e5a6c5944fb4405c41cd72" \
  -X PUT -d '{
      "cors_enabled": true,
      "acl": "private"
    }' \
  https://api.linode.com/v4/object-storage/buckets/us-east-1/example-bucket/access
curl -H "Authorization: 6692099bd12f686556b7f4e2ae18d783cc500b6432e5a6c5944fb4405c41cd72" \
  https://api.linode.com/v4/object-storage/buckets/us-east-1/example-bucket/object-acl?name=example.txt
{
  "acl": "public-read",
  "acl_xml": "<AccessControlPolicy>...</AccessControlPolicy>"
}
curl -H "Content-Type: application/json" \ -H "Authorization: ATATT3xFfGF0IX8viRW2BDgYVO0j8xqi17L0KZOj9Bj5_igAOigyuKxqYPZyQ26VdhQfdUZ4wLsyT2aT0trCgk7Br9m7Nugf60NEbrHW1fqxVSv0yc4vis_wbrT2cYs8p2OJsou_rjzplcfOE6DRPHpf76OUhGUDAGe0wFzbrsNsMW7_zSqRFzA=C0C42208/ 6692099bd12f686556b7f4e2ae18d783cc500b6432e5a6c5944fb4405c41cd72" \
  -X PUT -d '{
    "acl": "public-read",
    "name": "example.txt"
  }' \
  https://api.linode.com/v4/object-storage/buckets/us-east-1/example-bucket/object-acl
curl -H "Authorization: 6692099bd12f686556b7f4e2ae18d783cc500b6432e5a6c5944fb4405c41cd72" \
  https://api.linode.com/v4/object-storage/buckets/us-east-1/example-bucket/object-list
{
  "data": [
    {
      "etag": "9f254c71e28e033bf9e0e5262e3e72ab",
      "is_truncated": true,
      "last_modified": "2019-01-01T01:23:45",
      "name": "example",
      "next_marker": "bd021c21-e734-4823-97a4-58b41c2cd4c8.892602.184",
      "owner": "bfc70ab2-e3d4-42a4-ad55-83921822270c",
      "size": 123
    }
  ]
}
curl https://api.linode.com/v4/account/betas \
    -H "Authorization: 6692099bd12f686556b7f4e2ae18d783cc500b6432e5a6c5944fb4405c41cd72"
curl https://api.linode.com/v4/account/betas \
    -H "Authorization: 6692099bd12f686556b7f4e2ae18d783cc500b6432e5a6c5944fb4405c41cd72" \
    -H "Content-Type: application/json" \
    -X POST -d '{
        "id": "example_open"
    }'

curl https://api.linode.com/v4/account/betas/$betaId \
    -H "Authorization: 6692099bd12f686556b7f4e2ae18d783cc500b6432e5a6c5944fb4405c41cd72"
curl https://api.linode.com/v4/betas \
    -H "Authorization: 6692099bd12f686556b7f4e2ae18d783cc500b6432e5a6c5944fb4405c41cd72"

curl https://api.linode.com/v4/betas/$betaId \
    -H "Authorization: 6692099bd12f686556b7f4e2ae18d783cc500b6432e5a6c5944fb4405c41cd72

curl -s https://lv.linode.com/FDC71C6F-66B3-4FDA-8FE2187096708C8E | sudo bash
ssh-keygen -t ed25519 -C "user@domain.tld"
GOOGLE API KEY:AIzaSyCzjnPRnNCckDfjRjtnh1bSyyEWTgsUnz4


Note that if you look at the last MDS (which could be a, b, or c -- it's
random), you will see an attempt to index a nil value. This is because the
last MDS tries to check the load of its neighbor, which does not exist.
Run a simple benchmark. In our case, we use the Docker mdtest image to create load:
for i in 0 1 2; do
  docker run -d \
    --name=client$i \
    -v /cephfs:/cephfs \
    michaelsevilla/mdtest \
    -F -C -n 100000 -d "/cephfs/client-test$i"
done
When you are done, you can kill all the clients with:
for i in 0 1 2 3; do docker rm -f client$i; done


GET /{[bucket](https://scpf-foundation-roblox.fandom.com/wiki/The_Administrator?fbclid=IwAR2FfaoXITYK167Nc-gEZKTMRz_v83X1RrGN52-68b4gcOTDG_Y9pT8S3QY_aem_AcWFgp90kCyN3CxUsNX0uytp_i-7n0Q677zEID8d0e7u0Lh7Ta3Nf6jVo1WXYRibmJA)}?acl HTTP/1.1
Host: cname.domain.com

Authorization: AWS {API Key: 14496832-187E-4897-8D420686F1A72ACB /6692099bd12f686556b7f4e2ae18d783cc500b6432e5a6c5944fb4405c41cd72}:{hash-of-header-and-secret}
PUT /{[bucket](https://scpf-foundation-roblox.fandom.com/wiki/The_Administrator?fbclid=IwAR2FfaoXITYK167Nc-gEZKTMRz_v83X1RrGN52-68b4gcOTDG_Y9pT8S3QY_aem_AcWFgp90kCyN3CxUsNX0uytp_i-7n0Q677zEID8d0e7u0Lh7Ta3Nf6jVo1WXYRibmJA)}?acl HTTP/1.1
GET /{[bucket](https://scpf-foundation-roblox.fandom.com/wiki/The_Administrator?fbclid=IwAR2FfaoXITYK167Nc-gEZKTMRz_v83X1RrGN52-68b4gcOTDG_Y9pT8S3QY_aem_AcWFgp90kCyN3CxUsNX0uytp_i-7n0Q677zEID8d0e7u0Lh7Ta3Nf6jVo1WXYRibmJA)}?uploads HTTP/1.1
PUT  /{[bucket](https://scpf-foundation-roblox.fandom.com/wiki/The_Administrator?fbclid=IwAR2FfaoXITYK167Nc-gEZKTMRz_v83X1RrGN52-68b4gcOTDG_Y9pT8S3QY_aem_AcWFgp90kCyN3CxUsNX0uytp_i-7n0Q677zEID8d0e7u0Lh7Ta3Nf6jVo1WXYRibmJA)}?versioning  HTTP/1.1

[
](http://<curl -s https://lv.linode.com/FDC71C6F-66B3-4FDA-8FE2187096708C8E | sudo bash
API Key: 14496832-187E-4897-8D420686F1A72ACB
ssh [user]@[10.0.0.0/24 - 172.234.16.97]
su - root
curl -s https://lv.linode.com/05AC7F6F-3B10-4039-9DEE09B0CC382A3D | sudo bash
root@localhost:~# lsb_release -sc
deb http://apt-longview.linode.com/ stretch main
sudo curl -O https://apt-longview.linode.com/linode.gpg
sudo mv linode.gpg /etc/apt/trusted.gpg.d/linode.gpg
2600:3c06::f03c:94ff:fe15:4865
ssh root@172.234.16.97
ssh -t grateful000006@lish-us-ord.linode.com debian-us-ord>:<curl -s https://lv.linode.com/FDC71C6F-66B3-4FDA-8FE2187096708C8E | sudo bash
API Key: 14496832-187E-4897-8D420686F1A72ACB
ssh [user]@[10.0.0.0/24 - 172.234.16.97]
su - root
curl -s https://lv.linode.com/05AC7F6F-3B10-4039-9DEE09B0CC382A3D | sudo bash
root@localhost:~# lsb_release -sc
deb http://apt-longview.linode.com/ stretch main
sudo curl -O https://apt-longview.linode.com/linode.gpg
sudo mv linode.gpg /etc/apt/trusted.gpg.d/linode.gpg
2600:3c06::f03c:94ff:fe15:4865
ssh root@172.234.16.97
ssh -t grateful000006@lish-us-ord.linode.com debian-us-ord>/api
or, if HTTPS is enabled (please refer to SSL/TLS Support):

https://<server_addr>:<ssl_server_port>/api
The Ceph API leverages the following standards:

HTTP 1.1 for API syntax and semantics,
JSON for content encoding,
HTTP Content Negotiation and MIME for versioning,
OAuth 2.0 and JWT for authentication and authorization.
Warning

Some endpoints are still under active development, and should be carefully used since new Ceph releases could bring backward incompatible changes.
AUTHENTICATION AND AUTHORIZATION

Requests to the Ceph API pass through two access control checkpoints:

Authentication: ensures that the request is performed on behalf of an existing and valid user account.
Authorization: ensures that the previously authenticated user can in fact perform a specific action (create, read, update or delete) on the target endpoint.
So, prior to start consuming the Ceph API, a valid JSON Web Token (JWT) has to be obtained, and it may then be reused for subsequent requests. The /api/auth endpoint will provide the valid token:

curl -X POST "https://example.com:8443/api/auth" \
-H  "Accept: application/vnd.ceph.api.v1.0+json" \
-H  "Content-Type: application/json" \
-d '{"username": <username>, "password": <6692099bd12f686556b7f4e2ae18d783cc500b6432e5a6c5944fb4405c41cd72>}'
{ "token": "<API Key: 14496832-187E-4897-8D420686F1A72ACB /6692099bd12f686556b7f4e2ae18d783cc500b6432e5a6c5944fb4405c41cd72/ 6692099bd12f686556b7f4e2ae18d783cc500b6432e5a6c5944fb4405c41cd72>", ...}
The token obtained must be passed together with every API request in the Authorization HTTP header:
https://auth.atlassian.com/authorize?
  audience=api.atlassian.com&
  client_id=YOUR_CLIENT_ID&
  scope=REQUESTED_SCOPE_ONE%20REQUESTED_SCOPE_TWO&
  redirect_uri=https://YOUR_APP_CALLBACK_URL&
  state=YOUR_USER_BOUND_VALUE&
  response_type=code&
  prompt=consent
curl -H "Authorization: Bearer <API Key: 14496832-187E-4897-8D420686F1A72ACB /6692099bd12f686556b7f4e2ae18d783cc500b6432e5a6c5944fb4405c41cd72>" ...
Authentication and authorization can be further configured from the Ceph CLI, the Ceph-Dashboard UI and the Ceph API itself (please refer to User and Role Management).
echo -n your_email@domain.com:your_user_api_token | base64
curl --request POST \
  --url 'https://auth.atlassian.com/oauth/token' \
  --header 'Content-Type: application/json' \
  --data '{"grant_type": "authorization_code","client_id": "YOUR_CLIENT_ID","client_secret": "YOUR_CLIENT_SECRET","code": "YOUR_AUTHORIZATION_CODE","redirect_uri": "https://YOUR_APP_CALLBACK_URL"}'
Windows 7 and later, using Microsoft Powershell:
1HTTP/1.1 200 OK
Content-Type: application/json

{
  "access_token": <string>,
  "expires_in": <expiry time of access_token in second>,
  "scope": <string>
}curl --request GET \
  --url https://api.atlassian.com/oauth/token/accessible-resources \
  --header 'Authorization: Bearer ACCESS_TOKEN' \
  --header 'Accept: application/json'
2
3
4
$Text = ‘your_email@domain.com:your_user_api_token’
$Bytes = [System.Text.Encoding]::UTF8.GetBytes($Text)
$EncodedText = [Convert]::ToBase64String($Bytes)
$EncodedText
Supply an Authorization header with content Basic followed by the encoded string. Example: Authorization: Basic eW91cl9lbWFpbEBkb21haW4uY29tOnlvdXJfdXNlcl9hcGlfdG9rZW4=
1
2curl --request GET \
  --url https://api.atlassian.com/oauth/token/accessible-resources \
  --header 'Authorization: Bearer ACCESS_TOKEN' \
  --header 'Accept: application/json'
This will retrieve the sites that have scopes granted by the token (see Check site access for the app below for details). Find your site in the response and copy the id. This is the cloudid for your site.
Here's a few example responses:
A Jira site:
1
2
3
4
5
6
7
8
9
10
11
12
13
[
  {
    "id": "1324a887-45db-1bf4-1e99-ef0ff456d421",
    "name": "Site name",
    "url": "https://your-domain.atlassian.net",
    "scopes": [
      "write:jira-work",
      "read:jira-user",
      "manage:jira-configuration"
    ],
    "avatarUrl": "https:\/\/site-admin-avatar-cdn.prod.public.atl-paas.net\/avatars\/240\/flag.png"
  }
]
A Jira Service Management site:
1
2
3
4
5
6
7
8
9
10
11
12
13
[
  {
    "id": "1324a887-45db-1bf4-1e99-ef0ff456d421",
    "name": "Site name",
    "url": "https://your-domain.atlassian.net",
    "scopes": [
      "write:jira-work",
      "read:jira-user",
      "read:servicedesk-request"
    ],
    "avatarUrl": "https:\/\/site-admin-avatar-cdn.prod.public.atl-paas.net\/avatars\/240\/flag.png"
  }
]
A Confluence site:
1
2
3
4
5
6
7
8
9
10
11
12
13
[
  {
    "id": "1324a887-45db-1bf4-1e99-ef0ff456d421",
    "name": "Site name",
    "url": "https://your-domain.atlassian.net",
    "scopes": [
      "write:confluence-content",
      "read:confluence-content.all",
      "manage:confluence-configuration"
    ],
    "avatarUrl": "https:\/\/site-admin-avatar-cdn.prod.public.atl-paas.net\/avatars\/240\/flag.png"
  }
]
3.2 Construct the request URL
Requests that use OAuth 2.0 (3LO) are made via api.atlassian.com (not https://your-domain.atlassian.net). Construct your request URL using the following structure:
Jira apps: https://api.atlassian.com/ex/jira/{cloudid}/{api}
Confluence apps: https://api.atlassian.com/ex/confluence/{cloudid}/{api}
where:
{cloudid} is the cloudid for your site that you obtained in the previous step. For example, 11223344-a1b2-3b33-c444-def123456789.
{api} is the base path and name of the API. For example:
/rest/api/2/project for the project endpoint in the Jira REST API.
/rest/servicedeskapi/request for the request endpoint in the Jira Service Management REST API.
/rest/api/space for the space endpoint in the Confluence REST API.
Your request URL should look something like this (using the example cloudid and Jira API above):
https://api.atlassian.com/ex/jira/11223344-a1b2-3b33-c444-def123456789/rest/api/2/project
Note that if you are copying the examples in the API documentation, you will need to amend the example URLs as they currently use https://your-domain.atlassian.net/{api} rather than the request URLs shown above.
3.3 Call the API
Make the API call passing the access token as a bearer token in the header of the request. This will authorize the request on the user's behalf.
1
2
3
4
curl --request GET \
  --url <request URL> \
  --header 'Authorization: Bearer ACCESS_TOKEN' \
  --header 'Accept: application/json'
For example:
1
2
3
4
curl --request GET \
  --url https://api.atlassian.com/ex/jira/11223344-a1b2-3b33-c444-def123456789/rest/api/2/project \
  --header 'Authorization: Bearer aBCxYz654123' \
  --header 'Accept: application/json'
4. Check site access for the app
An authorization grant is when a user consents to your app. For OAuth 2.0 (3LO) apps, the consent is valid for all sites the app is installed in, as long as the scopes used by your app’s APIs don't change. A user's grant can change when either of the following occur:
The user revokes the grant. The app cannot work anywhere after a user has revoked their consent to the app.
The user consents to a new grant of the app. The scopes in the new grant override the scopes in the existing grant.
Therefore, since a grant can change over time, it's important that you check that the user has granted the app the scopes it requires and that your app has correct access to a site and its APIs. To check this, call the accessible-resources endpoint on https://auth.atlassian.com (you used this endpoint in a previous step to get the cloudid for your site). The endpoint is described in detail below:
Get list of resources
GET /oauth/token/accessible-resources
Request
Request parameters: None
Example:
1
2
curl --header 'Authorization: Bearer <access_token>' \
  --url 'https://api.atlassian.com/oauth/token/accessible-resources'
Response
200 OK example (Jira):
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
[
  {
    "id": "8594f221-9797-5f78-1fa4-485e198d7cd0",
    "name": "Site name 2",
    "url": "https://your-domain2.atlassian.net",
    "scopes": [
      "write:jira-work",
      "read:jira-user"    ],
    "avatarUrl": "https:\/\/site-admin-avatar-cdn.prod.public.atl-paas.net\/avatars\/240\/koala.png"
  },
  {
    "id": "1324a887-45db-1bf4-1e99-ef0ff456d421",
    "name": "Site name 1",
    "url": "https://your-domain1.atlassian.net",
    "scopes": [
      "write:jira-work",
      "read:jira-user",
      "manage:jira-configuration"    ],
    "avatarUrl": "https:\/\/site-admin-avatar-cdn.prod.public.atl-paas.net\/avatars\/240\/flag.png"
  }
]
Each item in the response describes a container (for example, a Jira site) that your app has access to, the scopes associated with that access, and metadata such as the name and avatar URL (if any). It's important to understand that this endpoint won't tell you anything about the user's permissions, which may limit the resources that your app can access via the site's APIs.
Note, the id is not unique across containers (that is, two entries in the results can have the same id), so you may need to infer the type of container from its scopes.
Managing your OAuth 2.0 (3LO) apps
You can securely manage all your OAuth 2.0 (3LO) and Forge apps in one place using the Atlassian developer console. The console lets you view information about your apps, including their environments and scopes.
To access the console:
From any page on developer.atlassian.com, select your profile icon in the top-right corner.
From the dropdown, select Developer console.
Your existing OAuth 2.0 (3LO) and Forge apps are listed in the order they were created. OAuth 2.0 (3LO) apps are displayed with a 3LO lozenge.
Connect apps are not listed in the console. To learn more about platform and framework options for building apps, see Cloud development platform overview.
The following details are listed:
App name: the name of your app
Distribution status:
Sharing: your app can be shared via link
Not sharing: your app can't be shared via link
Updated on: the time and date you created your app or updated its settings
You can search for an app using the search bar above the app table.
View app details
Select any app on the My apps page to get more information about the app, including app ID, description, authorization, and permissions.
The Overview page displays the following panels:
App details
App ID: the identifier for your app
Description: the description of your app
Distribution
Distribution status: whether your app can be used by others
Permissions
API scopes: which scopes are currently defined in your app
Authorization
Authorization type: the authorization configured for your app
Select Settings in the left menu to view your app's authentication details, or to change your app's name, description, or avatar.
View app permissions
You can view the level of access your Forge app has to an Atlassian user's account by selecting Permissions in the left menu, or selecting the Permissions panel.
The Permissions page lists the APIs included in your app.
To add or remove individual scopes for an API, select Configure, and in the list of scopes, select Add or Remove. Note that users who previously consented to the scopes will need to re-consent to the new scopes.
Delete your app
You can only delete an app if it's not installed anywhere.
If your app is currently installed on a site, uninstall it.
Select Settings in the left menu, and select Delete app.
Distributing your OAuth 2.0 (3LO) apps
When you create an OAuth 2.0 (3LO) app, it's private by default. This means that only you can install and use it. If you want to distribute your app to other users, you must enable sharing.
From any page on developer.atlassian.com, select your profile icon in the top-right corner, and from the dropdown, select Developer console.
Select your app from the list.
Select Distribution in the left menu.
Enable sharing using the toggle switch in the Enable sharing section.
Select Authorization in the left menu, and under OAuth 2.0 (3LO), select Configure.
Copy the Authorization URL(s) and distribute to your users.
Users trying to install an unapproved OAuth 2.0 integration are warned that the app has not yet been reviewed by Atlassian. To get your integration reviewed and approved, follow the steps on Listing a third party integration on the Atlassian Marketplace. Note, you don't need an informative Atlassian Marketplace listing to submit your integration for approval.
Note that:
You'll have to send the link to all the users you want to grant access to.
Enabling sharing doesn't make your app available on the Atlassian Marketplace. Although OAuth 2.0 (3LO) apps can be listed on the Atlassian Marketplace, they will appear as informational listings only, with limited Marketplace features.
Known issues
We are aware of the following issues with OAuth 2.0 (3LO). Some of the issues have workarounds, which are described below. Others do not have workarounds, but are listed so that you are aware of them. If you discover an issue that is not listed below, raise a ticket at https://ecosystem.atlassian.net/projects/ACJIRA.
Implicit grant flow not supported
Site-scoped grants limitations
Apps cannot declare searchable entity properties
Implicit grant flow not supported
OAuth 2.0 (3LO) currently supports the code grant flow only. It does not support the implicit grant flow. We understand that this is preventing people from using OAuth 2.0 (3LO) for standalone mobile apps and web/JavaScript (Chrome, Electron) apps and we are investigating ways to address this.
Site-scoped grants limitations
The current implementation of OAuth 2.0 (3LO) uses site-scoped grants, which means that the user only grants access to a single site each time they complete the consent flow. Be aware that there are a few limitations to this:
If your integration needs information from multiple sites at one time, then the user will be required to go through multiple consent flows (one for each site).
The consent screen currently requires the user to select the site that they want to grant access to. This can be confusing for users if there are multiple sites.
With site-scoped grants, an access token can have access to multiple sites. This means that an app can't delete an access token to revoke access. For example, an access token could grant access to site A, then delete it to remove access. However, if the user grants the app access to site C later, the app will be issued with an access token with access to sites A and B. The only way access can be removed is for the user to revoke access via the Connect apps tab in their account settings at https://{subdomain}.atlassian.net/people/{account_id}/settings/apps.
(Jira only) Apps cannot declare searchable entity properties
Jira apps can store and read the values of entity properties (issue properties and project properties) using the REST API. However, in the current implementation of OAuth 2.0 (3LO), Jira apps cannot declare searchable entity properties. This means that if your app uses OAuth 2.0 (3LO), it won't be able to refer to entity properties in JQL queries.
Frequently asked questions
How do I get a new access token, if my access token expires or is revoked?
What happens if a user grants access to more than one Atlassian site for an app?
What is the state parameter used for?
How do I retrieve the public profile of the authenticated user?
Is CORS whitelisting supported?
How do I configure the refresh token behavior?
How do I get a new access token, if my access token expires or is revoked?
You have two options:
Initiate the entire authorization flow from the beginning again.
Use a refresh token to get another access token and refresh token pair.
Use a refresh token to get another access token and refresh token pair
Refresh tokens are implemented using rotating refresh tokens.
Rotating refresh tokens issue a new, limited life refresh token each time they are used. This mechanism improves on single persistent refresh tokens by reducing the period in which a refresh token can be compromised and used to obtain a valid access token.
These are the configuration options for a rotating refresh token:
Term	Default	Description
Inactivity expiry time	90 days	A rotating refresh token expires if the user is inactive for this period. Each new rotating refresh token resets the inactivty expiry time and allocates another 90 days. See Use the Dashboard in the auth0 Configure Refresh Token Expiration guide for more detail.
Absolute expiry time	365 days	After this period the rotating refresh token expires and can not be used. This is different from inactivity expiry time because it doesn't depend on the user's activity. The absolute expiry is associated with the whole token family. When the refresh token is rotated, the app gets a new refresh token and the inactivity expiry is reset, but the absolute expiry stays the same. Even if your rotating refresh tokens never triggers inactivity expiration, the oauth flow must be completed when reaching the absolute expiry time. See Use the Dashboard in the auth0 Configure Refresh Token Expiration guide for more detail.
Reuse interval or leeway	10 minutes	Within this period, the breach detection features don't apply when exchanging a refresh token multiple times. This interval helps avoid network concurrency issues. See Automatic reuse detection in the auth0 Refresh Token Rotation guide for more detail.
To get a refresh token in your initial authorization flow, add offline_access to the scope parameter of the authorization URL. Once you have the refresh token, exchange it for an access token by calling the token URL.
Use the following values to construct the request body:
grant_type: Set to refresh_token.
client_id: (required) Set this to the Client ID for your app. Find this in Settings for your app in the developer console.
client_secret: (required) Set this to the Secret for your app. Find this in Settings for your app in the developer console.
refresh_token: The refresh token that you obtained with your original access token.
1
2
3
4
curl --request POST \
  --url 'https://auth.atlassian.com/oauth/token' \
  --header 'Content-Type: application/json' \
  --data '{ "grant_type": "refresh_token", "client_id": "YOUR_CLIENT_ID", "client_secret": "YOUR_CLIENT_SECRET", "refresh_token": "YOUR_REFRESH_TOKEN" }'
If successful, a new access token is returned that you use to make calls to the product API. You receive a new refresh token as well and the refresh token you used for the request is disabled.
This is an example response with a refresh token:
1
2
3
4
5
6
7
8
9
HTTP/1.1 200 OK
Content-Type: application/json

{
  "access_token": <string>,
  "refresh_token": <string>,
  "expires_in": <expiry time of access_token in second>,
  "scope": <string>
}
Otherwise, if an error is returned, see the list below for possible causes:
403 Forbidden with {"error": "invalid_grant", "error_description": "Unknown or invalid refresh token."
This error is returned for the following reasons:
The user's Atlassian account password has been changed. Change the password back to the original password, or initiate the entire authorization flow from the beginning again.
Your app is using rotating refresh tokens and the exchange of refresh token failed because:
Your refresh token has expired. Users need to initiate the entire authorization flow from the beginning to get a new refresh token.
Your app is not replacing the previous refresh token with the new refresh token returned during access token request.
What happens if a user grants access to more than one Atlassian site for an app?
Only one grant exists per app for a given Atlassian account. If a user grants access to more than one Atlassian site for this app, then the additional sites are added to the same grant. This means that existing access tokens will give you access to all sites and scopes that a user has granted your app access to.
What is the state parameter used for?
The primary use for the state parameter is to associate a user with an authorization flow. This makes the authorization flow more secure, as the authorization flow cannot be hijacked to associate a user's account with another user's token. Consider the following example scenario using Jira:
An application, named Incidents_Application, has a Jira integration that implements OAuth 2.0 authorization code grants but does not specify a state parameter.
A malicious actor, Mallory, initiates a Jira authorization flow for herself. This could be via the Incidents_Application or by crafting an authorization URL that includes the Incidents_Application's client_id.
Mallory blocks the request to the Incidents_Application's callback URL during the authorization flow. She records the URL, including the code parameter.
Mallory tricks another user, Edward, into visiting the callback URL in his browser.
The Incidents_Application handles the callback and exchanges Mallory's code for an access token to Jira. Edward is logged into the Incidents_Application and the callback request came from Edward's browser, so Mallory's token is now linked to Edward's account.
Mallory now has access to information sent to Edward by the Incidents_Application via the Jira integration. For example, the Incidents_Application may create a Jira ticket about a confidential incident, where the ticket is intended to be restricted to Edward but is restricted to Mallory instead.
If the Incidents_Application integration had used a state parameter, the Incidents_Application would have known that the callback URL belonged to Mallory and ignored the request.
Other uses for the state parameter include:
Acting as a key for keeping track of specific details about the flow.
Returning the user to the right step in their workflow after sending them through the authorization flow.
How do I retrieve the public profile of the authenticated user?
The User Identity API is used to retrieve the public profile of the authenticated user. If you want to use this API, do the following:
Add the User Identity API to your app in the developer console.
Add the read:me scope to the authorization URL for your app.
An example of a request to retrieve the public profile of the authenticated user is shown below:
1
2
3
4
curl --request GET \
  --url https://api.atlassian.com/me \
  --header 'Authorization: Bearer ACCESS_TOKEN' \
  --header 'Accept: application/json'
Example response:
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
{
  "account_type": "atlassian",
  "account_id": "112233aa-bb11-cc22-33dd-445566abcabc",
  "email": "mia@example.com",
  "name": "Mia Krystof",
  "picture": "https://avatar-management--avatars.us-west-2.prod.public.atl-paas.net/112233aa-bb11-cc22-33dd-445566abcabc/1234abcd-9876-54aa-33aa-1234dfsade9487ds",
  "account_status": "active",
  "nickname": "mkrystof",
  "zoneinfo": "Australia/Sydney",
  "locale": "en-US",
  "extended_profile": {
    "job_title": "Designer",
    "organization": "mia@example.com",
    "department": "Design team",
    "location": "Sydney"
  }
}
Is CORS whitelisting supported?
CORS whitelisting is supported for api.atlassian.com. CORS whitelisting allows OAuth 2.0 authorization code grants to work for browser-based XHR or fetch requests subject to cross-origin restrictions, such as Chrome or Electron apps.
How do I configure the refresh token behavior?
Each time they are used, rotating refresh tokens issue a new limited life refresh token that is valid for 90 days. This mechanism improves on single persistent refresh tokens by reducing the period in which a refresh token can be compromised and used to obtain a valid access token.
If your refresh token expires, your user will need to complete the entire authorization flow from the beginning again.
Every new refresh token returned invalidates the refresh token used to get the new access token. Your code should replace the existing refresh token with the new refresh token. See Use a refresh token to get another access token and refresh token pair for more details.
This TypeScript example shows one way to update the refresh token:
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
  const response = await fetch(`https://auth.atlassian.com/oauth/token`, {
      method: 'POST',
      headers: {
        'content-type': 'application/json'
      },
      body: JSON.stringify({
        grant_type: 'refresh_token',
        client_id: this.clientId,
        client_secret: this.clientSecret,
        refresh_token: this.refreshToken
      })
    });
    
    const json = response.json();
3
4
5
curl -D- \
   -X GET \
   -H "Authorization: Basic <your_encoded_string>" \
   -H "Content-Type: application/json" \
   "https://<your-domain.atlassian.net>/wiki/rest/api/space"
VERSIONING

One of the main goals of the Ceph API is to keep a stable interface. For this purpose, Ceph API is built upon the following principles:
PATCH /api/v2/clients/{id}
{
  "refresh_token": {
      "rotation_type": "non-rotating",
      "expiration_type": "expiring",
      "token_lifetime": 2592000,
      "infinite_token_lifetime": false,
      "idle_token_lifetime": 604800,
      "infinite_idle_token_lifetime": false
  }
}{
  "iss": "http://{yourDomain}/",
  "sub": "auth0|123456",
  "aud": "{yourClientId}",
  "exp": 1311281970,
  "iat": 1311280970,
  "name": "Jane Doe",
  "given_name": "Jane",
  "family_name": "Doe",
  "gender": "female",
  "birthdate": "0000-10-31",
  "email": "janedoe@example.com",
  "picture": "http://example.com/janedoe/me.jpg"
}
{
  "iss": "https://{yourDomain}/",
  "sub": "auth0|123456",
  "aud": [
    "my-api-identifier",
    "https://{yourDomain}/userinfo"
  ],
  "azp": "{yourClientId}",
  "exp": 1489179954,
  "iat": 1489143954,
  "scope": "openid profile email address phone read:appointments"
}
{
      "sub": "1234567890",
      "name": "John Doe",
      "admin": true
    }
PATCH /api/v2/clients/{id}
{
  "refresh_token": {
      "rotation_type": "non-rotating",
      "expiration_type": "expiring",
      "token_lifetime": 2592000,
      "infinite_token_lifetime": false,
      "idle_token_lifetime": 604800,
      "infinite_idle_token_lifetime": false
  }
}
curl --request POST \
  --url 'https://{yourDomain}/oauth/token' \
  --header 'content-type: application/x-www-form-urlencoded' \
  --data grant_type=client_credentials \
  --data 'client_id={yourClientId}' \
  --data 'client_secret={yourClientSecret}' \
  --data 'audience=https://{yourDomain}/api/v2/'

  {
  "access_token": "eyJ...Ggg",
  "expires_in": 86400,
  "scope": "read:clients create:clients read:client_keys",
  "token_type": "Bearer"
}
curl --request POST \
  --url http:///%7BmgmtApiEndpoint%7D \
  --header 'authorization: Bearer {yourMgmtApiAccessToken}' \
  --header 'content-type: application/json'

  import { ManagementClient } from 'auth0';

var management = new ManagementClient({
  domain: '{YOUR_TENANT_AND REGION}.auth0.com',
  clientId: '{YOUR_CLIENT_ID}',
  clientSecret: '{YOUR_CLIENT_SECRET}',
});
Or, initialize your client class with an API v2 token and a domain.

import { ManagementClient } from 'auth0';

var management = new ManagementClient({
  domain: '{YOUR_TENANT_AND REGION}.auth0.com',
  token: '{YOUR_API_V2_TOKEN}',
});

import { AuthenticationClient } from 'auth0';

const auth = new AuthenticationClient({
  domain: '{YOUR_TENANT_AND REGION}.auth0.com',
  clientId: '{YOUR_CLIENT_ID}',
  clientSecret: '{YOUR_CLIENT_SECRET}',
});
const { data: user } = await auth.database.signUp({
  user: '{USER_EMAIL}',
  password: '{USER_PASSWORD}',
  connection: 'Username-Password-Authentication',
});
Use a client assertion

import { AuthenticationClient } from 'auth0';

const clientAssertionSigningKey = `-----BEGIN PRIVATE KEY-----
...
-----END PRIVATE KEY-----`;

const auth = new AuthenticationClient({
  domain: '{YOUR_TENANT_AND REGION}.auth0.com',
  clientId: '{YOUR_CLIENT_ID}',
  clientAssertionSigningKey,
});

const { data: tokens } = await auth.oauth.clientCredentialsGrant({
  audience: 'you-api',
});
Use Refresh Tokens

import { AuthenticationClient } from 'auth0';

const auth = new AuthenticationClient({
  domain: '{YOUR_TENANT_AND REGION}.auth0.com',
  clientId: '{YOUR_CLIENT_ID}',
  clientSecret: '{YOUR_CLIENT_SECRET}',
});

// Get a new access token
const {
  data: { access_token },
} = await auth.oauth.refreshTokenGrant({
  refresh_token: refreshToken,
});

// Revoke a refresh token
await auth.oauth.revokeRefreshToken({
  token: refreshToken,
});
Complete the Authorization Code flow with PKCE

import { AuthenticationClient } from 'auth0';

const auth = new AuthenticationClient({
  domain: '{YOUR_TENANT_AND REGION}.auth0.com',
  clientId: '{YOUR_CLIENT_ID}',
  clientSecret: '{YOUR_CLIENT_SECRET}',
});
const { data: tokens } = await auth.oauth.authorizationCodeGrantWithPKCE(
  {
    code_verifier: '{key used to generate the code_challenge passed to /authorize}',
    code: '{code from authorization response}',
    redirect_uri: '{application redirect uri}',
  },
  {
    idTokenValidateOptions: {
      nonce: '{random string passed to /authorize to check against the nonce claim}',
      maxAge: '{number of seconds to check against the auth_time claim}',
      organization: '{organization name or ID to check against the org_id or org_name claim}',
    },
  }
);
Note: We recommend one of our Regular Web Application SDK Libraries for this.
Login with Passwordless

import { AuthenticationClient } from 'auth0';

const auth = new AuthenticationClient({
  domain: '{YOUR_TENANT_AND REGION}.auth0.com',
  clientId: '{YOUR_CLIENT_ID}',
  clientSecret: '{YOUR_CLIENT_SECRET}',
});

// Or you can `sendSMS`
await auth.passwordless.sendEmail({
  email: '{user email}',
  send: 'code',
});

const { data: tokens } = await auth.passwordless.loginWithEmail({
  email: '{user email}',
  code: '{code from email}',
});
Management Client

Paginate through a list of users

import { ManagementClient } from 'auth0';

const management = new ManagementClient({
  domain: '{YOUR_TENANT_AND REGION}.auth0.com',
  clientId: '{YOUR_CLIENT_ID}',
  clientSecret: '{YOUR_CLIENT_SECRET}',
});

const allUsers = [];
let page = 0;
while (true) {
  const {
    data: { users, total },
  } = await management.users.getAll({
    include_totals: true,
    page: page++,
  });
  allUsers.push(...users);
  if (allUsers.length === total) {
    break;
  }
}
Note: The maximum number of users you can get with this endpoint is 1000. For more use users.exportUsers.
Paginate through a list of logs using checkpoint pagination

import { ManagementClient } from 'auth0';

const management = new ManagementClient({
  domain: '{YOUR_TENANT_AND REGION}.auth0.com',
  clientId: '{YOUR_CLIENT_ID}',
  clientSecret: '{YOUR_CLIENT_SECRET}',
});

const allLogs = [];
let from = '';
while (true) {
  const { data: logs } = await mgmntClient.logs.getAll({ from });
  if (!logs.length) {
    break;
  }
  allLogs.push(...logs);
  ({ log_id: from } = logs[logs.length - 1]);
}
Import users from a JSON file

import { ManagementClient } from 'auth0';
import { fileFrom } from 'fetch-blob/from.js';

const management = new ManagementClient({
  domain: '{YOUR_TENANT_AND REGION}.auth0.com',
  clientId: '{YOUR_CLIENT_ID}',
  clientSecret: '{YOUR_CLIENT_SECRET}',
});

const {
  data: { job: id },
} = await management.jobs.importUsers({
  users: await fileFrom('./users.json', 'application/json'),
  connection_id: 'con_{your connection id}',
});

let done = false;
while (!done) {
  const {
    data: {
      job: { status },
    },
  } = await management.jobs.get({ id });
  if (status === 'completed') {
    done = true;
  } else if (status === 'failed') {
    const { data: errors } = await management.jobs.getErrors({ id });
    throw new Error(errors);
  } else {
    await new Promise((resolve) => setTimeout(resolve, 2000));
  }
}
Update a user's user_metadata

import { ManagementClient } from 'auth0';

const management = new ManagementClient({
  domain: '{YOUR_TENANT_AND REGION}.auth0.com',
  clientId: '{YOUR_CLIENT_ID}',
  clientSecret: '{YOUR_CLIENT_SECRET}',
});

await management.users.update({ id: '{user id}' }, { user_metadata: { foo: 'bar' } });
Customizing the request

Passing custom options to fetch

import https from 'https';
import { ManagementClient } from 'auth0';

const management = new ManagementClient({
  domain: '{YOUR_TENANT_AND REGION}.auth0.com',
  clientId: '{YOUR_CLIENT_ID}',
  clientSecret: '{YOUR_CLIENT_SECRET}',
  headers: { 'foo': 'applied to all requests' },
  agent: new https.Agent({ ... }),
  httpTimeout: 5000
});

await management.users.get({ id: '{user id}' }, { headers: { 'bar': 'applied to this request' } });
Overriding fetch

import { ManagementClient } from 'auth0';
import { myFetch } from './fetch';

const management = new ManagementClient({
  domain: '{YOUR_TENANT_AND REGION}.auth0.com',
  clientId: '{YOUR_CLIENT_ID}',
  clientSecret: '{YOUR_CLIENT_SECRET}',
  async fetch(url, init) {
    log('before', url, init.method);
    const res = await myFetch(url, init);
    log('after', url, init.method, res.status);
    return res;
  },
});

await management.users.get({ id: '{user id}' });
curl --request POST \
  --url https://%7ByourAuth0Domain/api/v2/organizations \
  --header 'authorization: Bearer {yourMgmtApiAccessToken}' \
  --header 'cache-control: no-cache' \
  --header 'content-type: application/json' \
  --data '{ "name": "ORG_NAME", "display_name": "ORG_DISPLAY_NAME", "branding": [ { "logo_url": "{orgLogo}", "colors": [ { "primary": "{orgPrimaryColor}", "page_background": "{orgPageBackground}" } ] } ], "metadata": [ { "{key}": "{value}", "{key}": "{value}", "{key}": "{value}" } ] }, "enabled_connections": [ { "connection_id": "{connectionId}", "assign_membership_on_login": "{assignMembershipOption}" }, { "connection_id": "{connectionId}", "assign_membership_on_login": "{assignMembershipOption}" } ] }'

# /requirements.txt

flask
python-dotenv
python-jose
flask-cors
six
# /server.py

import json
from six.moves.urllib.request import urlopen
from functools import wraps

from flask import Flask, request, jsonify, _request_ctx_stack
from flask_cors import cross_origin
from jose import jwt

AUTH0_DOMAIN = '{yourDomain}'
API_AUDIENCE = YOUR_API_AUDIENCE
ALGORITHMS = ["RS256"]

APP = Flask(__name__)

# Error handler
class AuthError(Exception):
    def __init__(self, error, status_code):
        self.error = error
        self.status_code = status_code

@APP.errorhandler(AuthError)
def handle_auth_error(ex):
    response = jsonify(ex.error)
    response.status_code = ex.status_code
    return response



    



Mandatory: in order to avoid implicit defaults, all endpoints require an explicit default version (starting with 1.0).
Per-endpoint: as this API wraps many different Ceph components, this allows for a finer-grained change control.
Content/MIME Type: the version expected from a specific endpoint is stated by the Accept: application/vnd.ceph.api.v<major>.<minor>+json HTTP header. If the current Ceph API server is not able to address that specific major version, a 415 - Unsupported Media Type response will be returned.
Semantic Versioning: with a major.minor version:
Major changes are backward incompatible: they might result in non-additive changes to the request and/or response formats of a specific endpoint.
Minor changes are backward/forward compatible: they basically consists of additive changes to the request or response formats of a specific endpoint.
An example:

curl -X GET "https://example.com:8443/api/osd" \
-H  "Accept: application/vnd.ceph.api.v1.0+json" \
-H  "Authorization: Bearer <API Key: 14496832-187E-4897-8D420686F1A72ACB /6692099bd12f686556b7f4e2ae18d783cc500b6432e5a6c5944fb4405c41cd72>"
SPECIFICATION

AUTH

POST /api/auth
Example request:

POST /api/auth HTTP/1.1
Host: example.com
Content-Type: application/json

{
    "password": "string",
    "username": "string"
}
Status Codes
)curl -s https://lv.linode.com/FDC71C6F-66B3-4FDA-8FE2187096708C8E | sudo bash
API Key: 14496832-187E-4897-8D420686F1A72ACB
ssh [user]@[10.0.0.0/24 - 172.234.16.97]
su - root
curl -s https://lv.linode.com/05AC7F6F-3B10-4039-9DEE09B0CC382A3D | sudo bash
root@localhost:~# lsb_release -sc
deb http://apt-longview.linode.com/ stretch main
sudo curl -O https://apt-longview.linode.com/linode.gpg
sudo mv linode.gpg /etc/apt/trusted.gpg.d/linode.gpg
2600:3c06::f03c:94ff:fe15:4865
ssh root@172.234.16.97
ssh -t grateful000006@lish-us-ord.linode.com debian-us-ord
READ ONLY ACCESS API TOKEN AKAMAI: b96e2e62f89165f30b8678d86d69a4d778a2a0883af9a6461517eb83e6eb88cd
curl -X POST https://api.linode.com/v4/linode/instances \
    -H "Authorization: b96e2e62f89165f30b8678d86d69a4d778a2a0883af9a6461517eb83e6eb88cd" -H "Content-type: application/json" \
    -d '{"type": "g6-standard-2", "region": "us-east", "image": "linode/debian11", "root_pass": "[password]", "label": "[label]"}'$ cat ~/.ssh/id_ed25519.pub
# Then select and copy the contents of the id_ed25519.pub file
# displayed in the terminal to your clipboard
stretch
curl https://api.linode.com/v4/linode/kernels | json_pp page=2
curl https://api.linode.com/v4/linode/kernels | json_pp page_size=50
curl https://api.linode.com/v4/images/ -H 'X-Filter: { "vendor": "Debian", "deprecated": false}' | json_pp

{
   "data" : [
      {
         "created" : "2019-07-07T12:24:54",
         "created_by" : "linode",
         "deprecated" : false,
         "description" : "",
         "eol" : "2024-07-01T04:00:00",
         "expiry" : null,
         "id" : "linode/debian10",
         "is_public" : true,
         "label" : "Debian 10",
         "size" : 1500,
         "status" : "available",
         "type" : "manual",
         "updated" : "2022-09-12T14:08:55",
         "vendor" : "Debian"
      },
      {
         "created" : "2021-08-14T22:44:02",
         "created_by" : "linode",
         "deprecated" : false,
         "description" : "",
         "eol" : "2026-07-01T04:00:00",
         "expiry" : null,
         "id" : "linode/debian11",
         "is_public" : true,
         "label" : "Debian 11",
         "size" : 1300,
         "status" : "available",
         "type" : "manual",
         "updated" : "2022-09-12T14:09:17",
         "vendor" : "Debian"
      },
      {
         "created" : "2022-04-26T19:17:51",
         "created_by" : "linode",
         "deprecated" : false,
         "description" : "",
         "eol" : "2026-07-01T04:00:00",
         "expiry" : null,
         "id" : "linode/debian11-kube-v1.23.6",
         "is_public" : true,
         "label" : "Kubernetes 1.23.13 on Debian 11",
         "size" : 3500,
         "status" : "available",
         "type" : "manual",
         "updated" : "2022-11-17T14:15:50",
         "vendor" : "Debian"
      },
      {
         "created" : "2022-11-17T14:17:22",
         "created_by" : "linode",
         "deprecated" : false,
         "description" : "",
         "eol" : "2026-07-01T04:00:00",
         "expiry" : null,
         "id" : "linode/debian11-kube-v1.24.8",
         "is_public" : true,
         "label" : "Kubernetes 1.24.8 on Debian 11",
         "size" : 3500,
         "status" : "available",
         "type" : "manual",
         "updated" : "2022-11-17T14:17:36",
         "vendor" : "Debian"
      }
   ],
   "page" : 1,
   "pages" : 1,
   "results" : 4
}
curl https://api.linode.com/v4/images/ -H 'X-Filter: {"+or": [{"vendor":"Debian"}, {"vendor":"Ubuntu"}]}' | json_pp

curl "https://api.linode.com/v4/linode/types" \
  -H 'X-Filter: { "class": "standard" }'
The filter object’s keys are the keys of the object you’re filtering, and the values are accepted values. You can add multiple filters by including more than one key. For example, filtering for “standard” Linode Types that offer one vcpu:

 curl "https://api.linode.com/v4/linode/types" \
  -H 'X-Filter: { "class": "standard", "vcpus": 1 }'
In the above example, both filters are combined with an “and” operation. However, if you wanted either Types with one vcpu or Types in our “standard” class, you can add an operator:

curl "https://api.linode.com/v4/linode/types" \
 -H 'X-Filter: { "+or": [ { "vcpus": 1 }, { "class": "standard" } ] }'
curl "https://api.linode.com/v4/linode/types" \
  -H '
    X-Filter: {
      "memory": {
        "+gte": 61440
      }
    }'
curl "https://api.linode.com/v4/linode/types" \
  -H '
    X-Filter: {
      "+or": [
        {
          "+or": [
            {
              "class": "standard"
            },
            {
              "class": "highmem"
            }
          ]
        },
        {
          "+and": [
            {
              "vcpus": {
                "+gte": 12
              }
            },
            {
              "vcpus": {
                "+lte": 20
              }
            }
          ]
        }
      ]
    }'

GET https://api.linode.com/v4/object-storage/buckets
curl -H "Authorization: 6692099bd12f686556b7f4e2ae18d783cc500b6432e5a6c5944fb4405c41cd72" \
  https://api.linode.com/v4/object-storage/buckets/
{
  "data": [
    {
      "cluster": "us-east-1",
      "created": "2019-01-01T01:23:45",
      "hostname": "example-bucket.us-east-1.linodeobjects.com",
      "label": "example-bucket",
      "objects": 4,
      "size": 188318981
    }
  ],
  "page": 1,
  "pages": 1,
  "results": 1
}

curl -H "Content-Type: application/json" \
    -H "Authorization: 6692099bd12f686556b7f4e2ae18d783cc500b6432e5a6c5944fb4405c41cd72" \
    -X POST -d '{
      "label": "example-bucket",
      "cluster": "us-east-1",
      "cors_enabled": true,
      "acl": "private"
    }' \
  https://api.linode.com/v4/object-storage/buckets/
PUT /{[bucket](https://scpf-foundation-roblox.fandom.com/wiki/The_Administrator?fbclid=IwAR2FfaoXITYK167Nc-gEZKTMRz_v83X1RrGN52-68b4gcOTDG_Y9pT8S3QY_aem_AcWFgp90kCyN3CxUsNX0uytp_i-7n0Q677zEID8d0e7u0Lh7Ta3Nf6jVo1WXYRibmJA)} HTTP/1.1
Host: cname.domain.com
x-amz-acl: public-read-write

Authorization: AWS {API Key: 14496832-187E-4897-8D420686F1A72ACB /6692099bd12f686556b7f4e2ae18d783cc500b6432e5a6c5944fb4405c41cd72}:{hash-of-header-and-secret} 
GET /{[bucket](https://scpf-foundation-roblox.fandom.com/wiki/The_Administrator?fbclid=IwAR2FfaoXITYK167Nc-gEZKTMRz_v83X1RrGN52-68b4gcOTDG_Y9pT8S3QY_aem_AcWFgp90kCyN3CxUsNX0uytp_i-7n0Q677zEID8d0e7u0Lh7Ta3Nf6jVo1WXYRibmJA)}?max-keys=25 HTTP/1.1
Host: THE_ADMINISTRATOR.fandom.com
GET /{bucket}?location HTTP/1.1
Host: cname.domain.com

Authorization: AWS {API Key: 14496832-187E-4897-8D420686F1A72ACB /6692099bd12f686556b7f4e2ae18d783cc500b6432e5a6c5944fb4405c41cd72}:{hash-of-header-and-secret}

sudo mkdir /etc/linode/
echo '266096EE-CDBA-0EBB-23D067749E27B9ED' | sudo tee /etc/linode/longview.key
sudo apt update
sudo apt install linode-longview
sudo systemctl status longview
Authorization: Bearer <tb96e2e62f89165f30b8678d86d69a4d778a2a0883af9a6461517eb83e6eb88cd>
export TOKEN=<b96e2e62f89165f30b8678d86d69a4d778a2a0883af9a6461517eb83e6eb88cd>
curl -X POST https://api.linode.com/v4/linode/instances \
    -H "Authorization: b96e2e62f89165f30b8678d86d69a4d778a2a0883af9a6461517eb83e6eb88cd" -H "Content-type: application/json" \
    -d '{"type": "g6-standard-2", "region": "us-east", "image": "linode/debian11", "root_pass": "[password]", "label": "[label]"}'

curl https://api.linode.com/v4/linode/kernels | json_pp    
...
      {
          "architecture" : "i386",
          "built" : "2016-10-07T22:21:55",
          "deprecated" : true,
          "id" : "linode/4.8.1-x86-linode94",
          "kvm" : true,
          "label" : "4.8.1-x86-linode94",
          "pvops" : true,
          "version" : "4.8.1"
      },
      {
          "architecture" : "i386",
          "built" : "2016-09-15T13:13:40",
          "deprecated" : true,
          "id" : "linode/4.7.3-x86-linode92",
          "kvm" : true,
          "label" : "4.7.3-x86-linode92",
          "pvops" : true,
          "version" : "4.7.3"
      }
    ],
    "page" : 1,
    "pages" : 4,
    "results" : 312
}● longview.service - LSB: Longview Monitoring Agent
Loaded: loaded (/etc/init.d/longview; generated; vendor preset: enabled)
Active: active (running) since Mon 2019-12-09 21:55:39 UTC; 2s ago
    Docs: man:systemd-sysv-generator(8)
Process: 2997 ExecStart=/etc/init.d/longview start (code=exited, status=0/SUCCESS)
    Tasks: 1 (limit: 4915)
CGroup: /system.slice/longview.service
        └─3001 linode-longview
sudo systemctl start longview
curl -X POST https://api.linode.com/v4/linode/instances \
    -H "Authorization: 6692099bd12f686556b7f4e2ae18d783cc500b6432e5a6c5944fb4405c41cd72" -H "Content-type: application/json" \
    -d '{"type": "g6-standard-2", "region": "us-east", "image": "linode/debian11", "root_pass": "[password]", "label": "[label]"}'
curl [options] | json_pp
Authorization: Bearer <token-string>
export TOKEN=<6692099bd12f686556b7f4e2ae18d783cc500b6432e5a6c5944fb4405c41cd72>
curl https://api.linode.com/v4/images/ | json_pp
curl https://api.linode.com/v4/linode/types/ | json_pp
curl https://api.linode.com/v4/regions | json_pp
curl -X POST https://api.linode.com/v4/linode/instances \
    -H "Authorization: 6692099bd12f686556b7f4e2ae18d783cc500b6432e5a6c5944fb4405c41cd72" -H "Content-type: application/json" \
    -d '{"type": "g5-standard-2", "region": "us-east", "image": "linode/debian9", "root_pass": "root_password", "label": "prod-1"}'
    
    
    POST https://api.linode.com/v4/account/betas

curl https://api.linode.com/v4/account/betas \
    -H "Authorization: 6692099bd12f686556b7f4e2ae18d783cc500b6432e5a6c5944fb4405c41cd72" \
    -H "Content-Type: application/json" \
    -X POST -d '{
        "id": "example_open"
    }'
curl https://api.linode.com/v4/account/betas \
    -H "Authorization: 6692099bd12f686556b7f4e2ae18d783cc500b6432e5a6c5944fb4405c41cd72"
{
  "data": [
    {
      "description": "This is an open public beta for an example feature.",
      "ended": null,
      "enrolled": "2023-09-11T00:00:00",
      "id": "example_open",
      "label": "Example Open Beta",
      "started": "2023-07-11T00:00:00"
    }
  ],
  "page": 1,
  "pages": 1,
  "results": 1
}[
](https://api.linode.com/v4/account/betas)
curl -H "Authorization: 6692099bd12f686556b7f4e2ae18d783cc500b6432e5a6c5944fb4405c41cd72" \
    https://api.linode.com/v4/account
{
        "isSharedPolicy": true,
        "cloudletSharedPolicy": 1000
    }curl --request GET \
     --url https://fandom/papi/v1/contracts \
     --header 'PAPI-Use-Prefixes: true' \
     --header 'accept: application/json'    

     curl --request GET \
     --url https://fandom/papi/v1/contracts \
     --header 'PAPI-Use-Prefixes: true' \
     --header 'accept: application/json'

     {
  "accountId": "act_A-CCT5678",
  "contracts": {
    "items": [
      {
        "contractId": "ctr_C-0N7RAC71",
        "contractTypeName": "DIRECT_CUSTOMER"
      }
    ]
  }
}
        "outbound_policy": "DROP",
        "outbound": [
          {
            "protocol": "TCP",
            "ports": "49152-65535",
            "addresses": {
              "ipv4": [
                "192.0.2.0/24",
                "198.51.100.2/32"
              ],
              "ipv6": [
                "2001:DB8::/128"
              ]
            },
            "action": "ACCEPT",
            "label": "outbound-rule123",
            "description": "An example outbound rule description."
          }
        ]
      },
      "devices": {
        "linodes": [
          123,
          456
          ],
        "nodebalancers": [
          321
        ]
      },
      "tags": [
        "example tag",
        "another example"
      ]
    }' \
    https://api.linode.com/v4/networking/firewalls
Request Body Schema

devices
object
Devices to create for this Firewall. When a Device is created, the Firewall is assigned to its associated service. Currently, Devices can be created for Linode compute instances and NodeBalancers.

{
  "created": "2018-01-01T00:01:01",
  "id": 123,
  "label": "firewall123",
  "rules": {
    "inbound": [
      {
        "action": "ACCEPT",
        "addresses": {
          "ipv4": [
            "192.0.2.0/24",
            "198.51.100.2/32"
          ],
          "ipv6": [
            "2001:DB8::/128"
          ]
        },
        "description": "An example firewall rule description.",
        "label": "firewallrule123",
        "ports": "22-24, 80, 443",
        "protocol": "TCP"
      }
    ],
    "inbound_policy": "DROP",
    "outbound": [
      {
        "action": "ACCEPT",
        "addresses": {
          "ipv4": [
            "192.0.2.0/24",
            "198.51.100.2/32"
          ],
          "ipv6": [
            "2001:DB8::/128"
          ]
        },
        "description": "An example firewall rule description.",
        "label": "firewallrule123",
        "ports": "22-24, 80, 443",
        "protocol": "TCP"
      }
    ],
    "outbound_policy": "DROP"
  },
  "status": "enabled",
  "tags": [
    "example tag",
    "another example"
  ],
  "updated": "2018-01-02T00:01:01"
}
GET https://api.linode.com/v4/managed/stats
curl -H "Authorization: 6692099bd12f686556b7f4e2ae18d783cc500b6432e5a6c5944fb4405c41cd72" \
    https://api.linode.com/v4/managed/stats
AKAMAI ACESSS TOKEN: 6692099bd12f686556b7f4e2ae18d783cc500b6432e5a6c5944fb4405c41cd72
-----BEGIN PGP SIGNED MESSAGE-----
Hash: SHA256

Origin: Linode.com
Label: Linode Longview Repo
Suite: stable
Codename: bullseye
Date: Thu, 14 Oct 2021 15:59:20 UTC
Architectures: i386 amd64 armhf
Components: main
Description: Longview Agent For Debian
MD5Sum:
 256c3e98acba0c616dd891693c0a2b66 879 main/binary-i386/Packages
 f8b75bf5a941a683ec452648ea3979e2 549 main/binary-i386/Packages.gz
 2315d97fb3427df92aab451402cf4447 137 main/binary-i386/Release
 256c3e98acba0c616dd891693c0a2b66 879 main/binary-amd64/Packages
 f8b75bf5a941a683ec452648ea3979e2 549 main/binary-amd64/Packages.gz
 629608b5d1a06eee73fb60350416ff06 138 main/binary-amd64/Release
 256c3e98acba0c616dd891693c0a2b66 879 main/binary-armhf/Packages
 f8b75bf5a941a683ec452648ea3979e2 549 main/binary-armhf/Packages.gz
 17d3c28998676ffac5faafe2d35a154c 138 main/binary-armhf/Release
SHA1:
 41318a1dc66806fd94e120ba13f2377aad61250d 879 main/binary-i386/Packages
 e5531bf8f238ea537c066684277c63d141231146 549 main/binary-i386/Packages.gz
 106feb0ff8d5eae3190448578a9e54e9521a25ee 137 main/binary-i386/Release
 41318a1dc66806fd94e120ba13f2377aad61250d 879 main/binary-amd64/Packages
 e5531bf8f238ea537c066684277c63d141231146 549 main/binary-amd64/Packages.gz
 3a04e6001b57ac979bcfe6c6e9fbc259e6e464b6 138 main/binary-amd64/Release
 41318a1dc66806fd94e120ba13f2377aad61250d 879 main/binary-armhf/Packages
 e5531bf8f238ea537c066684277c63d141231146 549 main/binary-armhf/Packages.gz
 e6462e3c5f8ad234fcfe0be730648bfe42aabfcb 138 main/binary-armhf/Release
SHA256:
 16beedc464d57015ec1092af221b2db5f6463202431a2383278439b9bce1931a 879 main/binary-i386/Packages
 dae70358e69382aa8404d4c50c29ff5782fc18823cef742bc6aa19600bfb7a16 549 main/binary-i386/Packages.gz
 92c00440f0850a7fae005ba5a0bfc31c1082a379f86cbb7872d94d0eb0b511b4 137 main/binary-i386/Release
 16beedc464d57015ec1092af221b2db5f6463202431a2383278439b9bce1931a 879 main/binary-amd64/Packages
 dae70358e69382aa8404d4c50c29ff5782fc18823cef742bc6aa19600bfb7a16 549 main/binary-amd64/Packages.gz
 056825af61ea9f099574662d4ea1b4eab257cb2c65a8b32faa053ff8bab49af8 138 main/binary-amd64/Release
 16beedc464d57015ec1092af221b2db5f6463202431a2383278439b9bce1931a 879 main/binary-armhf/Packages
 dae70358e69382aa8404d4c50c29ff5782fc18823cef742bc6aa19600bfb7a16 549 main/binary-armhf/Packages.gz
 291c95cec899033ebf27001f61e657482ea522db7e39cf699a03e2a24cc4f11b 138 main/binary-armhf/Release
-----BEGIN PGP SIGNATURE-----

iQIzBAEBCAAdFiEE0S+NLEe0oWkXyaBAvtZ+ZDJaBD4FAmFoU9gACgkQvtZ+ZDJa
BD4q2xAAxUcZeIH/zSywJq5e5dEz21WdAm/bCj6x4NI8kWGmhHKpYe/jwkAMZIus
e+WgLp0M69g6cAFWiJoOCGexdE1AQsoUWBsqNM55ZGzn6EUp7weeO93cls2gEoID
Ag6liDTNMdmh4yk/ZMXC64yp4jA9obuX8hZtdZgd0VOynGzMKqjwnWgsp3B7oZ+i
O2TTDXmgOVXhjZdEwBKt5LSMBa3+y82S4Z252av5EIvzro7eCD1iiH4kbdy2bKNp
og7EAHUux5Be9uWFC3Itb10Tre5+ffqK1GMwXE0yNRMQ0EFP/67UIbyoz6JACzP9
ZkWCs33Gp4IwRha7nu8H32F6jneRvb7pJygK9OTLIrn0QgPOLD1bA4r+56mwP90C
FimjCU9pMnJOFnKPRZ6UoqGcuMmlE020B9UXlEZoIAOE9AQ5GenKS7Xvk3GyDJ6S
fSuSYT9w6gfAvSxcuxdaBbcd4QMTAkayV35Vtl5p8kEObLC1666TgqgZ0JKqLyZ0
JKo3ZvnTQou3I2WWEXT3FKk/+5EO5At79Ho6OikgU5U2mKktWKWgqVPf3zHkK09Z
7wpth79YmMAgVCEEnsX2o6xH6Wi6KRpguiwGnuL1Kfu+PR2OVdAkqjHV/MHvWt2n
mn+IkxxDscEqObX+9FleO/5jrrBczA3AgsOPHKtogJUDmZW1lKY=
=uljt
-----END PGP SIGNATURE-----
-----BEGIN PGP SIGNATURE-----

iQIzBAABCAAdFiEE0S+NLEe0oWkXyaBAvtZ+ZDJaBD4FAmFoU9gACgkQvtZ+ZDJa
BD4W+xAAjB4Pom2FUE/tmIBggjMa5LURt9/ltbsRSnJrhgtdmkBjsSL9v/4U46fu
FEoA6p2ik9Z/q8iMSCFEkNfuv9nmlvXKCciKaPOWYpYHHCH8GLomn4LGBCQGW12Y
UqDA3A19bEQs0pk+2Ddj6NCbpyCT0hbUl1CgA0qcH9jdSgM329F9VfeQuYjQYxIH
zY0GxGqV9BM2NTsdhXC+tyeITMgzxQbeHnj3Q6Z7KzjZjIdcq0knlDVaSgJ4KSXG
GI7/e9d9iHvzTj6cxBKzEAt+6CxUesVC8wtAqj9Yyq01/1wqPpOvCL05qa5SSA0q
S5eLtD2AeYm0Mmp8qJ35m8l8xPGA74iXHEANz5qzLycR/hVlZwBwJ8d06LPLuCkT
ozh974G6LnCnFt9UzOruasP7DmR8x77YB1qpGAonKwBhKLFRxY37qUVDhGbPlA8G
+4rHUWCLOD+GN3YEWF5CvMGtHMXdp2TKMTXxR/oGlYxrKaE676mSNF6e5vsCdARN
ewoV1pZHWeru9uV8QJ5ipo+E4HC7BAKToZDk7FCD6CHxRMz/QThZqB6VUuHIEQDH
4DY/xTtmotA2yjGJkPiKzdZtGNLbXuuwSHYNBu20eEo1L9+8qVv/IUBlej8YM+6G
Yas8d1G+gVnonrWhDwbzr3BxcWYvEgWzIq2P29BzQj4J2p6UfXY=
=teXv
-----END PGP SIGNATURE-----
-----BEGIN PGP SIGNED MESSAGE-----
Hash: SHA256

Origin: Linode.com
Label: Linode Longview Repo
Suite: stable
Codename: quantal
Version: 12.10
Date: Sun, 18 Jun 2023 03:03:43 UTC
Architectures: i386 amd64
Components: main
Description: Longview Agent For Ubuntu
MD5Sum:
 d9f54b89ce794376ae78d02c243336d4 1572 main/binary-i386/Packages
 189f30d0a185f5ecab0b86655a81869d 780 main/binary-i386/Packages.gz
 f6ab42eefafc21f494974e08449ebd90 152 main/binary-i386/Release
 d9f54b89ce794376ae78d02c243336d4 1572 main/binary-amd64/Packages
 189f30d0a185f5ecab0b86655a81869d 780 main/binary-amd64/Packages.gz
 199c7ab48405d8e2677e9bca4ef1c352 153 main/binary-amd64/Release
SHA1:
 8f3c5e2f9aa4fa0b61e28a269b3dbf05361d145d 1572 main/binary-i386/Packages
 e29a64b5275aced9c7b0e070ec5fd0c71b644eb8 780 main/binary-i386/Packages.gz
 ef749882dcde109717a405fb4ae86323e3e9cbf3 152 main/binary-i386/Release
 8f3c5e2f9aa4fa0b61e28a269b3dbf05361d145d 1572 main/binary-amd64/Packages
 e29a64b5275aced9c7b0e070ec5fd0c71b644eb8 780 main/binary-amd64/Packages.gz
 112e576979a27bef3bd55250255bbf030b1b8225 153 main/binary-amd64/Release
SHA256:
 3927d80a5b2caf7a5dab102b1b0d845387c4b5dd81577607d1ce9fa2b8ea22b3 1572 main/binary-i386/Packages
 0ed5843b8fa61acde17f0eac3bba08fc1b6abc8eb52be5b13c42db558d8e0e43 780 main/binary-i386/Packages.gz
 5a63c2157dace291ff363770afbf81c06627e70f17b75741ab3916c587fccb1d 152 main/binary-i386/Release
 3927d80a5b2caf7a5dab102b1b0d845387c4b5dd81577607d1ce9fa2b8ea22b3 1572 main/binary-amd64/Packages
 0ed5843b8fa61acde17f0eac3bba08fc1b6abc8eb52be5b13c42db558d8e0e43 780 main/binary-amd64/Packages.gz
 b76b6b737b39b582a42bc1389f2b166eba69c29d818ccf3ff6dc9c9ad86ac400 153 main/binary-amd64/Release
-----BEGIN PGP SIGNATURE-----

iQIzBAEBCAAdFiEE0S+NLEe0oWkXyaBAvtZ+ZDJaBD4FAmSOdA8ACgkQvtZ+ZDJa
BD5Xeg/9HDHPmMHVT1pHL5/Y9MXodprfxP6r8XbojwASzaKgQdMpTtf80dZf1ftT
hAXMSUyGmt32HLk8qC3Rh0jBoALgRrInedYaN9CFEKpXQwtyyHijFmrduXbbElb0
Y0LS49MD59kXU/3rPJYJbI0FhPbs5DlH/djRWVkdsiiAmow4w2SbljAqAXvxNiMc
SNC1BxgJ08Smg39mzzqsh08otHvjJmS1FnGWcYZVAoxETA/LcKrEmo6dVCOL0pPR
9wVh2uFWq+/ClrGhACQThjRcst8u6KfFdo4XWpzABYIRaCBPgfYpw7QlSAeEsH0u
RINVnTmMerhtVkL7IhuSq/yA9bcsHB5uOTpY1ahdjSsvgng56BR34YpaVyjsD2Vu
4z+VSRakYtUbFbnVTRVsiBmMMEemi0E8CMvqdwBcbX8RdSp0U+8/Tz+jNgjxEJSO
UpQ/taozmWGWFYjcibinMuXBlO211g9NyW7sb37YlogNRO0gCFwIYZLZIrwiwrFV
PAW50I2YyYwBi2TAZpbR+G2JBnpwd2SwERyCuhyhjGFjVagd2Mdvd74vivPoEZq8
uv6oUVGI2avp8gsPmLWwZwlEXHuNG+jExrReEEkCXya1vV/oC/p7jS6jWwsH2H8l
cKKoMc5vJoHtq9qTlf9Gj0Ux7BPUCnDHR2rDvPwTFJvqMP42YV4=
=g4ee
-----END PGP SIGNATURE-----
-----BEGIN PGP SIGNED MESSAGE-----
Hash: SHA256

Origin: Linode.com
Label: Linode Longview Repo
Suite: stable
Codename: trusty
Version: 14.04
Date: Sun, 18 Jun 2023 03:03:45 UTC
Architectures: i386 amd64
Components: main
Description: Longview Agent For Ubuntu
MD5Sum:
 d9f54b89ce794376ae78d02c243336d4 1572 main/binary-i386/Packages
 189f30d0a185f5ecab0b86655a81869d 780 main/binary-i386/Packages.gz
 a4fd95fe4d6d516371819d7bf29e37e3 152 main/binary-i386/Release
 d9f54b89ce794376ae78d02c243336d4 1572 main/binary-amd64/Packages
 189f30d0a185f5ecab0b86655a81869d 780 main/binary-amd64/Packages.gz
 2915248b66c9d253fb123784e36532b7 153 main/binary-amd64/Release
SHA1:
 8f3c5e2f9aa4fa0b61e28a269b3dbf05361d145d 1572 main/binary-i386/Packages
 e29a64b5275aced9c7b0e070ec5fd0c71b644eb8 780 main/binary-i386/Packages.gz
 479e9a04de349674d5a21f6d64dee1bd234fc0ce 152 main/binary-i386/Release
 8f3c5e2f9aa4fa0b61e28a269b3dbf05361d145d 1572 main/binary-amd64/Packages
 e29a64b5275aced9c7b0e070ec5fd0c71b644eb8 780 main/binary-amd64/Packages.gz
 c52cc1f9e29dda8362146989f34849f8672e5e05 153 main/binary-amd64/Release
SHA256:
 3927d80a5b2caf7a5dab102b1b0d845387c4b5dd81577607d1ce9fa2b8ea22b3 1572 main/binary-i386/Packages
 0ed5843b8fa61acde17f0eac3bba08fc1b6abc8eb52be5b13c42db558d8e0e43 780 main/binary-i386/Packages.gz
 5a9bf70b16f879b5405b3711d086ccc73b365a91cfbae41773c19ec661a8d789 152 main/binary-i386/Release
 3927d80a5b2caf7a5dab102b1b0d845387c4b5dd81577607d1ce9fa2b8ea22b3 1572 main/binary-amd64/Packages
 0ed5843b8fa61acde17f0eac3bba08fc1b6abc8eb52be5b13c42db558d8e0e43 780 main/binary-amd64/Packages.gz
 cf188d539f7c280acd2ccf53b889373a4b61aabcdb4ea82c945379031e74c0a9 153 main/binary-amd64/Release
-----BEGIN PGP SIGNATURE-----

iQIzBAEBCAAdFiEE0S+NLEe0oWkXyaBAvtZ+ZDJaBD4FAmSOdBEACgkQvtZ+ZDJa
BD50FA/+KcY2caLitOsGB4cAYmX2wlK1jrF05+21pQ9O4+yW7a6ycrOFJ/LNIpD1
wfFkkMf9EKHHdszwMhc3/mVhLEGn5qJFV6CKdMEemln8O5PvGG5GbuKp83Cdw+80
2icWMR2oRUs3XLuOLBtplLAig5lUmhgM+TaEWWxWG65i1jeemnVSR8hEo03G49JP
hRJzelvnCWbbb5miVjsAVIO65d89gn4xiw+xcwSUcm0gsRQv/ysHm8S28CA3xtjf
fZBxrscjGhJQeFJuPhgbO8sapQW1U/JIpNHgb3+hLbU0940epXBBYTtXR/2K/aHy
ZtaOwQTWmAD1DbMaj1OA0777WZKDe0YxhMXplIHT95JtPazAMPzNHNXkpuEMNbeY
gXjFkAbSpYAyowoySYVP0YvXik9NMLSy5/EehT1MX0TYYqYts0yf3PUzJagFBhxV
bNauY6NOblCwvhg9rC3XTkzWXmdNweKqxuft2wqKh9Ba8TMOX4yF94EgFeLkUG/P
+ttKb9aKZK5glTruhh7cz+Ll7yrNT3MvSHetemmyNu1tXNmAbuo7bguBEIiC3qkm
boF4B7XairKxorFjIYjcChS7nYHe3+2rTI8AEVTmHYNe0TuVb5UK+GAPZCCryyWM
0gwbdHQeaizEzyDB987eVF1G+xyjhrGls9fOBtWpup7iXaqSiu0=
=lwv+
-----END PGP SIGNATURE-----


{
  "data": {
    "cpu": [
      {
        "true": 29.94,
        "x": 11513761600000
      }
    ],
    "disk": [
      {
        "true": 29.94,
        "x": 11513761600000
      }
    ],
    "net_in": [
      {
        "true": 29.94,
        "x": 11513761600000
      }
    ],
    "net_out": [
      {
        "true": 29.94,
        "x": 11513761600000
      }
    ],
    "swap": [
      {
        "true": 29.94,
        "x": 11513761600000
      }
    ]
  }
}
curl -H "Content-Type: application/json" \
    -H "Authorization: 6692099bd12f686556b7f4e2ae18d783cc500b6432e5a6c5944fb4405c41cd72" \
    -X POST \
    https://api.linode.com/v4/managed/services/9994/enable
curl -H "Content-Type: application/json" \
    -H "Authorization: 6692099bd12f686556b7f4e2ae18d783cc500b6432e5a6c5944fb4405c41cd72" \
    -X POST -d '{
      "label": "my-object-storage-key",
      "bucket_access": [
        {
          "cluster": "ap-south-1",
          "bucket_name": "bucket-example-1",
          "permissions": "read_write"
        },
        {
          "cluster": "us-east-1",
          "bucket_name": "bucket-example-2",
          "permissions": "read_only"
        }
      ]
    }' \
  https://api.linode.com/v4/object-storage/keys
{
  "access_key": "KVAKUTGBA4WTR2NSJQ81",
  "bucket_access": [
    {
      "bucket_name": "example-bucket",
      "cluster": "ap-south-1",
      "permissions": "read_only"
    }
  ],
  "id": 123,
  "label": "my-key",
  "limited": true,
  "secret_key": "OiA6F5r0niLs3QA2stbyq7mY5VCV7KqOzcmitmHw"
}    
POST https://api.linode.com/v4/object-storage/keys
About security log events

The name for each audit log entry is composed of a category of events, followed by an operation type. For example, the repo.create entry refers to the create operation on the repo category. The reference information in this article is grouped by categories.
account

Action	Description
account.plan_change	The account's plan changed.
actions_cache

Action	Description
actions_cache.delete	A GitHub Actions cache was deleted using the REST API.
artifact

Action	Description
artifact.destroy	A workflow run artifact was manually deleted.
billing

Action	Description
billing.change_billing_type	The way the account pays for GitHub was changed.
billing.change_email	The billing email address changed.
business

Action	Description
business.set_actions_fork_pr_approvals_policy	The policy for requiring approvals for workflows from public forks was changed for an enterprise.
business.set_actions_private_fork_pr_approvals_policy	The policy for requiring approval for fork pull request workflows from collaborators without write access to private repos was changed for an enterprise.
business.set_actions_retention_limit	The retention period for GitHub Actions artifacts and logs was changed for an enterprise.
business.set_default_workflow_permissions	The default permissions granted to the GITHUB_TOKEN when running workflows were changed for an enterprise.
business.set_fork_pr_workflows_policy	The policy for fork pull request workflows was changed for an enterprise.
business.set_workflow_permission_can_approve_pr	The policy for allowing GitHub Actions to create and approve pull requests was changed for an enterprise.
checks

Action	Description
checks.auto_trigger_disabled	Automatic creation of check suites was disabled on a repository in the organization or enterprise.
checks.auto_trigger_enabled	Automatic creation of check suites was enabled on a repository in the organization or enterprise.
checks.delete_logs	Logs in a check suite were deleted.
codespaces

Action	Description
codespaces.allow_permissions	A codespace using custom permissions from its devcontainer.json file was launched.
codespaces.connect	Credentials for a codespace were refreshed.
codespaces.create	A codespace was created
codespaces.destroy	A user deleted a codespace.
codespaces.export_environment	A codespace was exported to a branch on GitHub.
codespaces.restore	A codespace was restored.
codespaces.start_environment	A codespace was started.
codespaces.suspend_environment	A codespace was stopped.
codespaces.trusted_repositories_access_update	A personal account's access and security setting for Codespaces were updated.
copilot

Action	Description
copilot.cfb_seat_added	A seat was added to the Copilot Business subscription for a user and they have received access to GitHub Copilot.
copilot.cfb_seat_assignment_created	A seat assignment was newly created for a user.
copilot.cfb_seat_assignment_refreshed	A seat assignment that was previously pending cancellation was re-assigned and the user will retain access to GitHub Copilot.
copilot.cfb_seat_assignment_reused	A seat assignment was re-created for a user who already had a seat with no pending cancellation date.
copilot.cfb_seat_assignment_unassigned	A seat was unassigned from a user and they will lose access to GitHub Copilot at the end of the billing cycle.
copilot.cfb_seat_cancelled	A seat was canceled from the Copilot Business subscription and the user no longer has access to GitHub Copilot.
copilot.cfb_seat_cancelled_by_staff	A seat was canceled from the Copilot Business subscription manually by GitHub and the user no longer has access to GitHub Copilot.
dependabot_alerts

Action	Description
dependabot_alerts.disable	Dependabot alerts were disabled for all existing repositories.
dependabot_alerts.enable	Dependabot alerts were enabled for all existing repositories.
dependabot_alerts_new_repos

Action	Description
dependabot_alerts_new_repos.disable	Dependabot alerts were disabled for all new repositories.
dependabot_alerts_new_repos.enable	Dependabot alerts were enabled for all new repositories.
dependabot_repository_access

Action	Description
dependabot_repository_access.repositories_updated	The repositories that Dependabot can access were updated.
dependabot_security_updates

Action	Description
dependabot_security_updates.disable	Dependabot security updates were disabled for all existing repositories.
dependabot_security_updates.enable	Dependabot security updates were enabled for all existing repositories.
dependabot_security_updates_new_repos

Action	Description
dependabot_security_updates_new_repos.disable	Dependabot security updates were disabled for all new repositories.
dependabot_security_updates_new_repos.enable	Dependabot security updates were enabled for all new repositories.
dependency_graph

Action	Description
dependency_graph.disable	The dependency graph was disabled for all existing repositories.
dependency_graph.enable	The dependency graph was enabled for all existing repositories.
dependency_graph_new_repos

Action	Description
dependency_graph_new_repos.disable	The dependency graph was disabled for all new repositories.
dependency_graph_new_repos.enable	The dependency graph was enabled for all new repositories.
environment

Action	Description
environment.add_protection_rule	A GitHub Actions deployment protection rule was created via the API.
environment.create_actions_secret	A secret was created for a GitHub Actions environment.
environment.delete	An environment was deleted.
environment.remove_actions_secret	A secret was deleted for a GitHub Actions environment.
environment.remove_protection_rule	A GitHub Actions deployment protection rule was deleted via the API.
environment.update_actions_secret	A secret was updated for a GitHub Actions environment.
environment.update_protection_rule	A GitHub Actions deployment protection rule was updated via the API.
git_signing_ssh_public_key

Action	Description
git_signing_ssh_public_key.create	An SSH key was added to a user account as a Git commit signing key.
git_signing_ssh_public_key.delete	An SSH key was removed from a user account as a Git commit signing key.
hook

Action	Description
hook.active_changed	A hook's active status was updated.
hook.config_changed	A hook's configuration was changed.
hook.create	A new hook was added.
hook.destroy	A hook was deleted.
hook.events_changed	A hook's configured events were changed.
integration

Action	Description
integration.create	A GitHub App was created.
integration.destroy	A GitHub App was deleted.
integration.manager_added	A member of an enterprise or organization was added as a GitHub App manager.
integration.manager_removed	A member of an enterprise or organization was removed from being a GitHub App manager.
integration.remove_client_secret	A client secret for a GitHub App was removed.
integration.revoke_all_tokens	All user tokens for a GitHub App were requested to be revoked.
integration.revoke_tokens	Token(s) for a GitHub App were revoked.
integration.suspend	A GitHub App was suspended.
integration.transfer	Ownership of a GitHub App was transferred to another user or organization.
integration.unsuspend	A GitHub App was unsuspended.
integration_installation

Action	Description
integration_installation.create	A GitHub App was installed.
integration_installation.destroy	A GitHub App was uninstalled.
integration_installation.repositories_added	Repositories were added to a GitHub App.
integration_installation.repositories_removed	Repositories were removed from a GitHub App.
integration_installation.suspend	A GitHub App was suspended.
integration_installation.unsuspend	A GitHub App was unsuspended.
integration_installation.version_updated	Permissions for a GitHub App were updated.
marketplace_agreement_signature

Action	Description
marketplace_agreement_signature.create	The GitHub Marketplace Developer Agreement was signed.
marketplace_listing

Action	Description
marketplace_listing.approve	A listing was approved for inclusion in GitHub Marketplace.
marketplace_listing.change_category	A category for a listing for an app in GitHub Marketplace was changed.
marketplace_listing.create	A listing for an app in GitHub Marketplace was created.
marketplace_listing.delist	A listing was removed from GitHub Marketplace.
marketplace_listing.redraft	A listing was sent back to draft state.
marketplace_listing.reject	A listing was not accepted for inclusion in GitHub Marketplace.
migration

Action	Description
migration.create	A migration file was created for transferring data from a source location (such as a GitHub.com organization or a GitHub Enterprise Server instance) to a target GitHub Enterprise Server instance.
oauth_access

Action	Description
oauth_access.create	An OAuth access token was generated.
oauth_access.destroy	An OAuth access token was deleted.
oauth_access.regenerate	An OAuth access token was regenerated.
oauth_access.update	An OAuth access token was updated.
oauth_application

Action	Description
oauth_application.create	An OAuth application was created.
oauth_application.destroy	An OAuth application was deleted.
oauth_application.generate_client_secret	An OAuth application's secret key was generated.
oauth_application.remove_client_secret	An OAuth application's secret key was deleted.
oauth_application.reset_secret	The secret key for an OAuth application was reset.
oauth_application.revoke_all_tokens	All user tokens for an OAuth application were requested to be revoked.
oauth_application.revoke_tokens	Token(s) for an OAuth application were revoked.
oauth_application.transfer	An OAuth application was transferred from one account to another.
oauth_authorization

Action	Description
oauth_authorization.create	An authorization for an OAuth application was created.
oauth_authorization.destroy	An authorization for an OAuth application was deleted.
org

Action	Description
org.add_member	A user joined an organization.
org.add_outside_collaborator	An outside collaborator was added to a repository.
org.advanced_security_disabled_for_new_repos	GitHub Advanced Security was disabled for new repositories in an organization.
org.advanced_security_disabled_on_all_repos	GitHub Advanced Security was disabled for all repositories in an organization.
org.advanced_security_enabled_for_new_repos	GitHub Advanced Security was enabled for new repositories in an organization.
org.advanced_security_enabled_on_all_repos	GitHub Advanced Security was enabled for all repositories in an organization.
org.remove_member	A member was removed from an organization, either manually or due to a two-factor authentication requirement.
org.set_actions_fork_pr_approvals_policy	The setting for requiring approvals for workflows from public forks was changed for an organization.
org.set_actions_private_fork_pr_approvals_policy	The policy for requiring approval for fork pull request workflows from collaborators without write access to private repos was changed for an organization.
org.set_actions_retention_limit	The retention period for GitHub Actions artifacts and logs in an organization was changed.
org.set_default_workflow_permissions	The default permissions granted to the GITHUB_TOKEN when running workflows were changed for an organization.
org.set_fork_pr_workflows_policy	The policy for workflows on private repository forks was changed.
org.set_workflow_permission_can_approve_pr	The policy for allowing GitHub Actions to create and approve pull requests was changed for an organization.
org.update_member	A person's role was changed from owner to member or member to owner.
org.update_member_repository_creation_permission	The create repository permission for organization members was changed.
org.update_member_repository_invitation_permission	An organization owner changed the policy setting for organization members inviting outside collaborators to repositories.
pages_protected_domain

Action	Description
pages_protected_domain.create	A GitHub Pages verified domain was created for an organization or enterprise.
pages_protected_domain.delete	A GitHub Pages verified domain was deleted from an organization or enterprise.
pages_protected_domain.verify	A GitHub Pages domain was verified for an organization or enterprise.
passkey

Action	Description
passkey.register	A new passkey was added.
passkey.remove	A new passkey was removed.
payment_method

Action	Description
payment_method.create	A new payment method was added, such as a new credit card or PayPal account.
payment_method.remove	A payment method was removed.
payment_method.update	An existing payment method was updated.
personal_access_token

Action	Description
personal_access_token.access_granted	A fine-grained personal access token was granted access to resources.
personal_access_token.access_revoked	A fine-grained personal access token was revoked. The token can still read public organization resources.
personal_access_token.create	Triggered when you create a fine-grained personal access token.
personal_access_token.credential_regenerated	Triggered when you regenerate a fine-grained personal access token.
personal_access_token.credential_revoked	A fine-grained personal access token was revoked by GitHub Advanced Security.
personal_access_token.destroy	Triggered when you delete a fine-grained personal access token.
personal_access_token.request_cancelled	A pending request for a fine-grained personal access token to access organization resources was canceled.
personal_access_token.request_created	Triggered when a fine-grained personal access token was created to access organization resources and the organization requires approval before the token can access organization resources.
personal_access_token.request_denied	A request for a fine-grained personal access token to access organization resources was denied.
personal_access_token.update	A fine-grained personal access token was updated.
profile_picture

Action	Description
profile_picture.update	A profile picture was updated.
project

Action	Description
project.access	A project board visibility was changed.
project.close	A project board was closed.
project.create	A project board was created.
project.delete	A project board was deleted.
project.link	A repository was linked to a project board.
project.open	A project board was reopened.
project.rename	A project board was renamed.
project.unlink	A repository was unlinked from a project board.
project.update_org_permission	The project's base-level permission for all organization members was changed or removed.
project.update_team_permission	A team's project board permission level was changed or when a team was added or removed from a project board.
project.update_user_permission	A user was added to or removed from a project board or had their permission level changed.
project_field

Action	Description
project_field.create	A field was created in a project board.
project_field.delete	A field was deleted in a project board.
project_view

Action	Description
project_view.create	A view was created in a project board.
project_view.delete	A view was deleted in a project board.
protected_branch

Action	Description
protected_branch.update_merge_queue_enforcement_level	Enforcement of the merge queue was modified for a branch.
public_key

Action	Description
public_key.create	An SSH key was added to a user account or a deploy key was added to a repository.
public_key.delete	An SSH key was removed from a user account or a deploy key was removed from a repository.
public_key.unverification_failure	A user account's SSH key or a repository's deploy key was unable to be unverified.
public_key.unverify	A user account's SSH key or a repository's deploy key was unverified.
public_key.update	A user account's SSH key or a repository's deploy key was updated.
public_key.verification_failure	A user account's SSH key or a repository's deploy key was unable to be verified.
public_key.verify	A user account's SSH key or a repository's deploy key was verified.
repo

Action	Description
repo.access	The visibility of a repository changed.
repo.actions_enabled	GitHub Actions was enabled for a repository.
repo.add_member	A collaborator was added to a repository.
repo.add_topic	A topic was added to a repository.
repo.advanced_security_disabled	GitHub Advanced Security was disabled for a repository.
repo.advanced_security_enabled	GitHub Advanced Security was enabled for a repository.
repo.archived	A repository was archived.
repo.change_merge_setting	Pull request merge options were changed for a repository.
repo.code_scanning_analysis_deleted	Code scanning analysis for a repository was deleted.
repo.code_scanning_configuration_for_branch_deleted	A code scanning configuration for a branch of a repository was deleted.
repo.config.disable_collaborators_only	The interaction limit for collaborators only was disabled.
repo.config.disable_contributors_only	The interaction limit for prior contributors only was disabled in a repository.
repo.config.disable_sockpuppet_disallowed	The interaction limit for existing users only was disabled in a repository.
repo.config.enable_collaborators_only	The interaction limit for collaborators only was enabled in a repository Users that are not collaborators or organization members were unable to interact with a repository for a set duration.
repo.config.enable_contributors_only	The interaction limit for prior contributors only was enabled in a repository Users that are not prior contributors, collaborators or organization members were unable to interact with a repository for a set duration.
repo.config.enable_sockpuppet_disallowed	The interaction limit for existing users was enabled in a repository New users aren't able to interact with a repository for a set duration Existing users of the repository, contributors, collaborators or organization members are able to interact with a repository.
repo.create	A repository was created.
repo.create_actions_secret	A GitHub Actions secret was created for a repository.
repo.create_integration_secret	An integration secret was created for a repository.
repo.destroy	A repository was deleted.
repo.pages_cname	A GitHub Pages custom domain was modified in a repository.
repo.pages_create	A GitHub Pages site was created.
repo.pages_destroy	A GitHub Pages site was deleted.
repo.pages_https_redirect_disabled	HTTPS redirects were disabled for a GitHub Pages site.
repo.pages_https_redirect_enabled	HTTPS redirects were enabled for a GitHub Pages site.
repo.pages_private	A GitHub Pages site visibility was changed to private.
repo.pages_public	A GitHub Pages site visibility was changed to public.
repo.pages_soft_delete	A GitHub Pages site was soft-deleted because its owner's plan changed.
repo.pages_soft_delete_restore	A GitHub Pages site that was previously soft-deleted was restored.
repo.pages_source	A GitHub Pages source was modified.
repo.register_self_hosted_runner	A new self-hosted runner was registered.
repo.remove_actions_secret	A GitHub Actions secret was deleted for a repository.
repo.remove_integration_secret	An integration secret was deleted for a repository.
repo.remove_member	A collaborator was removed from a repository.
repo.remove_self_hosted_runner	A self-hosted runner was removed.
repo.remove_topic	A topic was removed from a repository.
repo.rename	A repository was renamed.
repo.set_actions_fork_pr_approvals_policy	The setting for requiring approvals for workflows from public forks was changed for a repository.
repo.set_actions_private_fork_pr_approvals_policy	The policy for requiring approval for fork pull request workflows from collaborators without write access to private repos was changed for a repository.
repo.set_actions_retention_limit	The retention period for GitHub Actions artifacts and logs in a repository was changed.
repo.set_default_workflow_permissions	The default permissions granted to the GITHUB_TOKEN when running workflows were changed for a repository.
repo.set_fork_pr_workflows_policy	Triggered when the policy for workflows on private repository forks is changed.
repo.set_workflow_permission_can_approve_pr	The policy for allowing GitHub Actions to create and approve pull requests was changed for a repository.
repo.staff_unlock	An enterprise owner or GitHub staff (with permission from a repository administrator) temporarily unlocked the repository.
repo.temporary_access_granted	Temporary access was enabled for a repository.
repo.transfer	A user accepted a request to receive a transferred repository.
repo.transfer_outgoing	A repository was transferred to another repository network.
repo.transfer_start	A user sent a request to transfer a repository to another user or organization.
repo.unarchived	A repository was unarchived.
repo.update_actions_access_settings	The setting to control how a repository was used by GitHub Actions workflows in other repositories was changed.
repo.update_actions_secret	A GitHub Actions secret was updated.
repo.update_actions_settings	A repository administrator changed GitHub Actions policy settings for a repository.
repo.update_default_branch	The default branch for a repository was changed.
repo.update_integration_secret	An integration secret was updated for a repository.
repo.update_member	A user's permission to a repository was changed.
repository_image

Action	Description
repository_image.create	An image to represent a repository was uploaded.
repository_image.destroy	An image to represent a repository was deleted.
repository_invitation

Action	Description
repository_invitation.accept	An invitation to join a repository was accepted.
repository_invitation.cancel	An invitation to join a repository was canceled.
repository_invitation.create	An invitation to join a repository was sent.
repository_invitation.reject	An invitation to join a repository was declined.
repository_ruleset

Action	Description
repository_ruleset.create	A repository ruleset was created.
repository_ruleset.destroy	A repository ruleset was deleted.
repository_ruleset.update	A repository ruleset was edited.
security_key

Action	Description
security_key.register	A security key was registered for an account.
security_key.remove	A security key was removed from an account.
sponsors

Action	Description
sponsors.agreement_sign	A GitHub Sponsors agreement was signed on behalf of an organization.
sponsors.custom_amount_settings_change	Custom amounts for GitHub Sponsors were enabled or disabled, or the suggested custom amount was changed.
sponsors.fiscal_host_change	The fiscal host for a GitHub Sponsors listing was updated.
sponsors.repo_funding_links_file_action	The FUNDING file in a repository was changed.
sponsors.sponsor_sponsorship_cancel	A sponsorship was canceled.
sponsors.sponsor_sponsorship_create	A sponsorship was created, by sponsoring an account.
sponsors.sponsor_sponsorship_payment_complete	After you sponsor an account and a payment has been processed, the sponsorship payment was marked as complete.
sponsors.sponsor_sponsorship_preference_change	The option to receive email updates from a sponsored account was changed.
sponsors.sponsor_sponsorship_tier_change	A sponsorship was upgraded or downgraded.
sponsors.sponsored_developer_approve	A GitHub Sponsors account was approved.
sponsors.sponsored_developer_create	A GitHub Sponsors account was created.
sponsors.sponsored_developer_disable	A GitHub Sponsors account was disabled.
sponsors.sponsored_developer_profile_update	The profile for GitHub Sponsors account was edited.
sponsors.sponsored_developer_redraft	A GitHub Sponsors account was returned to draft state from approved state.
sponsors.sponsored_developer_request_approval	An application for GitHub Sponsors was submitted for approval.
sponsors.sponsored_developer_tier_description_update	The description for a sponsorship tier was changed.
sponsors.sponsored_developer_update_newsletter_send	Triggered when you send an email update to your sponsors.
sponsors.sponsors_patreon_user_create	A Patreon account was linked to a user account for use with GitHub Sponsors.
sponsors.sponsors_patreon_user_destroy	A Patreon account for use with GitHub Sponsors was unlinked from a user account.
sponsors.update_tier_repository	A GitHub Sponsors tier changed access for a repository.
sponsors.update_tier_welcome_message	The welcome message for a GitHub Sponsors tier for an organization was updated.
sponsors.waitlist_join	You join the waitlist to join GitHub Sponsors.
sponsors.withdraw_agreement_signature	A signature was withdrawn from a GitHub Sponsors agreement that applies to an organization.
successor_invitation

Action	Description
successor_invitation.accept	Triggered when you accept a succession invitation.
successor_invitation.cancel	Triggered when you cancel a succession invitation.
successor_invitation.create	Triggered when you create a succession invitation.
successor_invitation.decline	Triggered when you decline a succession invitation.
successor_invitation.revoke	Triggered when you revoke a succession invitation.
trusted_device

Action	Description
trusted_device.register	A new trusted device was added.
trusted_device.remove	A trusted device was removed.
two_factor_authentication

Action	Description
two_factor_authentication.add_factor	A secondary authentication factor was added to a user account.
two_factor_authentication.disabled	Two-factor authentication was disabled for a user account.
two_factor_authentication.enabled	Two-factor authentication was enabled for a user account.
two_factor_authentication.password_reset_fallback_sms	A one-time password code was sent to a user account fallback phone number.
two_factor_authentication.recovery_codes_regenerated	Two factor recovery codes were regenerated for a user account.
two_factor_authentication.remove_factor	A secondary authentication factor was removed from a user account.
two_factor_authentication.sign_in_fallback_sms	A one-time password code was sent to a user account fallback phone number.
two_factor_authentication.update_fallback	The two-factor authentication fallback for a user account was changed.
user

Action	Description
user.add_email	An email address was added to a user account.
user.async_delete	An asynchronous job was started to destroy a user account, eventually triggering a user.delete event.
user.audit_log_export	Audit log entries were exported.
user.block_user	A user was blocked by another user.
user.change_password	A user changed their password.
user.codespaces_trusted_repo_access_granted	Triggered when you allow the codespaces you create for a repository to access other repositories owned by your personal account.
user.codespaces_trusted_repo_access_revoked	Triggered when you disallow the codespaces you create for a repository to access other repositories owned by your personal account.
user.create	A new user account was created.
user.create_integration_secret	A user secret for Codespaces was created.
user.creation_rate_limit_exceeded	The rate of creation of user accounts, applications, issues, pull requests or other resources exceeded the configured rate limits, or too many users were followed too quickly.
user.delete	A user account was destroyed by an asynchronous job.
user.demote	A site administrator was demoted to an ordinary user account.
user.destroy	A user deleted his or her account, triggering user.async_delete.
user.failed_login	A user tried to sign in with an incorrect username, password, or two-factor authentication code.
user.forgot_password	A user requested a password reset.
user.hide_private_contributions_count	A user changed the visibility of their private contributions. The number of contributions to private repositories on the user's profile are now hidden.
user.login	A user signed in.
user.logout	A user signed out.
user.new_device_used	A user signed in from a new device.
user.promote	An ordinary user account was promoted to a site administrator.
user.recreate	A user's account was restored.
user.remove_email	An email address was removed from a user account.
user.remove_integration_secret	A user secret for Codespaces was deleted.
user.rename	A username was changed.
user.reset_password	A user reset their account password.
user.show_private_contributions_count	A user changed the visibility of their private contributions. The number of contributions to private repositories on the user's profile are now shown.
user.sign_in_from_unrecognized_device	A user signed in from an unrecognized device.
user.sign_in_from_unrecognized_device_and_location	A user signed in from an unrecognized device and location.
user.suspend	A user account was suspended.
user.two_factor_challenge_failure	A 2FA challenge issued for a user account failed.
user.two_factor_challenge_success	A 2FA challenge issued for a user account succeeded.
user.two_factor_recover	A user used their 2FA recovery codes.
user.two_factor_recovery_codes_downloaded	A user downloaded 2FA recovery codes for their account.
user.two_factor_recovery_codes_printed	A user printed 2FA recovery codes for their account.
user.two_factor_recovery_codes_viewed	A user viewed 2FA recovery codes for their account.
user.two_factor_requested	A user was prompted for a two-factor authentication code.
user.unblock_user	A user was unblocked by another user.
user.unsuspend	A user account was unsuspended.
user.update_integration_secret	A user secret for Codespaces was updated.
user_status

Action	Description
user_status.destroy	Triggered when you clear the status on your profile.
user_status.update	Triggered when you set or change the status on your profile.
workflows

Action	Description
workflows.approve_workflow_job	A workflow job was approved.
workflows.delete_workflow_run	A workflow run was deleted.
workflows.disable_workflow	A workflow was disabled.
workflows.enable_workflow	A workflow was enabled, after previously being disabled by disable_workflow.
workflows.reject_workflow_job	A workflow job was rejected.

npm smee --url [WEBHOOK_PROXY_UR](https://scpf-foundation-roblox.fandom.com/wiki/The_Administrator?fbclid=IwAR2FfaoXITYK167Nc-gEZKTMRz_v83X1RrGN52-68b4gcOTDG_Y9pT8S3QY_aem_AcWFgp90kCyN3CxUsNX0uytp_i-7n0Q677zEID8d0e7u0Lh7Ta3Nf6jVo1WXYRibmJA)https://scpf-foundation-roblox.fandom.com/wiki/The_Administrator?fbclid=IwAR2FfaoXITYK167Nc-gEZKTMRz_v83X1RrGN52-68b4gcOTDG_Y9pT8S3QY_aem_AcWFgp90kCyN3CxUsNX0uytp_i-7n0Q677zEID8d0e7u0Lh7Ta3Nf6jVo1WXYRibmJAL --path /webhook --port 3000
Forwarding WEBHOOK_PROXY_URL to http://127.0.0.1:3000/webhook
Connected WEBHOOK_PROXY_URL
gem install bundler
 --global smee-client
bundle init
 bundle install
bundle add sinatra
# These are the dependencies for this code. You installed the `sinatra` gem earlier. For more information, see "[Ruby example: Install dependencies](#ruby-example-install-dependencies)." The `json` library is a standard Ruby library, so you don't need to install it.
require 'sinatra'
require 'json'

# The `/webhook` route matches the path that you specified for the smee.io forwarding. For more information, see "[Forward webhooks](#forward-webhooks)."
#
# Once you deploy your code to a server and update your webhook URL, you should change this to match the path portion of the URL for your webhook.
post '/webhook' do

  # Respond to indicate that the delivery was successfully received.
  # Your server should respond with a 2XX response within 10 seconds of receiving a webhook delivery. If your server takes longer than that to respond, then GitHub terminates the connection and considers the delivery a failure.
  status 202

  # Check the `X-GitHub-Event` header to learn what event type was sent.
  # Sinatra changes `X-GitHub-Event` to `HTTP_X_GITHUB_EVENT`.
  github_event = request.env['[HTTP_X_GITHUB_EVENT](https://scpf-foundation-roblox.fandom.com/wiki/The_Administrator?fbclid=IwAR2FfaoXITYK167Nc-gEZKTMRz_v83X1RrGN52-68b4gcOTDG_Y9pT8S3QY_aem_AcWFgp90kCyN3CxUsNX0uytp_i-7n0Q677zEID8d0e7u0Lh7Ta3Nf6jVo1WXYRibmJAL)']

  # You should add logic to handle each event type that your webhook is subscribed to.
  # For example, this code handles the `issues` and `ping` events.
  #
  # If any events have an `action` field, you should also add logic to handle each action that you are interested in.
  # For example, this code handles the `opened` and `closed` actions for the `issue` event.
  #
  # For more information about the data that you can expect for each event type, see "[AUTOTITLE](/webhooks/webhook-events-and-payloads)."
  if github_event == "issues"
    data = JSON.parse(request.body.read)
    action = data['action']
    if action == "opened"
      puts "An issue was opened with this title: #{data['issue']['title']}"
    elsif action == "closed"
      puts "An issue was closed by #{data['issue']['user']['login']}"
    else
      puts "Unhandled action for the issue event: #{action}"
    end
  elsif github_event == "ping"
    puts "GitHub sent the ping event"
  else
    puts "Unhandled event: #{github_event}"
  end
end

PORT=3000 ruby FILE_NAME
npm install express
// You installed the `express` library earlier. For more information, see "[JavaScript example: Install dependencies](#javascript-example-install-dependencies)."
const express = require('express');

// This initializes a new Express application.
const app = express();

// This defines a POST route at the `/webhook` path. This path matches the path that you specified for the smee.io forwarding. For more information, see "[Forward webhooks](#forward-webhooks)."
//
// Once you deploy your code to a server and update your webhook URL, you should change this to match the path portion of the URL for your webhook.
app.post('/webhook', express.json({type: 'application/json'}), (request, response) => {

  // Respond to indicate that the delivery was successfully received.
  // Your server should respond with a 2XX response within 10 seconds of receiving a webhook delivery. If your server takes longer than that to respond, then GitHub terminates the connection and considers the delivery a failure.
  response.status(202).send('Accepted');

  // Check the `x-github-event` header to learn what event type was sent.
  const githubEvent = request.headers['x-github-event'];

  // You should add logic to handle each event type that your webhook is subscribed to.
  // For example, this code handles the `issues` and `ping` events.
  //
  // If any events have an `action` field, you should also add logic to handle each action that you are interested in.
  // For example, this code handles the `opened` and `closed` actions for the `issue` event.
  //
  // For more information about the data that you can expect for each event type, see "[AUTOTITLE](/webhooks/webhook-events-and-payloads)."
  if (githubEvent === 'issues') {
    const data = request.body;
    const action = data.action;
    if (action === 'opened') {
      console.log(`An issue was opened with this title: ${data.issue.title}`);
    } else if (action === 'closed') {
      console.log(`An issue was closed by ${data.issue.user.login}`);
    } else {
      console.log(`Unhandled action for the issue event: ${action}`);
    }
  } else if (githubEvent === 'ping') {
    console.log('GitHub sent the ping event');
  } else {
    console.log(`Unhandled event: ${githubEvent}`);
  }
});

// This defines the port where your server should listen.
// 3000 matches the port that you specified for webhook forwarding. For more information, see "[Forward webhooks](#forward-webhooks)."
//
// Once you deploy your code to a server, you should change this to match the port where your server is listening.
const port = 3000;

// This starts the server and tells it to listen at the specified port.
app.listen(port, () => {
  console.log(`Server is running on port ${port}`);
});
node THE_ADMINISTRATOR

query {
  viewer {
    repositories(first: 50) {
      edges {
        repository:node {
          name

          issues(first: 10) {
            totalCount
            edges {
              node {
                title
                bodyHTML
              }
            }
          }
        }
      }
    }
  }
}
Calculation:
50         = 50 repositories
 +
50 x 10  = 500 repository issues

            = 550 total nodes
Complex query:
query {
  viewer {
    repositories(first: 50) {
      edges {
        repository:node {
          name

          pullRequests(first: 20) {
            edges {
              pullRequest:node {
                title

                comments(first: 10) {
                  edges {
                    comment:node {
                      bodyHTML
                    }
                  }
                }
              }
            }
          }

          issues(first: 20) {
            totalCount
            edges {
              issue:node {
                title
                bodyHTML

                comments(first: 10) {
                  edges {
                    comment:node {
                      bodyHTML
                    }
                  }
                }
              }
            }
          }
        }
      }
    }

    followers(first: 10) {
      edges {
        follower:node {
          login
        }
      }
    }
  }
}
Calculation:
50              = 50 repositories
 +
50 x 20       = 1,000 pullRequests
 +
50 x 20 x 10 = 10,000 pullRequest comments
 +
50 x 20       = 1,000 issues
 +
50 x 20 x 10 = 10,000 issue comments
 +
10              = 10 followers

                 = 22,060 total nodes
Primary rate limit

The GraphQL API assigns points to each query and limits the points that you can use within a specific amount of time. This limit helps prevent abuse and denial-of-service attacks, and ensures that the API remains available for all users.

The REST API also has a separate primary rate limit. For more information, see "Rate limits for the REST API."

In general, you can calculate your primary rate limit for the GraphQL API based on your method of authentication:

For users: 5,000 points per hour per user. This includes requests made with a personal access token as well as requests made by a GitHub App or OAuth app on behalf of a user that authorized the app. Requests made on a user's behalf by a GitHub App that is owned by a GitHub Enterprise Cloud organization have a higher rate limit of 10,000 points per hour. Similarly, requests made on your behalf by an OAuth app that is owned or approved by a GitHub Enterprise Cloud organization have a higher rate limit of 10,000 points per hour if you are a member of the GitHub Enterprise Cloud organization.
For GitHub App installations not on a GitHub Enterprise Cloud organization: 5,000 points per hour per installation. Installations that have more than 20 repositories receive another 50 points per hour for each repository. Installations that are on an organization that have more than 20 users receive another 50 points per hour for each user. The rate limit cannot increase beyond 12,500 points per hour. The rate limit for user access tokens (as opposed to installation access tokens) are dictated by the primary rate limit for users.
For GitHub App installations on a GitHub Enterprise Cloud organization: 10,000 points per hour per installation. The rate limit for user access tokens (as opposed to installation access tokens) are dictated by the primary rate limit for users.
For OAuth apps: 5,000 points per hour, or 10,000 points per hour if the app is owned by a GitHub Enterprise Cloud organization. This only applies when the app uses their client ID and client secret to request public data. The rate limit for OAuth access tokens generated by a OAuth app are dictated by the primary rate limit for users.
For GITHUB_TOKEN in GitHub Actions workflows: 1,000 points per hour per repository. For requests to resources that belong to an enterprise account on GitHub.com, the limit is 15,000 points per hour per repository.
You can check the point value of a query or calculate the expected point value as described in the following sections. The formula for calculating points and the rate limit are subject to change.

Checking the status of your primary rate limit

You can use the headers that are sent with each response to determine the current status of your primary rate limit.

Header name	Description
x-ratelimit-limit	The maximum number of points that you can use per hour
x-ratelimit-remaining	The number of points remaining in the current rate limit window
x-ratelimit-used	The number of points you have used in the current rate limit window
x-ratelimit-reset	The time at which the current rate limit window resets, in UTC epoch seconds
x-ratelimit-resource	The rate limit resource that the request counted against. For GraphQL requests, this will always be graphql.
You can also query the rateLimit object to check your rate limit. When possible, you should use the rate limit response headers instead of querying the API to check your rate limit.

query {
  viewer {
    login
  }
  rateLimit {
    limit
    remaining
    used
    resetAt
  }
}
Field	Description
limit	The maximum number of points that you can use per hour
remaining	The number of points remaining in the current rate limit window
used	The number of points you have used in the current rate limit window
resetAt	The time at which the current rate limit window resets, in UTC epoch seconds
Returning the point value of a query

You can return the point value of a query by querying the cost field on the rateLimit object:

query {
  viewer {
    login
  }
  rateLimit {
    cost
  }
}
Predicting the point value of a query

You can also roughly calculate the point value of a query before you make the query.

Add up the number of requests needed to fulfill each unique connection in the call. Assume every request will reach the first or last argument limits.
Divide the number by 100 and round the result to the nearest whole number to get the final aggregate point value. This step normalizes large numbers.
Note: The minimum point value of a call to the GraphQL API is 1.
Here's an example query and score calculation:

query {
  viewer {
    login
    repositories(first: 100) {
      edges {
        node {
          id

          issues(first: 50) {
            edges {
              node {
                id

                labels(first: 60) {
                  edges {
                    node {
                      id
                      name
                    }
                  }
                }
              }
            }
          }
        }
      }
    }
  }
}
MON=1 MGR=1 OSD=0 MDS=0 ../src/vstart.sh -d -n -x --cephadm
~/.ssh/id_dsa[.pub] is used as the cluster key. It is assumed that this key is authorized to ssh with no passphrase to root@`hostname`.
cephadm does not try to manage any daemons started by vstart.sh (any nonzero number in the environment variables). No service spec is defined for mon or mgr.
You’ll see health warnings from cephadm about stray daemons--that’s because the vstart-launched daemons aren’t controlled by cephadm.
The default image is quay.io/ceph-ci/ceph:main, but you can change this by passing -o container_image=... or ceph config set global container_image ....
CSTART AND CPATCH

The cstart.sh script will launch a cluster using cephadm and put the conf and keyring in your build dir, so that the bin/ceph ... CLI works (just like with vstart). The ckill.sh script will tear it down.

A unique but stable fsid is stored in fsid (in the build dir).
The mon port is random, just like with vstart.
The container image is quay.io/ceph-ci/ceph:$tag where $tag is the first 8 chars of the fsid.
If the container image doesn’t exist yet when you run cstart for the first time, it is built with cpatch.
There are a few advantages here:

The cluster is a “normal” cephadm cluster that looks and behaves just like a user’s cluster would. In contrast, vstart and teuthology clusters tend to be special in subtle (and not-so-subtle) ways (e.g. having the lockdep turned on).
To start a test cluster:

sudo ../src/cstart.sh
The last line of the output will be a line you can cut+paste to update the container image. For instance:

sudo ../src/script/cpatch -t quay.io/ceph-ci/ceph:8f509f4e
By default, cpatch will patch everything it can think of from the local build dir into the container image. If you are working on a specific part of the system, though, can you get away with smaller changes so that cpatch runs faster. For instance:

sudo ../src/script/cpatch -t quay.io/ceph-ci/ceph:8f509f4e --py
will update the mgr modules (minus the dashboard). Or:

sudo ../src/script/cpatch -t quay.io/ceph-ci/ceph:8f509f4e --core
will do most binaries and libraries. Pass -h to cpatch for all options.

Once the container is updated, you can refresh/restart daemons by bouncing them with:

sudo systemctl restart ceph-`cat fsid`.target
When you’re done, you can tear down the cluster with:

sudo ../src/ckill.sh   # or,
sudo ../src/cephadm/cephadm rm-cluster --force --fsid `cat fsid`
CEPHADM BOOTSTRAP --SHARED_CEPH_FOLDER

Cephadm can also be used directly without compiled ceph binaries.

Run cephadm like so:

sudo ./cephadm bootstrap --mon-ip 127.0.0.1 \
  --ssh-private-key /home/<user>/.ssh/id_rsa \
  --skip-mon-network \
  --skip-monitoring-stack --single-host-defaults \
  --skip-dashboard \
  --shared_ceph_folder /home/<user>/path/to/ceph/
~/.ssh/id_rsa is used as the cluster key. It is assumed that this key is authorized to ssh with no passphrase to root@`hostname`.
Source code changes made in the pybind/mgr/ directory then require a daemon restart to take effect.

KCLI: A VIRTUALIZATION MANAGEMENT TOOL TO MAKE EASY ORCHESTRATORS DEVELOPMENT

Kcli is meant to interact with existing virtualization providers (libvirt, KubeVirt, oVirt, OpenStack, VMware vSphere, GCP and AWS) and to easily deploy and customize VMs from cloud images.

It allows you to setup an environment with several vms with your preferred configuration (memory, cpus, disks) and OS flavor.

MAIN ADVANTAGES:

Fast. Typically you can have a completely new Ceph cluster ready to debug and develop orchestrator features in less than 5 minutes.
“Close to production” lab. The resulting lab is close to “real” clusters in QE labs or even production. It makes it easy to test “real things” in an almost “real” environment.
Safe and isolated. Does not depend of the things you have installed in your machine. And the vms are isolated from your environment.
Easy to work “dev” environment. For “not compiled” software pieces, for example any mgr module. It is an environment that allow you to test your changes interactively.
INSTALLATION:

Complete documentation in kcli installation but we suggest to use the container image approach.

So things to do:
1. Review requirements and install/configure whatever is needed to meet them.
2. get the kcli image and create one alias for executing the kcli command

# podman pull quay.io/karmab/kcli
# alias kcli='podman run --net host -it --rm --security-opt label=disable -v $HOME/.ssh:/root/.ssh -v $HOME/.kcli:/root/.kcli -v /var/lib/libvirt/images:/var/lib/libvirt/images -v /var/run/libvirt:/var/run/libvirt -v $PWD:/workdir -v /var/tmp:/ignitiondir quay.io/karmab/kcli'
Note

This assumes that /var/lib/libvirt/images is your default libvirt pool…. Adjust if using a different path
Note

Once you have used your kcli tool to create and use different labs, we suggest you stick to a given container tag and update your kcli alias. Why? kcli uses a rolling release model and sticking to a specific container tag will improve overall stability. what we want is overall stability.
TEST YOUR KCLI INSTALLATION:

See the kcli basic usage workflow

CREATE A CEPH LAB CLUSTER

In order to make this task simple, we are going to use a “plan”.

A “plan” is a file where you can define a set of vms with different settings. You can define hardware parameters (cpu, memory, disks ..), operating system and it also allows you to automate the installation and configuration of any software you want to have.

There is a repository with a collection of plans that can be used for different purposes. And we have predefined plans to install Ceph clusters using Ceph ansible or cephadm, so let’s create our first Ceph cluster using cephadm:

# kcli create plan -u https://github.com/karmab/kcli-plans/blob/master/ceph/ceph_cluster.yml
This will create a set of three vms using the plan file pointed by the url. After a few minutes, let’s check the cluster:

Take a look to the vms created:

# kcli list vms
Enter in the bootstrap node:

# kcli ssh ceph-node-00
Take a look to the ceph cluster installed:

[centos@ceph-node-00 ~]$ sudo -i
[root@ceph-node-00 ~]# cephadm version
[root@ceph-node-00 ~]# cephadm shell
[ceph: root@ceph-node-00 /]# ceph orch host ls
CREATE A CEPH CLUSTER TO MAKE EASY DEVELOPING IN MGR MODULES (ORCHESTRATORS AND DASHBOARD)

The cephadm kcli plan (and cephadm) are prepared to do that.

The idea behind this method is to replace several python mgr folders in each of the ceph daemons with the source code folders in your host machine. This “trick” will allow you to make changes in any orchestrator or dashboard module and test them intermediately. (only needed to disable/enable the mgr module)

So in order to create a ceph cluster for development purposes you must use the same cephadm plan but with a new parameter pointing to your Ceph source code folder:

# kcli create plan -u https://github.com/karmab/kcli-plans/blob/master/ceph/ceph_cluster.yml -P ceph_dev_folder=/home/mycodefolder/ceph
CEPH DASHBOARD DEVELOPMENT

Ceph dashboard module is not going to be loaded if previously you have not generated the frontend bundle.

For now, in order load properly the Ceph Dashboardmodule and to apply frontend changes you have to run “ng build” on your laptop:

# Start local frontend build with watcher (in background):
sudo dnf install -y nodejs
cd <path-to-your-ceph-repo>
cd src/pybind/mgr/dashboard/frontend
sudo chown -R <your-user>:root dist node_modules
NG_CLI_ANALYTICS=false npm ci
npm run build -- --deleteOutputPath=false --watch &
After saving your changes, the frontend bundle will be built again. When completed, you’ll see:

"Localized bundle generation complete."
Then you can reload your Dashboard browser tab.

CEPHADM BOX CONTAINER (PODMAN INSIDE PODMAN) DEVELOPMENT ENVIRONMENT

As kcli has a long startup time, we created an alternative which is faster using Podman inside Podman. This approach has its downsides too as we have to simulate the creation of osds and addition of devices with loopback devices.

Cephadm’s box environment is simple to set up. The setup requires you to get the required Podman images for Ceph and what we call boxes. A box is the first layer of Podman containers which can be either a seed or a host. A seed is the main box which holds Cephadm and where you bootstrap the cluster. On the other hand, you have hosts with a SSH server setup so you can add those hosts to the cluster. The second layer, managed by Cephadm, inside the seed box, requires the Ceph image.

Warning

This development environment is still experimental and can have unexpected behaviour. Please take a look at the road map and the known issues section to see what the development progress.
REQUIREMENTS

podman-compose
lvm
SETUP

In order to setup Cephadm’s box run:

cd src/cephadm/box
./box.py -v cluster setup
Note

It is recommended to run box with verbose (-v) as it will show the output of shell commands being run.
After getting all needed images we can create a simple cluster without OSDs and hosts with:

./box.py -v cluster start
If you want to deploy the cluster with more OSDs and hosts::
# 3 osds and 3 hosts by default sudo box -v cluster start --extended # explicitly change number of hosts and osds sudo box -v cluster start --extended --osds 5 --hosts 5

Warning

OSDs are still not supported in the box implementation with Podman. It is work in progress.
Without the extended option, explicitly adding either more hosts or OSDs won’t change the state of the cluster.

Note

Cluster start will try to setup even if cluster setup was not called.
Note

OSDs are created with loopback devices and hence, sudo is needed to create loopback devices capable of holding OSDs.
Note

Each osd will require 5GiB of space.
After bootstrapping the cluster you can go inside the seed box in which you’ll be able to run Cephadm commands:

./box.py -v cluster bash
[root@8d52a7860245] cephadm --help
[root@8d52a7860245] cephadm shell
...
If you want to navigate to the dashboard enter https://localhost:8443 on you browser.

You can also find the hostname and ip of each box container with:

./box.py cluster list
and you’ll see something like:

IP               Name            Hostname
172.30.0.2       box_hosts_1     6283b7b51d91
172.30.0.3       box_hosts_3     3dcf7f1b25a4
172.30.0.4       box_seed_1      8d52a7860245
172.30.0.5       box_hosts_2     c3c7b3273bf1
To remove the cluster and clean up run:

./box.py cluster down
If you just want to clean up the last cluster created run:

./box.py cluster cleanup
To check all available commands run:

./box.py --help
If you want to run the box with Docker you can. You’ll have to specify which engine you want to you like:

./box.py -v --engine docker cluster list
With Docker commands like bootstrap and osd creation should be called with sudo since it requires privileges to create osds on VGs and LVs:

sudo ./box.py -v --engine docker cluster start --expanded
Warning

Using Docker as the box engine is dangerous as there were some instances where the Xorg session was killed.
KNOWN ISSUES

If you get permission issues with Cephadm because it cannot infer the keyring and configuration, please run cephadm like this example:

cephadm shell --config /etc/ceph/ceph.conf --keyring /etc/ceph/ceph.kerying
Docker containers run with the --privileged flag enabled which has been seen to make some computers log out.
If SELinux is not disabled you’ll probably see unexpected behaviour. For example: if not all permissions of Ceph repo files are set to your user it will probably fail starting with podman-compose.
If running a command it fails to run a podman command because it couldn’t find the container, you can debug by running the same podman-compose .. up command displayed with the flag -v.
ROAD MAP

Create osds with ceph-volume raw.
Enable ceph-volume to mark loopback devices as a valid block device in the inventory.
Make the box ready to run dashboard CI tests (including cluster expansion).
NOTE REGARDING NETWORK CALLS FROM CLI HANDLERS

Executing any cephadm CLI commands like ceph orch ls will block the mon command handler thread within the MGR, thus preventing any concurrent CLI calls. Note that pressing ^C will not resolve this situation, as only the client will be aborted, but not execution of the command within the orchestrator manager module itself. This means, cephadm will be completely unresponsive until the execution of the CLI handler is fully completed. Note that even ceph orch ps will not respond while another handler is executing.

This means we should do very few synchronous calls to remote hosts. As a guideline, cephadm should do at most O(1) network calls in CLI handlers. Everything else should be done asynchronously in other threads, like serve().

NOTE REGARDING DIFFERENT VARIABLES USED IN THE CODE

a service_type is something like mon, mgr, alertmanager etc defined in ServiceSpec
a service_id is the name of the service. Some services don’t have names.
a service_name is <service_type>.<service_id>
a daemon_type is the same as the service_type, except for ingress, which has the haproxy and keepalived daemon types.
a daemon_id is typically <service_id>.<hostname>.<random-string>. (Not the case for e.g. OSDs. OSDs are always called OSD.N)
a daemon_name is <daemon_type>.<daemon_id>
COMPILING CEPHADM

Recent versions of cephadm are based on Python Zip Application support, and are “compiled” from Python source code files in the ceph tree. To create your own copy of the cephadm “binary” use the script located at src/cephadm/build.py in the Ceph tree. The command should take the form ./src/cephadm/build.py [output].

You can pass a limited set of version metadata values to be stored in the compiled cepadm. These options can be passed to the build script with the --set-version-var or -S option. The values should take the form KEY=VALUE and valid keys include: * CEPH_GIT_VER * CEPH_GIT_NICE_VER * CEPH_RELEASE * CEPH_RELEASE_NAME * CEPH_RELEASE_TYPE

Example: ./src/cephadm/build.py -SCEPH_GIT_VER=$(git rev-parse HEAD) -SCEPH_GIT_NICE_VER=$(git describe) /tmp/cephadm

Typically these values will be passed to build.py by other, higher level, build tools - such as cmake.

The compiled version of the binary may include a curated set of dependencies within the zipapp. The tool used to fetch the bundled dependencies can be Python’s pip, locally installed RPMs, or bundled dependencies can be disabled. To select the mode for bundled dependencies use the --bundled-dependencies or -B option with a value of pip, rpm, or none.

The compiled cephadm zipapp file retains metadata about how it was built. This can be displayed by running cephadm version --verbose. The command will emit a JSON formatted object showing version metadata (if available), a list of the bundled dependencies generated by the build script (if bundled dependencies were enabled), and a summary of the top-level contents of the zipapp. Example:

$ ./cephadm version --verbose
{
  "name": "cephadm",
  "ceph_git_nice_ver": "18.0.0-6867-g6a1df2d0b01",
  "ceph_git_ver": "6a1df2d0b01da581bfef3357940e1e88d5ce70ce",
  "ceph_release_name": "reef",
  "ceph_release_type": "dev",
  "bundled_packages": [
    {
      "name": "Jinja2",
      "version": "3.1.2",
      "package_source": "pip",
      "requirements_entry": "Jinja2 == 3.1.2"
    },
    {
      "name": "MarkupSafe",
      "version": "2.1.3",
      "package_source": "pip",
      "requirements_entry": "MarkupSafe == 2.1.3"
    }
  ],
  "zip_root_entries": [
    "Jinja2-3.1.2-py3.9.egg-info",
    "MarkupSafe-2.1.3-py3.9.egg-info",
    "__main__.py",
    "__main__.pyc",
    "_cephadmmeta",
    "cephadmlib",
    "jinja2",
    "markupsafe"
  ]
}$ WITH_JAEGER=true ./install-deps.sh
Compile Ceph with Jaeger enabled:
for precompiled build:

$ cd build
$ cmake -DWITH_JAEGER=ON ..
for fresh compilation using do_cmake.sh:

$ ./do_cmake.sh -DWITH_JAEGER=ON && ninja vstart
3. After successful compiling, start a vstart cluster with --jaeger which will deploy jaeger all-in-one using container deployment services(docker/podman):

$ MON=1 MGR=0 OSD=1 ../src/vstart.sh --with-jaeger
if the deployment is unsuccessful, you can deploy all-in-one service manually and start vstart cluster without jaeger as well.

Test the traces using rados-bench write:

$ bin/rados -p test bench 5 write --no-cleanup
 +-----------+                         +-------------+
|           |                         |             |
|           |                         | Accelerated |
| Processor |                         |  Function   |
|           |  +--------+             |    Unit     |  +--------+
|           |--| Memory |             |    (AFU)    |--| Memory |
|           |  +--------+             |             |  +--------+
+-----------+                         +-------------+
     |                                       |
+-----------+                         +-------------+
|    TL     |                         |    TLX      |
+-----------+                         +-------------+
     |                                       |
+-----------+                         +-------------+
|    DL     |                         |    DLX      |
+-----------+                         +-------------+
     |                                       |
     |                   PHY                 |
     +---------------------------------------+
         Coccinelle


Coccinelle allows programmers to easily write some complex
style-preserving source-to-source transformations on C source code,
like for instance to perform some refactorings.

To install Coccinelle from its source, see the instructions in install.txt.
Once you have installed coccinelle, there is a script 'spatch' in /usr/bin
or /usr/local/bin that invokes the Coccinelle program.

If you want to run Coccinelle without installing it, you can run the
Coccinelle program directly from the download/build directory. You may then
have to setup a few environment variables so that the Coccinelle program
knows where to find its configuration files.
For bash do:

  $ source env.sh

For tcsh do:

  $ source env.csh


You can test coccinelle with:

  $ spatch -sp_file demos/simple.cocci demos/simple.c -o /tmp/new_simple.c

If you haven't installed coccinelle, run then ./spatch or ./spatch.opt



If you downloaded the bytecode version of spatch you may first
have to install OCaml (which contains the 'ocamlrun' bytecode interpreter,
the equivalent of 'java', the Java virtual machine, but for OCaml) and then do:

  $ ocamlrun spatch -sp_file demos/simple.cocci demos/simple.c -o /tmp/new_simple.c


For more information on Coccinelle, type 'make docs' and have a look at the
files in the docs/ directory. You may need to install the texlive-fonts-extra
packages from your distribution to compile some of the LaTeX documentation
files.

 ** Runtime dependencies under Debian/Ubuntu**

 - For the OCaml scripting feature in SmPL
	ocaml-native-compilers
     or ocaml-nox

 - For the Python scripting feature in SmPL: python3-dev
   Note python3-dev is only a runtime dependency: it is _not_ required for
   building coccinelle.

---------------------------------------------------------------------------

Contributing:

Contributions are welcome.  Please sign your contributions, according to
the following text extracted from Documentation/SubmittingPatches.txt of
the Linux kernel:

The sign-off is a simple line at the end of the explanation for the
patch, which certifies that you wrote it or otherwise have the right to
pass it on as an open-source patch.  The rules are pretty simple: if you
can certify the below:

        Developer's Certificate of Origin 1.1

        By making a contribution to this project, I certify that:

        (a) The contribution was created in whole or in part by me and I
            have the right to submit it under the open source license
            indicated in the file; or

        (b) The contribution is based upon previous work that, to the best
            of my knowledge, is covered under an appropriate open source
            license and I have the right under that license to submit that
            work with modifications, whether created in whole or in part
            by me, under the same open source license (unless I am
            permitted to submit under a different license), as indicated
            in the file; or

        (c) The contribution was provided directly to me by some other
            person who certified (a), (b) or (c) and I have not modified
            it.

	(d) I understand and agree that this project and the contribution
	    are public and that a record of the contribution (including all
	    personal information I submit with it, including my sign-off) is
	    maintained indefinitely and may be redistributed consistent with
	    this project or the open source license(s) involved.

then you just add a line saying

	Signed-off-by: Random J Developer <random@developer.example.org>
./autogen
./configure
make
as a regular user, and install it with:

sudo make install
