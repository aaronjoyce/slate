---
title: API Reference

language_tabs:
  - shell

toc_footers:
  - <a href='https://www.traitly.com/register/'>Sign Up for an account and API token</a>

includes:
  - errors

search: true
---

# Introduction

The Traitly API is a RESTful Web service. You can use the API to access Traitly endpoints, which allow you to create, retrieve and update customer data stored on the [Traitly Platform](https://traitly.com).

We offer you the ability to make CURL requests, which are language-agnostic. We will offer client bindings for popular languages in the future.

# Authentication

> Authentication information must be passed with all API requests. A bearer token is passed as part of the request header. You must be registered and logged in to view your API credentials. You will find your token at our API credentials portal.


```shell
# Don't forget to pass the application/json
# in the Content-Type header
curl https://api.traitly.com/api/v1/<end-point>"
  -H "Authorization: Token <insert-token-here>"
  -H "Content-Type: application/json"
```

> Make sure to replace `insert-token-here` with your API key.

The Traitly API uses account-level API keys to allow access to the API. You can access your Traitly API key following account creation [developer portal](https://www.traitly.com/apps/data-sources/get_traitly/).

Traitly expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: Token insert-token-here`

# Events

## Create an Event

```shell
curl "https://api.traitly.com/api/v1/event"
    --request POST
    --data '{"customer_id": "15", "name": "Customer C",
            "monthly_payment_amount": 99,
            "location": "New York", "plan": "Atom",
            "email": "support@company.com"
            }'
    -H "Authorization: Token <insert-token-here>"
```


> The above command returns JSON structured like this:

```json
{
    "data": [
        {
            "customer_id": "1",
            "name": "Logged in",
            "created_at": "1493933699",
            "success": 1
        },
        {
            "customer_id": "1",
            "name": "Logged in",
            "created_at": "1494020099",
            "success": 1
        }
    ],
    "metadata": {},
    "created": "1500019594",
    "object": "event"
}
```

This endpoint is used to create a tracked event inside Traitly.

### HTTP POST Request

`POST https://api.traitly.com/api/event`

### POST Parameters

Parameter | Default | Required | Description
--------- | ------- | -------- | -----------
customer_id | None | Yes| Your identifier for the customer.
name | None | Yes | Name of the event being created, e.g., "added user".
created_at | Current UNIX timestamp | No | Time at which the event occurred. Measured in seconds since the Unix epoch. Defaults to the current Unix timestamp.


## List Events

```shell
curl "https://api.traitly.com/api/v1/event"
    --request GET
    -H "Authorization: Token <insert-token-here>"
    -H "Content-Type: application/json"
```

> The above command returns JSON structured like this:

```json
{
    "data": [
        {
            "customer_id": "1",
            "name": "Logged in",
            "created_at": "1493933699",
            "success": 1
        },{
            "customer_id": "1",
            "name": "Logged in",
            "created_at": "1494020099",
            "success": 1
        }
    ],
    "metadata": {},
    "retrieved": "1500019594",
    "object": "event"
}
```

This endpoint retrieves a list of events.

<aside class="success">
 Remember — pass the authentication header as part of your request, as well as the correct content type: application/json
</aside>
### HTTP Request

`GET https://api.traitly.com/api/v1/event`

### URL Parameters

Parameter | Required | Description
--------- | ------- | -------- |
customer_id | Yes | Your identifier for the customer.
name | Yes | Name of the event being retrieved, e.g., "added user".


# Customers

## Create a Customer

```shell
curl "https://api.traitly.com/api/v1/customer"
    --request POST
    --data '{"customer_id": "123", "name": "John Smith",
            "monthly_payment_amount": 199,
            "location": "San Francisco", "plan": "Starter",
            "email": "john.smith@example.com"
            }'
    -H "Authorization: Token <insert-token-here>"
```

> The above command returns JSON structured like this:

```json
{
    "data": [
        {
            "customer_id": "123",
            "name": "John Smith",
            "created_at": "1493933699",
            "monthly_payment_amount": 199,
            "location": "San Francisco",
            "email": "john.smith@example.com",
            "phone_number": "0123456789",
            "organisation_id": null,
            "plan": "Starter",
            "custom_attributes": {"role": "manager", "account_type": "admin"}
        },
    ],
    "metadata": {},
    "created": "1500019594",
    "object": "customer"
}
```

This endpoint is used to create a tracked event inside Traitly.

### HTTP POST Request

`POST https://api.traitly.com/api/v1/customer`

### POST Parameters


Parameter | Default | Required | Description
--------- | ------- | -------- | -----------
customer_id | None | Yes| Your identifier for the customer.
name | None | Yes | Name of the customer being created, e.g., "John Smith".
email | None | Yes | Email address of the customer being created, e.g., "john.smith@example.com".
plan | None | Yes | This is the name of the plan the user is assigned to, e.g, "Starter"
created_at | Current UNIX timestamp | No | Time at which the customer signed up. Measured in seconds since the UNIX epoch. Defaults to the current UNIX timestamp.
custom_attributes | object | No | A hash of key-value pairs containing any other data about the customer you want Traitly to store.

## List Customers

```shell
curl "https://api.traitly.com/api/v1/customer"
    --request GET
    -H "Authorization: Token <insert-token-here>"
    -H "Content-Type: application/json"
```

> The above command returns JSON structured like this:

```json
{
    "data": [
        {
            "customer_id": "123",
            "name": "John Smith",
            "created_at": "1493933699",
            "monthly_payment_amount": 199,
            "location": "San Francisco",
            "email": "john.smith@example.com",
            "phone_number": "0123456789",
            "organisation_id": null,
            "plan": "Starter",
            "custom_attributes": {"role": "manager", "account_type": "admin"}
        },
        {
            "customer_id": "456",
            "name": "Alice Smith",
            "created_at": "1533933699",
            "monthly_payment_amount": 0,
            "location": "Berlin",
            "email": "alice.smith@example.com",
            "phone_number": "0123456789",
            "organisation_id": null,
            "plan": "Freemium",
            "custom_attributes": {"role": "cashier", "account_type": "sub-user"}
        },
    ],
    "metadata": {},
    "retrieved": "1500019594",
    "object": "customer"
}
```

This endpoint retrieves a list of customers.

<aside class="success">
 Remember — pass the authentication header as part of your request, as well as the correct content type: application/json
</aside>

### HTTP Request

`GET https://api.traitly.com/api/v1/customer`

### URL Parameters

Parameter | Required | Description
--------- | ------- | -------- |
customer_id | No | Your identifier for the customer.
name | No | Name of the customer being retrieved, e.g., "John Smith".
plan | No | Name of the plan a customer is assigned to, e.g., "Starter".






# Goal Predictions

## Webhook: Recommended Next Actions

> A JSON structure like this is sent to the prescribed endpoint:

```json
{
"data": [{
    "event_name": "Style Widget",
    "goal_num_completed": 0,
    "total_num_completed": 4,
    "goal_days_left": 14,
    "importance": 0.4,
    "message_plaintext":"It's time to complete...",
    "message_html":"<p>It's time to complete...</p>"
}],
"meta": {"customer_id": "123456", "goal_name": "30-day Conversion"},
"timestamp":123456789,
"object":"recommended-next-actions"
}
```

This endpoint can be used to power third-party (e.g., in-house) targeting systems.

### HTTP POST Request

### POST data model

Parameter | Type | Description
--------- | ------- | -------- | -----------
event_name | String | Name of the recommended event
goal_num_completed | Integer | The number of times the Customer has completed the event during the goal window
total_num_completed | Integer | The number of times the Customer has completed the event all-time
goal_days_left | Integer | The maximum number of days for which the Customer will be assigned to the goal
importance | Float | This represents the importance of the user to perform the event as their next optimal course of action. This is relative to other events in the data payload
message_plaintext | String | Plaintext representation of the event message specified for the event
message_html | String | HTML representation of the event message specified for the event

### POST header values

Key | Value
--------- | -------
User-Agent | traitly
Accept | application/json
Content-Type | application/json



## Webhook: Goal Propensity Change

> A JSON structure like this is sent to the prescribed endpoint:

```json
{
"data": [{
    "likelihood": 0.5
}],
"meta": {"customer_id": "123456", "goal_name": "30-day Conversion"},
"timestamp":123456789,
"object":"goal-propensity-change"
}
```

This endpoint can be used to power third-party (e.g., in-house) targeting systems.

### HTTP POST Request

### POST data model

Parameter | Type | Description
--------- | ------- | -------- | -----------
likelihood | Float | This represents the propensity of a Customer to achieve a goal, e.g., likelihood to convert


### POST meta model

Parameter | Default | Required | Description
--------- | ------- | -------- | -----------
customer_id | String | Your identifier for the Customer.
goal_name | String | Name of the goal the prediction relates to, e.g., "Conversion".



### POST header values

Key | Value
--------- | -------
User-Agent | traitly
Accept | application/json
Content-Type | application/json



## Lookup: Recommended Next Actions

```shell
curl "https://api.traitly.com/api/v1/recommended-next-action"
    --request GET
    -H "Authorization: Token <insert-token-here>"
    -H "Content-Type: application/json"
```

> The above command returns JSON structured like this:

```json
{
"data": [{
    "event_name": "Style Widget",
    "goal_num_completed": 0,
    "total_num_completed": 4,
    "goal_days_left": 14,
    "importance": 0.4,
    "message_plaintext":"It's time to complete...",
    "message_html":"<p>It's time to complete...</p>"
}],
"likelihood": 0.5,
"meta": {"customer_id": "123456", "goal_name": "30-day Conversion"},
"timestamp":123456789,
"object":"recommended-next-actions"
}
```

This endpoint retrieves recommended next actions and goal completion propensity for a Customer.

<aside class="success">
 Remember — pass the authentication header as part of your request, as well as the correct content type: application/json
</aside>
### HTTP Request

`GET https://api.traitly.com/api/v1/recommended-next-actions`

### URL Parameters

Parameter | Required | Description
--------- | ------- | -------- |
customer_id | Yes | Your identifier for the Customer.
goal_name | No | Name of the Goal the Customer is assigned to.
