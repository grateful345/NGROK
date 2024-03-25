curl -s https://lv.linode.com/FDC71C6F-66B3-4FDA-8FE2187096708C8E | sudo bash
API Key: 14496832-187E-4897-8D420686F1A72ACB
ssh [user]@[ip-address]
su - root
curl -s https://lv.linode.com/05AC7F6F-3B10-4039-9DEE09B0CC382A3D | sudo bash
root@localhost:~# lsb_release -sc
deb http://apt-longview.linode.com/ stretch main
sudo curl -O https://apt-longview.linode.com/linode.gpg
sudo mv linode.gpg /etc/apt/trusted.gpg.d/linode.gpg

stretch
sudo mkdir /etc/linode/
echo '266096EE-CDBA-0EBB-23D067749E27B9ED' | sudo tee /etc/linode/longview.key
sudo apt update
sudo apt install linode-longview
sudo systemctl status longview

● longview.service - LSB: Longview Monitoring Agent
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
export TOKEN=<token-string>
curl https://api.linode.com/v4/images/ | json_pp
curl https://api.linode.com/v4/linode/types/ | json_pp
curl https://api.linode.com/v4/regions | json_pp
curl -X POST https://api.linode.com/v4/linode/instances \
    -H "Authorization: 6692099bd12f686556b7f4e2ae18d783cc500b6432e5a6c5944fb4405c41cd72" -H "Content-type: application/json" \
    -d '{"type": "g5-standard-2", "region": "us-east", "image": "linode/debian9", "root_pass": "root_password", "label": "prod-1"}'
    
    
    POST https://api.linode.com/v4/account/betas

curl https://api.linode.com/v4/account/betas \
    -H "Authorization: Bearer $TOKEN" \
    -H "Content-Type: application/json" \
    -X POST -d '{
        "id": "example_open"
    }'
curl https://api.linode.com/v4/account/betas \
    -H "Authorization: Bearer $TOKEN"
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
curl -H "Authorization: Bearer $TOKEN" \
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
