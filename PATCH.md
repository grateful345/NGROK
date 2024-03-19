whsec_ 5V2GHGaht2mGJGNOmesTtTaxuJWFRssS
---
 README.md | 364 ++++++++++++++++++++++++++++++++++++++++++++++++++++++
 1 file changed, 364 insertions(+)

diff --git a/README.md b/README.md
index fa0eecd..2f8419f 100644
--- a/README.md
+++ b/README.md
@@ -119,6 +119,19 @@ spec:
 
 
 ngrok http 80 --request-header-remove "foo" --request-header-add "foo: new-value"
+ssh -R 443:localhost:80 v2@connect.ngrok-agent.com http
+ssh -R example.ngrok.app:443:localhost:80 v2@connect.ngrok-agent.com http
+ssh -R 443:localhost:80 v2@connect.ngrok-agent.com http \
+  --basic-auth "username1:password1" \
+  --basic-auth "username2:password2"
+ssh -R 443:localhost:80 v2@connect.ngrok-agent.com http --oauth=google
+ssh -R 0:192.168.1.2:80 v2@connect.ngrok-agent.com http
+
+ssh -R 0:localhost:22 v2@connect.ngrok-agent.com tcp
+ssh -R 1.tcp.eu.ngrok.io:12345:localhost:3389 connect.eu.ngrok-agent.com tcp
+ssh -R app.example.com:443:localhost:443 v2@connect.ngrok-agent.com tls
+ssh -R 443:localhost:80 v2@connect.eu.ngrok-agent.com http
+
 
 This will cause the HTTP request in this case to become:
 
@@ -197,6 +210,357 @@ bot_2dvYwRDLFZfzm3QuX1Yfq0xCPZh
 2dvZEkjdgaLw0K0a5G0RX80fTjJ_k2h32aY22XRhNpU5qeWd API KEY 
 
 ngrok config check
