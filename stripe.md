sk_test_51OR5ePGF83d3fsgWlh41IbGHGtqdiPuFhrcWczglEeFJvQxajyQVCQiZYVZz62HOuYL9tA8dxEQ2MRbxbcYsf8OF00CdDfT6Xq
---
 keith.md | 712 +++++++++++++++++++++++++++++++++++++++++++++++++++++++
 1 file changed, 712 insertions(+)

diff --git a/keith.md b/keith.md
index 0db29b4..87738f3 100644
--- a/keith.md
+++ b/keith.md
@@ -6,10 +6,722 @@ stripe.api_key = "sk_test_51OR5ePGF83d3fsgWlh41IbGHGtqdiPuFhrcWczglEeFJvQxajyQVC
 stripe.Customer.modify(
   "cus_V9T7vofUbZMqpv",
   source="tok_visa",
+select
+  id,
+  amount,
+  fee,
+  currency
+from balance_transactions -- this table is the canonical record of changes to your Stripe balance
+where
+  created < data_load_time and
+  created >= data_load_time - interval '1' month
+order by created desc
+limit 10
+# Install through pip
+pip3 install --upgrade stripe
+PyPi
+Python
+(orgname-account_name).
+
+Syntax
+
+CURRENT_ACCOUNT_NAME()
+Arguments
+
+None.
+
+Returns
+
+Returns the name of the current account.
+
+The data type of the returned value is VARCHAR.
+
+Example
+
+This shows how to call the CURRENT_ACCOUNT_NAME function:
+
+SELECT CURRENT_ACCOUNT_NAME();
+Output:
+
++-----------------------------+
+| CURRENT_ACCOUNT_NAME()      |
+|-----------------------------|
+| keith bieszczat                 |
++-----------------------------+
+Was this page helpful?
+Yes
+sk_test_51OR5ePGF83d3fsgWlh41IbGHGtqdiPuFhrcWczglEeFJvQxajyQVCQiZYVZz62HOuYL9tA8dxEQ2MRbxbcYsf8OF00CdDfT6Xq
+
+pk_test_51OR5ePGF83d3fsgWcl7ad29rrqOUNvjdYXN1JrElZlEyDloYQpFPuxSeRZH8KiCgvshlSaDYnuu1xxYiiWOCHj7W00Nrph1csX
+import stripe, logging
+stripe.api_key = sk_test_51OR5ePGF83d3fsgWlh41IbGHGtqdiPuFhrcWczglEeFJvQxajyQVCQiZYVZz62HOuYL9tA8dxEQ2MRbxbcYsf8OF00CdDfT6Xq
+
+def example_function(**kwargs):
+  try:
+    stripe.PaymentIntent.create(**kwargs)
+  except stripe.error.CardError as e:
+    charge = stripe.Charge.retrieve(e.error.payment_intent.latest_charge)
+    if charge.outcome.type == 'blocked':
+      logging.error("Payment blocked for suspected fraud.")
+    elif e.code == 'card_declined':
+      logging.error("Payment declined by the issuer.")
+    elif e.code == 'expired_card':
+      logging.error("Card expired.")
+    else:
+      logging.error("Other card error.")
+      import stripe, logging
+stripe.api_key = sk_test_51OR5ePGF83d3fsgWlh41IbGHGtqdiPuFhrcWczglEeFJvQxajyQVCQiZYVZz62HOuYL9tA8dxEQ2MRbxbcYsf8OF00CdDfT6Xq
+
+def example_function(**kwargs):
+  try:
+    stripe.PaymentIntent.create(**kwargs)
+  except stripe.error.CardError as e:
+    if e.error.payment_intent.charges.data[0].outcome.type == 'blocked':
+      logging.error("Payment blocked for suspected fraud.")
+    elif e.code == 'card_declined':
+      logging.error("Payment declined by the issuer.")
+    elif e.code == 'expired_card':
+      logging.error("Card expired.")
+    else:
+      logging.error("Other card error.")
+
+import stripe
+stripe.api_key = "sk_test_51OR5eP...OF00CdDfT6Xqsk_test_51OR5ePGF83d3fsgWlh41IbGHGtqdiPuFhrcWczglEeFJvQxajyQVCQiZYVZz62HOuYL9tA8dxEQ2MRbxbcYsf8OF00CdDfT6Xq"
+stripe.Charge.retrieve(
+  'ch_3Ln0cK2eZvKYlo2C1QmvaARY',
+  expand=['customer', 'invoice.subscription']
+)
+RESPONSE
+{
+  "id": "ch_3LmzzQ2eZvKYlo2C0XjzUzJV",
+  "object": "charge",
+  "customer": {
+    "id": "cu_14HOpH2eZvKYlo2CxXIM7Pb2",
+    "object": "customer",
+    // ...
+  },
+  "invoice": {
+    "id": "in_1LmzzQ2eZvKYlo2CpyWn8szu",
+    "object": "invoice",
+    "subscription": {
+      "id": "su_1LmzoG2eZvKYlo2Cpw6S7dAq",
+      "object": "subscription",
+      // ...
+    },
+    // ...
+  },
+  // ...
+}
+Idempotent requests
+
+The API supports idempotency for safely retrying requests without accidentally performing the same operation twice. When creating or updating an object, use an idempotency key. Then, if a connection error occurs, you can safely repeat the request without risk of creating a second object or performing the update twice.
+To perform an idempotent request, provide an additional IdempotencyKey element to the request options.
+Stripe’s idempotency works by saving the resulting status code and body of the first request made for any given idempotency key, regardless of whether it succeedes or fails. Subsequent requests with the same key return the same result, including 500 errors.
+A client generates an idempotency key, which is a unique key that the server uses to recognize subsequent retries of the same request. How you create unique keys is up to you, but we suggest using V4 UUIDs, or another random string with enough entropy to avoid collisions. Idempotency keys are up to 255 characters long.
+You can remove keys from the system automatically after they’re at least 24 hours old. We generate a new request if a key is reused after the original is pruned. The idempotency layer compares incoming parameters to those of the original request and errors if they’re the same to prevent accidental misuse.
+We save results only after the execution of an endpoint begins. If incoming parameters fail validation, or the request conflicts with another request that’s executing concurrently, we don’t save the idempotent result because no API endpoint initiates the execution. You can retry these requests. Learn more about when you can retry idempotent requests.
+All POST requests accept idempotency keys. Don’t send idempotency keys in GET and DELETE requests because it has no effect. These requests are idempotent by definition.
+Related video: Idempotency and retries
+Server-side language
+
+import stripe
+stripe.api_key = 'sk_test_51OR5eP...OF00CdDfT6Xqsk_test_51OR5ePGF83d3fsgWlh41IbGHGtqdiPuFhrcWczglEeFJvQxajyQVCQiZYVZz62HOuYL9tA8dxEQ2MRbxbcYsf8OF00CdDfT6Xq'
+customer = stripe.Customer.create(
+  description='My First Test Customer',
+  idempotency_key='KG5LxwFBepaKHyUD',
+)
+Metadata
+
+Updateable Stripe objects—including Account, Charge, Customer, PaymentIntent, Refund, Subscription, and Transfer have a metadata parameter. You can use this parameter to attach key-value data to these Stripe objects.
+You can specify up to 50 keys, with key names up to 40 characters long and values up to 500 characters long.
+You can use metadata to store additional, structured information on an object. For example, you could store your user’s full name and corresponding unique identifier from your system on a Stripe Customer object. Stripe doesn’t use metadata—for example, we don’t use it to authorize or decline a charge and it won’t be seen by your users unless you choose to show it to them.
+Some of the objects listed above also support a description parameter. You can use the description parameter to annotate a charge-for example, a human-readable description such as 2 shirts for test@example.com. Unlike metadata, description is a single string, which your users might see (for example, in email receipts Stripe sends on your behalf).
+Don’t store any sensitive information (bank account numbers, card details, and so on) as metadata or in the description parameter.
+Related video: Metadata
+Sample metadata use cases
+Link IDs: Attach your system’s unique IDs to a Stripe object to simplify lookups. For example, add your order number to a charge, your user ID to a customer or recipient, or a unique receipt number to a transfer.
+Refund papertrails: Store information about the reason for a refund and the individual responsible for its creation.
+Customer details: Annotate a customer by storing an internal ID for your future use.
+POST 
+/v1/customers
+Server-side language
+
+import stripe
+stripe.api_key = "sk_test_51OR5eP...OF00CdDfT6Xqsk_test_51OR5ePGF83d3fsgWlh41IbGHGtqdiPuFhrcWczglEeFJvQxajyQVCQiZYVZz62HOuYL9tA8dxEQ2MRbxbcYsf8OF00CdDfT6Xq"
+stripe.Customer.create(metadata={"order_id": "6735"})
+{
+  "id": "cus_123456789",
+  "object": "customer",
+  "address": {
+    "city": "city",
+    "country": "US",
+    "line1": "line 1",
+    "line2": "line 2",
+    "postal_code": "90210",
+    "state": "CA"
+  },
+  "balance": 0,
+  "created": 1483565364,
+  "currency": null,
+  "default_source": null,
+  "delinquent": false,
+  "description": null,
+  "discount": null,
+  "email": null,
+  "invoice_prefix": "C11F7E1",
+  "invoice_settings": {
+    "custom_fields": null,
+    "default_payment_method": null,
+    "footer": null,
+    "rendering_options": null
+  },
+  "livemode": false,
+  "metadata": {
+    "order_id": "6735"
+  },
+  "name": null,
+  "next_invoice_sequence": 1,
+  "phone": null,
+  "preferred_locales": [],
+  "shipping": null,
+  "tax_exempt": "none"
+}
+Pagination
+
+All top-level API resources have support for bulk fetches through “list” API methods. For example, you can list charges, list customers, and list invoices. These list API methods share a common structure and accept, at a minimum, the following three parameters: limit, starting_after, and ending_before.
+Stripe’s list API methods use cursor-based pagination through the starting_after and ending_before parameters. Both parameters accept an existing object ID value (see below) and return objects in reverse chronological order. The ending_before parameter returns objects listed before the named object. The starting_after parameter returns objects listed after the named object. These parameters are mutually exclusive. You can use either the starting_after or ending_before parameter, but not both simultaneously.
+Our client libraries offer auto-pagination helpers to traverse all pages of a list.
+Related video: Pagination and auto-pagination
+Parameters
+
+
+limit
+optional, default is 10
+This specifies a limit on the number of objects to return, ranging between 1 and 100.
+
+starting_after
+optional object ID
+A cursor to use in pagination. starting_after is an object ID that defines your place in the list. For example, if you make a list request and receive 100 objects, ending with obj_foo, your subsequent call can include starting_after=obj_foo to fetch the next page of the list.
+
+ending_before
+optional object ID
+A cursor to use in pagination. ending_before is an object ID that defines your place in the list. For example, if you make a list request and receive 100 objects, starting with obj_bar, your subsequent call can include ending_before=obj_bar to fetch the previous page of the list.
+List Response Format
 
 
+object
+string, value is "list"
+A string that provides a description of the object type that returns.
+
+data
+array
+An array containing the actual response elements, paginated by any request parameters.
+
+has_more
+boolean
+Whether or not there are more elements available after this set. If false, this set comprises the end of the list.
+
+url
+url
+The URL for accessing this list.
+RESPONSE
+{
+  "object": "list",
+  "url": "/v1/customers",
+  "has_more": false,
+  "data": [
+    {
+      "id": "cus_4QFJOjw2pOmAGJ",
+      "object": "customer",
+      "address": null,
+      "balance": 0,
+      "created": 1405641735,
+      "currency": "usd",
+      "default_source": "card_14HOpG2eZvKYlo2Cz4u5AJG5",
+      "delinquent": false,
+      "description": "New customer",
+      "discount": null,
+      "email": null,
+      "invoice_prefix": "7D11B54",
+      "invoice_settings": {
+        "custom_fields": null,
+        "default_payment_method": null,
+        "footer": null,
+        "rendering_options": null
+      },
+      "livemode": false,
+      "metadata": {
+        "order_id": "6735"
+      },
+      "name": "cus_4QFJOjw2pOmAGJ",
+      "next_invoice_sequence": 25,
+      "phone": null,
+      "preferred_locales": [],
+      "shipping": null,
+      "tax_exempt": "none",
+      "test_clock": null
+    },
+    {...},
+    {...}
+  ]
+}
+Search
+
+Some top-level API resource have support for retrieval via “search” API methods. For example, you can search charges, search customers, and search subscriptions.
+Stripe’s search API methods utilize cursor-based pagination via the page request parameter and next_page response parameter. For example, if you make a search request and receive "next_page": "pagination_key" in the response, your subsequent call can include page=pagination_key to fetch the next page of results.
+Our client libraries offer auto-pagination helpers to easily traverse all pages of a search result.
+Search request format
+
+
+query
+required
+The search query string. See search query language.
+
+limit
+optional
+A limit on the number of objects to be returned. Limit can range between 1 and 100, and the default is 10.
+
+page
+optional
+A cursor for pagination across multiple pages of results. Don’t include this parameter on the first call. Use the next_page value returned in a previous response to request subsequent results.
+Search response format
+
+
+object
+string, value is "search_result"
+A string describing the object type returned.
+
+url
+string
+The URL for accessing this list.
+
+has_more
+boolean
+Whether or not there are more elements available after this set. If false, this set comprises the end of the list.
+
+data
+array
+An array containing the actual response elements, paginated by any request parameters.
+
+next_page
+string
+A cursor for use in pagination. If has_more is true, you can pass the value of next_page to a subsequent call to fetch the next page of results.
+
+total_count
+optional positive integer or zero
+The total number of objects that match the query, only accurate up to 10,000. This field is not included by default. To include it in the response, expand the total_count field.
+RESPONSE
+{
+  "object": "search_result",
+  "url": "/v1/customers/search",
+  "has_more": false,
+  "data": [
+    {
+      "id": "cus_4QFJOjw2pOmAGJ",
+      "object": "customer",
+      "address": null,
+      "balance": 0,
+      "created": 1405641735,
+      "currency": "usd",
+      "default_source": "card_14HOpG2eZvKYlo2Cz4u5AJG5",
+      "delinquent": false,
+      "description": "someone@example.com for Coderwall",
+      "discount": null,
+      "email": null,
+      "invoice_prefix": "7D11B54",
+      "invoice_settings": {
+        "custom_fields": null,
+        "default_payment_method": null,
+        "footer": null,
+        "rendering_options": null
+      },
+      "livemode": false,
+      "metadata": {
+        "foo": "bar"
+      },
+      "name": "fakename",
+      "next_invoice_sequence": 25,
+      "phone": null,
+      "preferred_locales": [],
+      "shipping": null,
+      "tax_exempt": "none",
+      "test_clock": null
+    },
+    {...},
+    {...}
+  ]
+}
+Auto-pagination
+
+Our libraries support auto-pagination. This feature allows you to easily iterate through large lists of resources without having to manually perform the requests to fetch subsequent pages.
+To use the auto-pagination feature in Python, simply issue an initial “list” call with the parameters you need, then call auto_paging_iter() on the returned list object to iterate over all objects matching your initial parameters.
+Server-side language
+
+import stripe
+stripe.api_key = "sk_test_51OR5eP...OF00CdDfT6Xqsk_test_51OR5ePGF83d3fsgWlh41IbGHGtqdiPuFhrcWczglEeFJvQxajyQVCQiZYVZz62HOuYL9tA8dxEQ2MRbxbcYsf8OF00CdDfT6Xq"
+customers = stripe.Customer.list(limit=3)
+for customer in customers.auto_paging_iter():
+  # Do something with customer
+Request IDs
+
+Each API request has an associated request identifier. You can find this value in the response headers, under Request-Id. You can also find request identifiers in the URLs of individual request logs in your Dashboard.
+To expedite the resolution process, provide the request identifier when you contact us about a specific request.
+Server-side language
+
 import stripe
 stripe.api_key = "sk_test_51OR5eP...OF00CdDfT6Xqsk_test_51OR5ePGF83d3fsgWlh41IbGHGtqdiPuFhrcWczglEeFJvQxajyQVCQiZYVZz62HOuYL9tA8dxEQ2MRbxbcYsf8OF00CdDfT6Xq"
+customer = stripe.Customer.create()
+print(customer.last_response.request_id)
+Versioning
+
+When backwards-incompatible changes are made to the API, we release a new, dated version. The current version is 2023-10-16. Learn more about API upgrades and backwards compatibility. For information on all API updates, view our API changelog.
+Starting from stripe-python v6, the API version fixed at the time of your stripe-python version release dictates the requests you send using stripe-python.
+On stripe-python versions v5 or lower, requests made with stripe-python use your Stripe account’s default API version, controlled in the Dashboard.
+You can override the API version in your code in all versions.
+To override the API version, assign the version to the stripe.api_version property, or set it per-request as shown in the adjacent code sample. When overriding it per-request, methods on the returned object reuse the same Stripe version.
+Webhook events use the API version that’s set during your webhook’s endpoint creation. Otherwise, they use your Stripe account’s default API version (controlled in the Dashboard). If you’re on stripe-python v6 or later, match your webhook endpoint API version to the version pinned by your version of stripe-python (stripe.api_version property).
+You can upgrade your API version in the Developer Dashboard. As a precaution, use API versioning to test a new API version before committing to an upgrade.
+Related video: Versioning
+Server-side language
+
+import stripe
+stripe.api_key = "sk_test_51OR5eP...OF00CdDfT6Xqsk_test_51OR5ePGF83d3fsgWlh41IbGHGtqdiPuFhrcWczglEeFJvQxajyQVCQiZYVZz62HOuYL9tA8dxEQ2MRbxbcYsf8OF00CdDfT6Xq"
+stripe.api_version = "2023-10-16"
+Balance
+
+This is an object representing your Stripe balance. You can retrieve it to see the balance currently on your Stripe account.
+You can also retrieve the balance history, which contains a list of transactions that contributed to the balance (charges, payouts, and so forth).
+The available and pending amounts for each currency are broken down further by payment source types.
+Related guide: Understanding Connect account balances
+ENDPOINTS
+GET
+/v1/balance
+
+
+
+secret
+string
+The endpoint’s secret, used to generate webhook signatures. Only returned at creation.
+
+status
+string
+The status of the webhook. It can be enabled or disabled.
+
+url
+string
+The URL of the webhook endpoint.
+More attributes
+Expand all
+
+
+object
+string
+
+application
+nullable string
+
+created
+timestamp
+
+livemode
+boolean
+THE WEBHOOK ENDPOINT OBJECT
+{
+  "id": "we_1Mr5jULkdIwHu7ix1ibLTM0x",
+  "object": "webhook_endpoint",
+  "api_version": null,
+  "application": null,
+  "created": 1680122196,
+  "description": null,
+  "enabled_events": [
+    "charge.succeeded",
+    "charge.failed"
+  ],
+  "livemode": false,
+  "metadata": {},
+  "secret": "whsec_wRNftLajMZNeslQOP6vEPm4iVx5NlZ6z",
+  "status": "enabled",
+  "url": "https://example.com/my/webhook/endpoint"
+}
+Create a webhook endpoint
+
+A webhook endpoint must have a url and a list of enabled_events. You may optionally specify the Boolean connect parameter. If set to true, then a Connect webhook endpoint that notifies the specified url about events from all connected accounts is created; otherwise an account webhook endpoint that notifies the specified url only about events from your account is created. You can also create webhook endpoints in the webhooks settings section of the Dashboard.
+Parameters
+
+
+enabled_events
+array of enums
+Required
+The list of events to enable for this endpoint. You may specify ['*'] to enable all events, except those that require explicit selection.
+Possible enum values
+account.application.authorized
+Occurs whenever a user authorizes an application. Sent to the related application only.
+account.application.deauthorized
+Occurs whenever a user deauthorizes an application. Sent to the related application only.
+account.external_account.created
+Occurs whenever an external account is created.
+account.external_account.deleted
+Occurs whenever an external account is deleted.
+account.external_account.updated
+Occurs whenever an external account is updated.
+account.updated
+Occurs whenever an account status or property has changed.
+application_fee.created
+Occurs whenever an application fee is created on a charge.
+application_fee.refund.updated
+Occurs whenever an application fee refund is updated.
+application_fee.refunded
+Occurs whenever an application fee is refunded, whether from refunding a charge or from refunding the application fee directly. This includes partial refunds.
+balance.available
+Occurs whenever your Stripe balance has been updated (e.g., when a charge is available to be paid out). By default, Stripe automatically transfers funds in your balance to your bank account on a daily basis. This event is not fired for negative transactions.
+Show 339 more
+
+url
+string
+Required
+The URL of the webhook endpoint.
+
+api_version
+string
+Events sent to this endpoint will be generated with this Stripe Version instead of your account’s default Stripe Version.
+
+description
+string
+An optional description of what the webhook is used for.
+
+metadata
+dictionary
+Set of key-value pairs that you can attach to an object. This can be useful for storing additional information about the object in a structured format. Individual keys can be unset by posting an empty value to them. All keys can be unset by posting an empty value to metadata.
+More parameters
+Expand all
+
+
+connect
+boolean
+Returns
+
+Returns the webhook endpoint object with the secret field populated.
+POST 
+/v1/webhook_endpoints
+Server-side language
+
+import stripe
+stripe.api_key = "sk_test_51OR5eP...OF00CdDfT6Xqsk_test_51OR5ePGF83d3fsgWlh41IbGHGtqdiPuFhrcWczglEeFJvQxajyQVCQiZYVZz62HOuYL9tA8dxEQ2MRbxbcYsf8OF00CdDfT6Xq"
+stripe.WebhookEndpoint.create(
+  enabled_events=["charge.succeeded", "charge.failed"],
+  url="https://example.com/my/webhook/endpoint",
+)
+RESPONSE
+{
+  "id": "we_1Mr5jULkdIwHu7ix1ibLTM0x",
+  "object": "webhook_endpoint",
+  "api_version": null,
+  "application": null,
+  "created": 1680122196,
+  "description": null,
+  "enabled_events": [
+    "charge.succeeded",
+    "charge.failed"
+  ],
+  "livemode": false,
+  "metadata": {},
+  "secret": "whsec_wRNftLajMZNeslQOP6vEPm4iVx5NlZ6z",
+  "status": "enabled",
+  "url": "https://example.com/my/webhook/endpoint"
+}
+Update a webhook endpoint
+
+Updates the webhook endpoint. You may edit the url, the list of enabled_events, and the status of your endpoint.
+Parameters
+
+
+description
+string
+An optional description of what the webhook is used for.
+
+enabled_events
+array of enums
+The list of events to enable for this endpoint. You may specify ['*'] to enable all events, except those that require explicit selection.
+Possible enum values
+account.application.authorized
+Occurs whenever a user authorizes an application. Sent to the related application only.
+account.application.deauthorized
+Occurs whenever a user deauthorizes an application. Sent to the related application only.
+account.external_account.created
+Occurs whenever an external account is created.
+account.external_account.deleted
+Occurs whenever an external account is deleted.
+account.external_account.updated
+Occurs whenever an external account is updated.
+account.updated
+Occurs whenever an account status or property has changed.
+application_fee.created
+Occurs whenever an application fee is created on a charge.
+application_fee.refund.updated
+Occurs whenever an application fee refund is updated.
+application_fee.refunded
+Occurs whenever an application fee is refunded, whether from refunding a charge or from refunding the application fee directly. This includes partial refunds.
+balance.available
+Occurs whenever your Stripe balance has been updated (e.g., when a charge is available to be paid out). By default, Stripe automatically transfers funds in your balance to your bank account on a daily basis. This event is not fired for negative transactions.
+Show 339 more
+
+metadata
+dictionary
+Set of key-value pairs that you can attach to an object. This can be useful for storing additional information about the object in a structured format. Individual keys can be unset by posting an empty value to them. All keys can be unset by posting an empty value to metadata.
+
+url
+string
+The URL of the webhook endpoint.
+More parameters
+Expand all
+
+
+disabled
+boolean
+Returns
+
+The updated webhook endpoint object if successful. Otherwise, this call raises an error.
+POST 
+/v1/webhook_endpoints/:id
+Server-side language
+
+import stripe
+stripe.api_key = "sk_test_51OR5eP...OF00CdDfT6Xqsk_test_51OR5ePGF83d3fsgWlh41IbGHGtqdiPuFhrcWczglEeFJvQxajyQVCQiZYVZz62HOuYL9tA8dxEQ2MRbxbcYsf8OF00CdDfT6Xq"
+stripe.WebhookEndpoint.modify(
+  "we_1Mr5jULkdIwHu7ix1ibLTM0x",
+  url="https://example.com/new_endpoint",
+)
+RESPONSE
+{
+  "id": "we_1Mr5jULkdIwHu7ix1ibLTM0x",
+  "object": "webhook_endpoint",
+  "api_version": null,
+  "application": null,
+  "created": 1680122196,
+  "description": null,
+  "enabled_events": [
+    "charge.succeeded",
+    "charge.failed"
+  ],
+  "livemode": false,
+  "metadata": {},
+  "status": "disabled",
+  "url": "https://example.com/new_endpoint"
+}
+Retrieve a webhook endpoint
+
+Retrieves the webhook endpoint with the given ID.
+Parameters
+
+No parameters.
+Returns
+
+Returns a webhook endpoint if a valid webhook endpoint ID was provided. Raises an error otherwise.
+GET 
+/v1/webhook_endpoints/:id
+Server-side language
+
+import stripe
+stripe.api_key = "sk_test_51OR5eP...OF00CdDfT6Xqsk_test_51OR5ePGF83d3fsgWlh41IbGHGtqdiPuFhrcWczglEeFJvQxajyQVCQiZYVZz62HOuYL9tA8dxEQ2MRbxbcYsf8OF00CdDfT6Xq"
+stripe.WebhookEndpoint.retrieve("we_1Mr5jULkdIwHu7ix1ibLTM0x")
+RESPONSE
+{
+  "id": "we_1Mr5jULkdIwHu7ix1ibLTM0x",
+  "object": "webhook_endpoint",
+  "api_version": null,
+  "application": null,
+  "created": 1680122196,
+  "description": null,
+  "enabled_events": [
+    "charge.succeeded",
+    "charge.failed"
+  ],
+  "livemode": false,
+  "metadata": {},
+  "status": "enabled",
+  "url": "https://example.com/my/webhook/endpoint"
+}
+List all webhook endpoints
+
+Returns a list of your webhook endpoints.
+Parameters
+
+No parameters.
+More parameters
+Expand all
+
+
+ending_before
+string
+
+limit
+integer
+
+starting_after
+string
+Returns
+
+A dictionary with a data property that contains an array of up to limit webhook endpoints, starting after webhook endpoint starting_after. Each entry in the array is a separate webhook endpoint object. If no more webhook endpoints are available, the resulting array will be empty. This request should never raise an error.
+GET 
+/v1/webhook_endpoints
+Server-side language
+
+import stripe
+stripe.api_key = "sk_test_51OR5eP...OF00CdDfT6Xqsk_test_51OR5ePGF83d3fsgWlh41IbGHGtqdiPuFhrcWczglEeFJvQxajyQVCQiZYVZz62HOuYL9tA8dxEQ2MRbxbcYsf8OF00CdDfT6Xq"
+stripe.WebhookEndpoint.list(limit=3)
+RESPONSE
+{
+  "object": "list",
+  "url": "/v1/webhook_endpoints",
+  "has_more": false,
+  "data": [
+    {
+      "id": "we_1Mr5jULkdIwHu7ix1ibLTM0x",
+      "object": "webhook_endpoint",
+      "api_version": null,
+      "application": null,
+      "created": 1680122196,
+      "description": null,
+      "enabled_events": [
+        "charge.succeeded",
+        "charge.failed"
+      ],
+      "livemode": false,
+      "metadata": {},
+      "status": "enabled",
+      "url": "https://example.com/my/webhook/endpoint"
+    }
+    {...}
+    {...}
+  ],
+}
+
+curl https://api.stripe.com/v1/balance \
+  -u "{{sk_test_51OR5ePGF83d3fsgWlh41IbGHGtqdiPuFhrcWczglEeFJvQxajyQVCQiZYVZz62HOuYL9tA8dxEQ2MRbxbcYsf8OF00CdDfT6Xq}}" \
+  -H "Stripe-Account: {{CONNECTED_ACCOUNT_ID}}" \
+  -d "expand[]"="instant_available.net_available"# Or find the Stripe package on http://pypi.python.org/pypi/stripe/
+requirements.txt
+Python
+# Set your secret key. Remember to switch to your live secret key in production.
+# See your keys here: https://dashboard.stripe.com/apikeys
+import stripe
+stripe.api_key = "sk_test_51OR5ePGF83d3fsgWlh41IbGHGtqdiPuFhrcWczglEeFJvQxajyQVCQiZYVZz62HOuYL9tA8dxEQ2MRbxbcYsf8OF00CdDfT6Xq"
+
+stripe.Account.modify(
+  "{{CONNECTED_ACCOUNT_ID}}",
+  settings={"payouts": {"schedule": {"interval": "manual"}}},
+)
+curl https://api.stripe.com/v1/balance \
+  -u "{{sk_test_51OR5ePGF83d3fsgWlh41IbGHGtqdiPuFhrcWczglEeFJvQxajyQVCQiZYVZz62HOuYL9tA8dxEQ2MRbxbcYsf8OF00CdDfT6Xq}}" \
+  -H "Stripe-Account: {{CONNECTED_ACCOUNT_ID}}" \
+  -d "expand[]"="instant_available.net_available"
+
+
+# Find the version you want to pin:
+# https://github.com/stripe/stripe-python/blob/master/CHANGELOG.md
+# Specify that version in your requirements.txt file
+stripe>=5.0.0import stripe
+stripe.api_key = "sk_test_51OR5eP...OF00CdDfT6Xqsk_test_51OR5ePGF83d3fsgWlh41IbGHGtqdiPuFhrcWczglEeFJvQxajyQVCQiZYVZz62HOuYL9tA8dxEQ2MRbxbcYsf8OF00CdDfT6Xq"
 stripe.Token.create(
   account={
     "individual": {"first_name": "Jane", "last_name": "Doe"},
