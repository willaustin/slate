---
title: API Reference

language_tabs:
  - php
  - shell

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='http://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction method

Welcome to the Xpress Bill Pay API!

We have language bindings in Shell and PHP. You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# Wallet

## Payment method object

> An example payment method

```json
    {
        "wallet_id": "4",
        "wallet_name": "My Visa",
        "cust_id": "1",
        "entity_id": "0",
        "pay_method_id": "1",
        "business": 0,
        "cc_first_six": "411111",
        "cc_last_four": "1111",
        "cc_exp_month": 11,
        "cc_exp_year": 2016,
        "b_fname": "Test",
        "b_lname": "Tester",
        "b_address": "Any Street",
        "b_city": "Any City",
        "b_state": "ST",
        "b_zip": "12345",
        "b_phone": "555-555-5555",
        "b_email": "test@test.com",
        "last_edit": "2015-04-01 14:44:40",
        "date_added": "2015-03-30 13:41:22"
    }
```

### Limiting returned fields

<aside class="notice">
The fields that are returned may be limited by passing a comma separated string as the value of the 'fields' parameter. e.g. ?fields=field1,field2 (which would then return only 'field1' and 'field2').
</aside>

Property Name | Description | Type
------------- | ----------- | ----
wallet_id | The id of the wallet | numeric string
wallet_name | The name of the wallet | string
cust_id | The customer id who owns the wallet | numeric string
entity_id | The entity id (if the wallet has been setup by and admin) | numeric string
pay_method_id | The payment method id which determines what type of card<br>(Visa, Discover, etc.) it is or whether it is a checking or savings account | numeric string
business | If the wallet contains bank account information this determines whether the account is a personal or business account | boolean (as 0 or 1)
cc_first_six | The first six un-encrypted numbers of the credit card | numeric string
cc_last_four | The last four un-encrypted numbers of the credit card | numeric string
cc_exp_month | The credit card expiration month | int (numeric month without leading zero)
cc_exp_year | The credit card expiration year | int (numeric four digit year)
b_fname | The billing first name | string
b_lname | The billing last name | string
b_address | The billing address | string
b_city | The billing city | string
b_state | The billing state | string
b_zip | The billing zip | string
b_phone | The billing phone | string
b_email | The billing email | string
last_edit | The timestamp of the last edit | MySQL datetime
date_added | The timestamp of when the wallet was added | MySQL datetime

### Including extra fields

<aside class="notice">
Extra fields may be included by passing any or all of the following fields as a comma separated string as the value of the 'expand' parameter. e.g. ?expand=field1,field2,field3
</aside>

> payment_info card type

```json
    {
        "type": "card",
        "lastFourCard": "4444",
        "expMonth": 12,
        "expYear": 2016
    }
```

> payment_info bank type

```json
    {
        "type": "bank",
        "bankName": "First Bank of XBP",
        "checkingOrSavings": "CHECKING",
        "lastThreeRouting": "820",
        "lastFourAccount": "4333"
    }
```

Property Name | Description | Type
------------- | ----------- | ----
full_name | The combined first `b_fname` and last `b_lname` billing name | string
payment_info | An array containing the payment info specifying the type of wallet and relevant information (see adjacent JSON sample) | array

## View all payment methods

> Request

```php
    <?php
    require 'XpressBillPay.php';
    $xbp = new XpressBillPay();
    /* Authentication code here */

    $wallets = $xbp->api('/wallets');
```

```shell
    curl "https://api.xpressbillpay.com/v1/wallets"
      -H "Authorization: Bearer <access_token>"
```

> Response

```json
    {
        "items": [
            {
                "wallet_id": "4",
                "wallet_name": "My Visa",
                "cust_id": "1",
                "entity_id": "0",
                "pay_method_id": "1",
                "business": 0,
                "cc_first_six": "411111",
                "cc_last_four": "1111",
                "cc_exp_month": 11,
                "cc_exp_year": 2016,
                "b_fname": "Test",
                "b_lname": "Tester",
                "b_address": "Any Street",
                "b_city": "Any City",
                "b_state": "ST",
                "b_zip": "12345",
                "b_phone": "555-555-5555",
                "b_email": "test@test.com",
                "last_edit": "2015-04-01 14:44:40",
                "date_added": "2015-03-30 13:41:22"
            }
        ],
        "_links": {
            "self": {
                "href": "https://api.xpressbillpay.com/v1/wallets?page=1"
            }
        },
        "_meta": {
            "totalCount": 5,
            "pageCount": 1,
            "currentPage": 1,
            "perPage": 20
        }
    }
```

This endpoint retrieves all payment methods for the logged in user.

### HTTP Request

`GET https://api.xpressbillpay.com/v1/wallets`

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/3"
  -H "Authorization: meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Isis",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">If you're not using an administrator API key, note that some kittens will return 403 Forbidden if they are hidden for admins only.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the cat to retrieve

