# InitiatePayment

`RESTful Endpoint: POST /assets/asset-accounts/{assetAccountId}/payments`

Initiates payment in provided `AssetSymbol`, instructing funds to be transfered from one wallet to another within same network and same asset.

> **Note**: InitiatePayment triggers PolicyEngine.

To initiate a payment to an asset account, send a `POST` request to the endpoint. Incldue an asset account identifier as a path parameter, and in the request body send the amount and type of funds as well as the receiver's kind and address:

```http
POST /assets/asset-accounts/:assetAccountId/payments
```

```json
{
    "receiver": 
    {
        "kind": "BlockchainWalletAddress",
        "address": "0x...."
    }
    "assetSymbol":  "ETH",
    "amount": "0.0001"
}
```

If successful, the response contains, among other things, a **date stamp** and a **new payment ID**, confirming that a new payment of the correct **amount** and **type** is being **initiated**:

```json
{ 
    "status": "Initiated",
    "assetSymbol": "ETH",
    "id": pa-five-blue-caab30165c"
    "dateCreated": "2022-06-20t09:45:15.017Z"
}
```

When the payment is in the process of being initiated, its `status` is `Initiated`. Once complete, the payment's `status` changes from `Initiated` to `Executed`. To confirm that this has occurred, you can use the [`GetPaymentById` method](GetPaymentById.md).

## Input Query Parameters

* Path parameter `assetAccountId`: `String`.

## Input Body Parameters

* externalId: `String` \[_Optional_]
* assetSymbol: `AssetSymbol`
* amount: `Amount`
* receiver: `PaymentInstrument`
* note: `String` \[_Optional_]
* narrative: `String` \[_Optional_]

_Please consult OpenAPI file full breakdown and including nested properties._

__

{% swagger src="../../.gitbook/assets/production-dfns-api-openapi.json" path="/assets/asset-accounts/{assetAccountId}/payments" method="post" %}
[production-dfns-api-openapi.json](../../.gitbook/assets/production-dfns-api-openapi.json)
{% endswagger %}
