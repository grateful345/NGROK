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