+curl \
+-X POST \
+-H "Authorization: Bearer {2dvZEkjdgaLw0K0a5G0RX80fTjJ_k2h32aY22XRhNpU5qeWd}" \
+-H "Content-Type: application/json" \
+-H "Ngrok-Version: 2" \
+-d '{"acl":["bind:1.tcp.ngrok.io:20002","bind:132.devices.company.com"],"description":"for device #132","public_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDmGS49FkSODAcKhn3+/47DW2zEn19BZvzRQ8RZjL3v6hCIX2qXfsFK35EGxNI0wV23H4xXC2gVRPHKU71YnCb50tad3yMBTM6+2yfGsEDasEH/anmBLclChKvuGiT547RskZlpbAbdq3GvbzmY+R/2EBRMOiObpc8XmSzKAd05j28kqN0+rZO65SWId0MXdvJdSCSAnuRqBNd/aXKlu8hBPDcgwbT2lMkuR+ApoBS2FLRBOiQyt2Ol0T7Uuf7lTLlazpGB3uTw5zFYUNXkuuI6cAP8QYuY1Bne/hNrG8t3Aw9a1yc2C4Fz1hJ/4OMRxTQ8SUQf+Rmxs8DryMlMFJ8r device132@example.com"}' \
+https://api.ngrok.com/ssh_credentials
+{
+	"acl": ["bind:1.tcp.ngrok.io:20002", "bind:132.devices.company.com"],
+	"created_at": "2024-02-16T19:35:31Z",
+	"description": "for device #132",
+	"id": "sshcr_2cSjyydertQFE3OLV3NIEJIp6Kh",
+	"owner_id": "usr_2cSjwF6w6AynjfPtm4Ww5xTdkId",
+	"public_key": "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDmGS49FkSODAcKhn3+/47DW2zEn19BZvzRQ8RZjL3v6hCIX2qXfsFK35EGxNI0wV23H4xXC2gVRPHKU71YnCb50tad3yMBTM6+2yfGsEDasEH/anmBLclChKvuGiT547RskZlpbAbdq3GvbzmY+R/2EBRMOiObpc8XmSzKAd05j28kqN0+rZO65SWId0MXdvJdSCSAnuRqBNd/aXKlu8hBPDcgwbT2lMkuR+ApoBS2FLRBOiQyt2Ol0T7Uuf7lTLlazpGB3uTw5zFYUNXkuuI6cAP8QYuY1Bne/hNrG8t3Aw9a1yc2C4Fz1hJ/4OMRxTQ8SUQf+Rmxs8DryMlMFJ8r device132@example.com",
+	"uri": "https://api.ngrok.com/ssh_credentials/sshcr_2cSjyydertQFE3OLV3NIEJIp6Kh"
+}
+
+curl \
+-X GET \
+-H "Authorization: Bearer {2dvZEkjdgaLw0K0a5G0RX80fTjJ_k2h32aY22XRhNpU5qeWd}" \
+-H "Ngrok-Version: 2" \
+https://api.ngrok.com/ssh_credentials/sshcr_2cSjyydertQFE3OLV3NIEJIp6Kh
+
+{
+	"acl": ["bind:1.tcp.ngrok.io:20002", "bind:132.devices.company.com"],
+	"created_at": "2024-02-16T19:35:31Z",
+	"description": "my dev machine",
+	"id": "sshcr_2cSjyydertQFE3OLV3NIEJIp6Kh",
+	"metadata": "{\"hostname\": \"macbook.local\"}",
+	"owner_id": "usr_2cSjwF6w6AynjfPtm4Ww5xTdkId",
+	"public_key": "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDmGS49FkSODAcKhn3+/47DW2zEn19BZvzRQ8RZjL3v6hCIX2qXfsFK35EGxNI0wV23H4xXC2gVRPHKU71YnCb50tad3yMBTM6+2yfGsEDasEH/anmBLclChKvuGiT547RskZlpbAbdq3GvbzmY+R/2EBRMOiObpc8XmSzKAd05j28kqN0+rZO65SWId0MXdvJdSCSAnuRqBNd/aXKlu8hBPDcgwbT2lMkuR+ApoBS2FLRBOiQyt2Ol0T7Uuf7lTLlazpGB3uTw5zFYUNXkuuI6cAP8QYuY1Bne/hNrG8t3Aw9a1yc2C4Fz1hJ/4OMRxTQ8SUQf+Rmxs8DryMlMFJ8r device132@example.com",
+	"uri": "https://api.ngrok.com/ssh_credentials/sshcr_2cSjyydertQFE3OLV3NIEJIp6Kh"
+}
+
+curl \
+-X GET \
+-H "Authorization: Bearer {2dvZEkjdgaLw0K0a5G0RX80fTjJ_k2h32aY22XRhNpU5qeWd}" \
+-H "Ngrok-Version: 2" \
+https://api.ngrok.com/ssh_credentials
+
+{
+	"next_page_uri": null,
+	"ssh_credentials": [
+		{
+			"acl": ["bind:1.tcp.ngrok.io:20002", "bind:132.devices.company.com"],
+			"created_at": "2024-02-16T19:35:31Z",
+			"description": "for device #132",
+			"id": "sshcr_2cSjyydertQFE3OLV3NIEJIp6Kh",
+			"owner_id": "usr_2cSjwF6w6AynjfPtm4Ww5xTdkId",
+			"public_key": "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDmGS49FkSODAcKhn3+/47DW2zEn19BZvzRQ8RZjL3v6hCIX2qXfsFK35EGxNI0wV23H4xXC2gVRPHKU71YnCb50tad3yMBTM6+2yfGsEDasEH/anmBLclChKvuGiT547RskZlpbAbdq3GvbzmY+R/2EBRMOiObpc8XmSzKAd05j28kqN0+rZO65SWId0MXdvJdSCSAnuRqBNd/aXKlu8hBPDcgwbT2lMkuR+ApoBS2FLRBOiQyt2Ol0T7Uuf7lTLlazpGB3uTw5zFYUNXkuuI6cAP8QYuY1Bne/hNrG8t3Aw9a1yc2C4Fz1hJ/4OMRxTQ8SUQf+Rmxs8DryMlMFJ8r device132@example.com",
+			"uri": "https://api.ngrok.com/ssh_credentials/sshcr_2cSjyydertQFE3OLV3NIEJIp6Kh"
+		}
+	],
+	"uri": "https://api.ngrok.com/ssh_credentials"
+}
+curl \
+-X PATCH \
+-H "Authorization: Bearer {2dvZEkjdgaLw0K0a5G0RX80fTjJ_k2h32aY22XRhNpU5qeWd}" \
+-H "Content-Type: application/json" \
+-H "Ngrok-Version: 2" \
+-d '{"description":"my dev machine","metadata":"{\"hostname\": \"macbook.local\"}"}' \
+https://api.ngrok.com/ssh_credentials/sshcr_2cSjyydertQFE3OLV3NIEJIp6Kh
+{
+	"acl": ["bind:1.tcp.ngrok.io:20002", "bind:132.devices.company.com"],
+	"created_at": "2024-02-16T19:35:31Z",
+	"description": "my dev machine",
+	"id": "sshcr_2cSjyydertQFE3OLV3NIEJIp6Kh",
+	"metadata": "{\"hostname\": \"macbook.local\"}",
+	"owner_id": "usr_2cSjwF6w6AynjfPtm4Ww5xTdkId",
+	"public_key": "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDmGS49FkSODAcKhn3+/47DW2zEn19BZvzRQ8RZjL3v6hCIX2qXfsFK35EGxNI0wV23H4xXC2gVRPHKU71YnCb50tad3yMBTM6+2yfGsEDasEH/anmBLclChKvuGiT547RskZlpbAbdq3GvbzmY+R/2EBRMOiObpc8XmSzKAd05j28kqN0+rZO65SWId0MXdvJdSCSAnuRqBNd/aXKlu8hBPDcgwbT2lMkuR+ApoBS2FLRBOiQyt2Ol0T7Uuf7lTLlazpGB3uTw5zFYUNXkuuI6cAP8QYuY1Bne/hNrG8t3Aw9a1yc2C4Fz1hJ/4OMRxTQ8SUQf+Rmxs8DryMlMFJ8r device132@example.com",
+	"uri": "https://api.ngrok.com/ssh_credentials/sshcr_2cSjyydertQFE3OLV3NIEJIp6Kh"
+}
+curl \
+-X POST \
+-H "Authorization: Bearer {2dvZEkjdgaLw0K0a5G0RX80fTjJ_k2h32aY22XRhNpU5qeWd}" \
+-H "Content-Type: application/json" \
+-H "Ngrok-Version: 2" \
+-d '{"description":"development cred for alan@example.com"}' \
+https://api.ngrok.com/credentials
+{
+	"acl": [],
+	"created_at": "2024-02-16T19:35:10Z",
+	"description": "development cred for alan@example.com",
+	"id": "cr_2cSjwF80LQJdOIaFZDbLWO9pMxd",
+	"owner_id": "usr_2cSjwF6w6AynjfPtm4Ww5xTdkId",
+	"token": "2cSjwF80LQJdOIaFZDbLWO9pMxd_3qYXgk4mMNpksRrJdRt6Z",
+	"uri": "https://api.ngrok.com/credentials/cr_2cSjwF80LQJdOIaFZDbLWO9pMxd"
+}
+curl \
+-X GET \
+-H "Authorization: Bearer {2dvZEkjdgaLw0K0a5G0RX80fTjJ_k2h32aY22XRhNpU5qeWd}" \
+-H "Ngrok-Version: 2" \
+https://api.ngrok.com/credentials/cr_2cSjwF80LQJdOIaFZDbLWO9pMxd
+
+{
+	"acl": [],
+	"created_at": "2024-02-16T19:35:10Z",
+	"description": "device alpha-2",
+	"id": "cr_2cSjwF80LQJdOIaFZDbLWO9pMxd",
+	"metadata": "{\"device_id\": \"d5111ba7-0cc5-4ba3-8398-e6c79e4e89c2\"}",
+	"owner_id": "usr_2cSjwF6w6AynjfPtm4Ww5xTdkId",
+	"token": null,
+	"uri": "https://api.ngrok.com/credentials/cr_2cSjwF80LQJdOIaFZDbLWO9pMxd"
+}
+curl \
+-X GET \
+-H "Authorization: Bearer {2dvZEkjdgaLw0K0a5G0RX80fTjJ_k2h32aY22XRhNpU5qeWd}" \
+-H "Ngrok-Version: 2" \
+https://api.ngrok.com/credentials
+
+{
+	"credentials": [
+		{
+			"acl": [],
+			"created_at": "2024-02-16T19:35:09Z",
+			"description": "credential for \"api-examples-c954256d6ada8b72@example.com\"",
+			"id": "cr_2cSjwL9yhXwTeYnIOSxZlvZ8S8y",
+			"owner_id": "usr_2cSjwF6w6AynjfPtm4Ww5xTdkId",
+			"token": null,
+			"uri": "https://api.ngrok.com/credentials/cr_2cSjwL9yhXwTeYnIOSxZlvZ8S8y"
+		},
+		{
+			"acl": ["bind:1.tcp.ngrok.io:20002", "bind:132.devices.company.com"],
+			"created_at": "2024-02-16T19:35:10Z",
+			"description": "for device #132",
+			"id": "cr_2cSjwHg6uyMl2h31jEgXZOHI77u",
+			"owner_id": "usr_2cSjwF6w6AynjfPtm4Ww5xTdkId",
+			"token": null,
+			"uri": "https://api.ngrok.com/credentials/cr_2cSjwHg6uyMl2h31jEgXZOHI77u"
+		},
+		{
+			"acl": [],
+			"created_at": "2024-02-16T19:35:10Z",
+			"description": "development cred for alan@example.com",
+			"id": "cr_2cSjwF80LQJdOIaFZDbLWO9pMxd",
+			"owner_id": "usr_2cSjwF6w6AynjfPtm4Ww5xTdkId",
+			"token": null,
+			"uri": "https://api.ngrok.com/credentials/cr_2cSjwF80LQJdOIaFZDbLWO9pMxd"
+		}
+	],
+	"next_page_uri": null,
+	"uri": "https://api.ngrok.com/credentials"
+}
+
+
+
+
+curl \
+-X PATCH \
+-H "Authorization: Bearer {2dvZEkjdgaLw0K0a5G0RX80fTjJ_k2h32aY22XRhNpU5qeWd}" \
+-H "Content-Type: application/json" \
+-H "Ngrok-Version: 2" \
+-d '{"description":"device alpha-2","metadata":"{\"device_id\": \"d5111ba7-0cc5-4ba3-8398-e6c79e4e89c2\"}"}' \
+https://api.ngrok.com/credentials/cr_2cSjwF80LQJdOIaFZDbLWO9pMxd
+{
+	"acl": [],
+	"created_at": "2024-02-16T19:35:10Z",
+	"description": "device alpha-2",
+	"id": "cr_2cSjwF80LQJdOIaFZDbLWO9pMxd",
+	"metadata": "{\"device_id\": \"d5111ba7-0cc5-4ba3-8398-e6c79e4e89c2\"}",
+	"owner_id": "usr_2cSjwF6w6AynjfPtm4Ww5xTdkId",
+	"token": null,
+	"uri": "https://api.ngrok.com/credentials/cr_2cSjwF80LQJdOIaFZDbLWO9pMxd"
+}
+import ngrok
+
+listener = ngrok.forward("localhost:8080", authtoken_from_env=True,
+    circuit_breaker=0.5)
+
+print(f"Ingress established at: {listener.url()}");
+
+package main
+
+import (
+	"context"
+	"fmt"
+	"log"
+	"net"
+	"net/http"
+	"net/url"
+	"os"
+
+	"golang.ngrok.com/ngrok"
+	"golang.ngrok.com/ngrok/config"
+)
+
+func main() {
+	l, err := ngrok.Listen(context.Background(),
+		config.HTTPEndpoint(
+			config.WithCircuitBreaker(0.1),
+		),
+		ngrok.WithAuthtokenFromEnv(),
+	)
+	if err != nil {
+		log.Fatal(err)
+	}
+	fmt.Println("Running at", l.URL())
+	go makeRequests(l.URL())
+	http.Serve(l, http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
+		if r.URL.Path == "/500" {
+			w.WriteHeader(500)
+			fmt.Fprintln(w, "Hello error!")
+		} else {
+			w.WriteHeader(200)
+			fmt.Fprintln(w, "Hello world!")
+		}
+	}))
+}
+
+func makeRequests(appURL string) {
+	// make sure we always dial the same IP addresss for testing purposes because
+	// circuit breaker state is applied on each ngrok edge server individually
+	u, _ := url.Parse(appURL)
+	addrs, err := net.LookupHost(u.Host)
+	if err != nil {
+		log.Fatal(err)
+	}
+	httpClient := http.Client{Transport: &http.Transport{
+		Dial: func(network, _ string) (net.Conn, error) {
+			return net.Dial(network, addrs[0]+":443")
+		},
+	}}
+
+	// make requests that return a 500 until the circuit opens
+	for {
+		resp, err := httpClient.Get(appURL + "/500")
+		if err != nil {
+			log.Fatal(err)
+		}
+		fmt.Printf("Status Code %d\n", resp.StatusCode)
+		if resp.StatusCode == 503 {
+			fmt.Println("Circuit opened")
+			break
+		}
+	}
+
+	// make requests that will eventually return a 200 which will close the circuit
+	for {
+		resp, err := httpClient.Get(appURL)
+		if err != nil {
+			log.Fatal(err)
+		}
+		fmt.Printf("Status Code %d\n", resp.StatusCode)
+		if resp.StatusCode != 503 {
+			fmt.Println("Circuit closed")
+			os.Exit(0)
+		}
+	}
+}
+
+package main
+
+import (
+	"context"
+	"fmt"
+	"log"
+	"net"
+	"net/http"
+	"net/url"
+	"os"
+
+	"golang.ngrok.com/ngrok"
+	"golang.ngrok.com/ngrok/config"
+)
+
+func main() {
+	l, err := ngrok.Listen(context.Background(),
+		config.HTTPEndpoint(
+			config.WithCircuitBreaker(0.1),
+		),
+		ngrok.WithAuthtokenFromEnv(),
+	)
+	if err != nil {
+		log.Fatal(err)
+	}
+	fmt.Println("Running at", l.URL())
+	go makeRequests(l.URL())
+	http.Serve(l, http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
+		if r.URL.Path == "/500" {
+			w.WriteHeader(500)
+			fmt.Fprintln(w, "Hello error!")
+		} else {
+			w.WriteHeader(200)
+			fmt.Fprintln(w, "Hello world!")
+		}
+	}))
+}
+
+func makeRequests(appURL string) {
+	// make sure we always dial the same IP addresss for testing purposes because
+	// circuit breaker state is applied on each ngrok edge server individually
+	u, _ := url.Parse(appURL)
+	addrs, err := net.LookupHost(u.Host)
+	if err != nil {
+		log.Fatal(err)
+	}
+	httpClient := http.Client{Transport: &http.Transport{
+		Dial: func(network, _ string) (net.Conn, error) {
+			return net.Dial(network, addrs[0]+":443")
+		},
+	}}
+
+	// make requests that return a 500 until the circuit opens
+	for {
+		resp, err := httpClient.Get(appURL + "/500")
+		if err != nil {
+			log.Fatal(err)
+		}
+		fmt.Printf("Status Code %d\n", resp.StatusCode)
+		if resp.StatusCode == 503 {
+			fmt.Println("Circuit opened")
+			break
+		}
+	}
+
+	// make requests that will eventually return a 200 which will close the circuit
+	for {
+		resp, err := httpClient.Get(appURL)
+		if err != nil {
+			log.Fatal(err)
+		}
+		fmt.Printf("Status Code %d\n", resp.StatusCode)
+		if resp.StatusCode != 503 {
+			fmt.Println("Circuit closed")
+			os.Exit(0)
+		}
+	}
+
+export NGROK_AUTHTOKEN="<2dvYx8b2Jxcr6rQ7rMK4g0f5lxd_6MRbqiQJdYkspcWN1vb65>"
+go mod init example.com/ngrok-circuit-breaker
+go get golang.ngrok.com/ngrok
+go run example.go
+import ngrok
+
+listener = ngrok.forward("localhost:8080", authtoken_from_env=True,
+    verify_webhook_provider="twilio",
+    verify_webhook_secret="{twilio signing secret}")
+
+print(f"Ingress established at: {listener.url()}");
+
+git clone https://github.com/ngrok/ngrok-webhook-nodejs-sample.git
+cd ngrok-webhook-nodejs-sample
+npm install
+npm start
+ngrok http 3000
+
+ngrok http 3000 --verify-webhook stripe --verify-webhook-secret {whsec_ 5V2GHGaht2mGJGNOmesTtTaxuJWFRssS}
+
+
+
+
 
 authtoken: 4nq9771bPxe8ctg7LKr_2ClH7Y15Zqe4bWLWF9p
 api_key: 24yRd5U3DestCQapJrrVHLOqiAC_7RviwRqpd3wc9dKLujQZN
