# Sales-Engineer-Test

For the test I used Postman to built all the payment flow. In the next part of this document, we can se all points of the test. Also we can found the .json file, where is the source code of the queries built previously. 



## Payment flow:
### Global variables:
- app_id: com.test.test_alfa-bank
- private_key: c02fbcf5-211c-43a1-901b-4a3428caace4
- public_key: 307cb8ba-8e60-486f-8cc4-5ffb298b64d4
- x-payments-os-env:  test
- token: token
- paymentid: 8827b552-87ac-4639-a417-62d35487424f
### 1. Create a token:
- Link: https://api.paymentsos.com/tokens
- Headers:
```
app_id:{{app_id}}
public_key:{{public_key}}
Content-Type:application/json
api-version:1.3.0
x-payments-os-env:{{x-payments-os-env}}
x-client-user-agent:123
```
- Body:
```
{
  "token_type": "credit_card",
  "credit_card_cvv": "123",
  "card_number": "4111111111111111",
  "expiration_date": "10/29",
  "holder_name": "John Mark",
  "billing_address": {
    "country": "USA",
    "state": "NY",
    "city": "NYC",
    "line1": "fifth avenue 10th"
  }
}
```

### 2. Create Payment 
- Link: https://api.paymentsos.com/payments
- Headers:
```
app_id:{{app_id}}
private_key:{{private_key}}
Content-Type:application/json
api-version:1.3.0
x-payments-os-env:{{x-payments-os-env}}
```
- Body:
```
{
  "amount": 5000,
  "currency": "USD",
  "order": {
    "id": "myorderid"
  }
} 
```
### 3. Create Authorization
- Link: https://api.paymentsos.com/payments
- Headers:
```
app_id:{{app_id}}
private_key:{{private_key}}
Content-Type:application/json
api-version:1.3.0
x-payments-os-env:test
idempotency_key:asd
x-client-user-agent:123
```
- Body:
```
{
    "payment_method": {
        "credit_card_cvv": "123",
        "token": {{token}},
        "type": "tokenized"
    },
    "reconciliation_id": "40762342"
}
```

## Technical definitions:

## Conclusion:
