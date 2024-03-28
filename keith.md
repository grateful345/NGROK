# Set your secret key. Remember to switch to your live secret key in production.
# See your keys here: https://dashboard.stripe.com/apikeys
import stripe
stripe.api_key = "sk_test_51OR5ePGF83d3fsgWlh41IbGHGtqdiPuFhrcWczglEeFJvQxajyQVCQiZYVZz62HOuYL9tA8dxEQ2MRbxbcYsf8OF00CdDfT6Xq"

stripe.Customer.modify(
  "cus_V9T7vofUbZMqpv",
  source="tok_visa",


import stripe
stripe.api_key = "sk_test_51OR5eP...OF00CdDfT6Xqsk_test_51OR5ePGF83d3fsgWlh41IbGHGtqdiPuFhrcWczglEeFJvQxajyQVCQiZYVZz62HOuYL9tA8dxEQ2MRbxbcYsf8OF00CdDfT6Xq"
stripe.Token.create(
  account={
    "individual": {"first_name": "Jane", "last_name": "Doe"},
    "tos_shown_and_accepted": True,
  },
)
RESPONSE
{
  "id": "ct_1BZ6xr2eZvKYlo2CsSOhuTfi",
  "object": "token",
  "client_ip": "104.198.25.169",
  "created": 1513297331,
  "livemode": false,
  "redaction": null,
  "type": "account",
  "used": false
}
Create a bank account token

Creates a single-use token that represents a bank account’s details. You can use this token with any API method in place of a bank account dictionary. You can only use this token once. To do so, attach it to a Custom account.
Parameters


bank_account
dictionary
The bank account this token will represent.
Show child parameters
More parameters
Expand all


customer
string
Connect only
Returns

Returns the created bank account token if it’s successful. Otherwise, this call raises an error.
POST 
/v1/tokens
Server-side language

import stripe
stripe.api_key = "sk_test_51OR5eP...OF00CdDfT6Xqsk_test_51OR5ePGF83d3fsgWlh41IbGHGtqdiPuFhrcWczglEeFJvQxajyQVCQiZYVZz62HOuYL9tA8dxEQ2MRbxbcYsf8OF00CdDfT6Xq"
stripe.Token.create(
  bank_account={
    "country": "US",
    "currency": "usd",
    "account_holder_name": "Jenny Rosen",
    "account_holder_type": "individual",
    "routing_number": "110000000",
    "account_number": "000123456789",
  },
)
RESPONSE
{
  "id": "tok_1N3T00LkdIwHu7ixt44h1F8k",
  "object": "token",
  "bank_account": {
    "id": "ba_1NWScr2eZvKYlo2C8MgV5Cwn",
    "object": "bank_account",
    "account_holder_name": "Jenny Rosen",
    "account_holder_type": "individual",
    "account_type": null,
    "bank_name": "STRIPE TEST BANK",
    "country": "US",
    "currency": "usd",
    "fingerprint": "1JWtPxqbdX5Gamtz",
    "last4": "6789",
    "routing_number": "110000000",
    "status": "new"
  },
  "client_ip": null,
  "created": 1689981645,
  "livemode": false,
  "redaction": null,
  "type": "bank_account",
  "used": false
}
Create a card token

Creates a single-use token that represents a credit card’s details. You can use this token in place of a credit card dictionary with any API method. You can only use these tokens once by creating a new Charge object or by attaching them to a Customer object.
In most cases, you can use our recommended payments integrations instead of using the API.
Parameters


card
object | string
The card this token will represent. If you also pass in a customer, the card must be the ID of a card belonging to the customer. Otherwise, if you do not pass in a customer, this is a dictionary containing a user’s credit card details, with the options described below.
Show child parameters
Returns

Returns the created card token if it’s successful. Otherwise, this call raises an error.
POST 
/v1/tokens
Server-side language

import stripe
stripe.api_key = "sk_test_51OR5eP...OF00CdDfT6Xqsk_test_51OR5ePGF83d3fsgWlh41IbGHGtqdiPuFhrcWczglEeFJvQxajyQVCQiZYVZz62HOuYL9tA8dxEQ2MRbxbcYsf8OF00CdDfT6Xq"
stripe.Token.create(
  card={
    "number": "4242424242424242",
    "exp_month": "5",
    "exp_year": "2024",
    "cvc": "314",
  },
)
RESPONSE
{
  "id": "tok_1N3T00LkdIwHu7ixt44h1F8k",
  "object": "token",
  "card": {
    "id": "card_1N3T00LkdIwHu7ixRdxpVI1Q",
    "object": "card",
    "address_city": null,
    "address_country": null,
    "address_line1": null,
    "address_line1_check": null,
    "address_line2": null,
    "address_state": null,
    "address_zip": null,
    "address_zip_check": null,
    "brand": "Visa",
    "country": "US",
    "cvc_check": "unchecked",
    "dynamic_last4": null,
    "exp_month": 5,
    "exp_year": 2024,
    "fingerprint": "mToisGZ01V71BCos",
    "funding": "credit",
    "last4": "4242",
    "metadata": {},
    "name": null,
    "tokenization_method": null,
    "wallet": null
  },
  "client_ip": "52.35.78.6",
  "created": 1683071568,
  "livemode": false,
  "type": "card",
  "used": false
}
Create a CVC update token

Creates a single-use token that represents an updated CVC value that you can use for [CVC re-collection] (/docs/payments/accept-a-payment-synchronously#web-recollect-cvc). Use this token when you confirm a card payment or use a saved card on a PaymentIntent with confirmation_method: manual.
For most cases, use our JavaScript library instead of using the API. For a PaymentIntent with confirmation_method: automatic, use our recommended payments integration without tokenizing the CVC value.
Parameters


cvc_update
dictionary
Required
The updated CVC value this token represents.
Show child parameters
Returns

Returns the created CVC update token if it’s successful. Otherwise, this call raises an error.
POST 
/v1/tokens
Server-side language

import stripe
stripe.api_key = "sk_test_51OR5eP...OF00CdDfT6Xqsk_test_51OR5ePGF83d3fsgWlh41IbGHGtqdiPuFhrcWczglEeFJvQxajyQVCQiZYVZz62HOuYL9tA8dxEQ2MRbxbcYsf8OF00CdDfT6Xq"
stripe.Token.create(cvc_update={"cvc": "123"})
RESPONSE
{
  "id": "cvctok_1NkWsu2eZvKYlo2CFDm6ab7X",
  "object": "token",
  "client_ip": null,
  "created": 1693334608,
  "livemode": false,
  "redaction": null,
  "type": "cvc_update",
  "used": false
}
Create a person token

Creates a single-use token that represents the details for a person. Use this when you create or update persons associated with a Connect account. Learn more about account tokens.
You can only create person tokens with your application’s publishable key and in live mode. You can use your application’s secret key to create person tokens only in test mode.
Parameters


person
dictionary
Required
Information for the person this token represents.
Show child parameters
Returns

Returns the created person token if it’s successful. Otherwise, this call raises an error.
POST 
/v1/tokens
Server-side language

import stripe
stripe.api_key = "sk_test_51OR5eP...OF00CdDfT6Xqsk_test_51OR5ePGF83d3fsgWlh41IbGHGtqdiPuFhrcWczglEeFJvQxajyQVCQiZYVZz62HOuYL9tA8dxEQ2MRbxbcYsf8OF00CdDfT6Xq"
stripe.Token.create(
  person={"first_name": "Jane", "last_name": "Doe", "relationship": {"owner": True}},
)
RESPONSE
{
  "id": "cpt_1EDww82eZvKYlo2CsdelTHFu",
  "object": "token",
  "client_ip": "8.21.168.117",
  "created": 1552582904,
  "livemode": false,
  "redaction": null,
  "type": "person",
  "used": false
}
Create a PII token

Creates a single-use token that represents the details of personally identifiable information (PII). You can use this token in place of an id_number or id_number_secondary in Account or Person Update API methods. You can only use a PII token once.
Parameters


pii
dictionary
Required
The PII this token represents.
Show child parameters
Returns

Returns the created PII token if it’s successful. Otherwise, this call raises an error.
POST 
/v1/tokens
Server-side language

import stripe
stripe.api_key = "sk_test_51OR5eP...OF00CdDfT6Xqsk_test_51OR5ePGF83d3fsgWlh41IbGHGtqdiPuFhrcWczglEeFJvQxajyQVCQiZYVZz62HOuYL9tA8dxEQ2MRbxbcYsf8OF00CdDfT6Xq"
stripe.Token.create(pii={"id_number": "000000000"})
RESPONSE
{
  "id": "pii_18PwbX2eZvKYlo2CzRXgwN3J",
  "object": "token",
  "client_ip": "124.123.76.134",
  "created": 1466783547,
  "livemode": false,
  "redaction": null,
  "type": "pii",
  "used": false
}
Retrieve a token

Retrieves the token with the given ID.
Parameters

No parameters.
Returns

Returns a token if you provide a valid ID. Raises an error otherwise.
GET 
/v1/tokens/:id
Server-side language

import stripe
stripe.api_key = "sk_test_51OR5eP...OF00CdDfT6Xqsk_test_51OR5ePGF83d3fsgWlh41IbGHGtqdiPuFhrcWczglEeFJvQxajyQVCQiZYVZz62HOuYL9tA8dxEQ2MRbxbcYsf8OF00CdDfT6Xq"
stripe.Token.retrieve("tok_1N3T00LkdIwHu7ixt44h1F8k")
RESPONSE
{
  "id": "tok_1N3T00LkdIwHu7ixt44h1F8k",
  "object": "token",
  "card": {
    "id": "card_1N3T00LkdIwHu7ixRdxpVI1Q",
    "object": "card",
    "address_city": null,
    "address_country": null,
    "address_line1": null,
    "address_line1_check": null,
    "address_line2": null,
    "address_state": null,
    "address_zip": null,
    "address_zip_check": null,
    "brand": "Visa",
    "country": "US",
    "cvc_check": "unchecked",
    "dynamic_last4": null,
    "exp_month": 5,
    "exp_year": 2024,
    "fingerprint": "mToisGZ01V71BCos",
    "funding": "credit",
    "last4": "4242",
    "metadata": {},
    "name": null,
    "tokenization_method": null,
    "wallet": null
  },
  "client_ip": "52.35.78.6",
  "created": 1683071568,
  "livemode": false,
  "type": "card",

{
  "object": "list",
  "data": [
    {
      "object": "bank_account",
      "available_payout_methods": [
        "standard",
        "instant"
      ],
      ...
    }
  ],
}
select
  id,
  amount,
  fee,
  currency
from balance_transactions -- this table is the canonical record of changes to your Stripe balance
where
  created < data_load_time and
  created >= data_load_time - interval '1' month
order by created desc
limit 10
)
Event data
{
"object": {
"id"
:
"fa_1OiSr4GF83d3fsgWN5I1RQL1"
,
"object"
:
"treasury.financial_account"
,
"active_features": [
"inbound_transfers.ach"
,
"outbound_payments.ach"
,
"outbound_payments.us_domestic_wire"
,
"financial_addresses.aba"
,
"deposit_insurance"
,
"intra_stripe_flows"
,
"outbound_transfers.ach"
,
"outbound_transfers.us_domestic_wire"
,
],
"balance": {
"cash": {
"usd"
:
0
,
},
"inbound_pending": {
"usd"
:
0
,
},
"outbound_pending": {
"usd"
:
0
,
},
},
"country"
:
"US"
,
"created"
:
1707618798
,
"financial_addresses": [
"0": {
"aba": {
"account_holder_name"
:
"God’s Time Travel Corporation "
,
"account_number_last4"
:
"7766"
,
"bank_name"
:
"Stripe Test Bank"
,
"routing_number"
:
"000000001"
,
},
"supported_networks": [
"ach"
,
"us_domestic_wire"
,
],
"type"
:
"aba"
,
},
],
"livemode"
:
false
,
"metadata": {},
"pending_features": [],
"restricted_features": [],
"status"
:
"open"
,
"status_details": {
"closed"
:
null
,
},
"supported_currencies": [
"usd"
,
],
},
"previous_attributes": {
"active_features": [],
"pending_features": [
"inbound_transfers.ach"
,
"outbound_payments.ach"
,
"outbound_payments.us_domestic_wire"
,
"financial_addresses.aba"
,
"deposit_insurance"
,
"intra_stripe_flows"
,
"outbound_transfers.ach"
,
"outbound_transfers.us_domestic_wire"
,
],
},
