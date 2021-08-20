---
description: Learn how to use the Rewards API on Cosmos
---

# Rewards API

Test out our Rewards API today with [**DataHub**](https://datahub.figment.io/sign_up?service=cosmos)!

{% api-method method="get" host="https://cosmos--search.datahub.figment.io/rewards" path=" " %}
{% api-method-summary %}
rewards
{% endapi-method-summary %}

{% api-method-description %}
Rewards enpoint allows users to query daily reward summaries for an account.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="network" type="string" required=true %}
Network identifier \(eg. `cosmos`\)
{% endapi-method-parameter %}

{% api-method-parameter name="chain\_id" type="string" required=true %}
The chain id \(eg. `cosmoshub-4`\)
{% endapi-method-parameter %}

{% api-method-parameter name="account" type="string" required=true %}
The account identifier
{% endapi-method-parameter %}

{% api-method-parameter name="start\_time" type="string" required=true %}
The start time in UTC. Daily reward summaries will be calculated in 24 hour periods from the start time.
{% endapi-method-parameter %}

{% api-method-parameter name="end\_time" type="string" required=true %}
The end time in UTC.
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Success response
{% endapi-method-response-example-description %}

```javascript
[
    {
    "start": 3997443,
    "end": 4009234,
    "time": "2020-11-08T02:00:00Z",
    "validator": "cosmosvaloper1lzhlnpahvznwfv4jmay2tgaha5kmz5qxerarrl",
    "rewards": [{
        "text": "14485183.076655587945uatom",
        "currency": "uatom",
        "numeric": 14485183076655587945173239,
        "exp": 18
    }]
    }
]
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=400 %}
{% api-method-response-example-description %}
Bad parameters sent
{% endapi-method-response-example-description %}

```javascript
{
  "error": "Bad parameters sent"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=500 %}
{% api-method-response-example-description %}
Internal/Other server error while processing request
{% endapi-method-response-example-description %}

```javascript
{
  "error": "Something bad happened" 
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

## Example Request

```http
/rewards?network=cosmos&start_time=2021-04-01T02:00:00.00Z&chain_id=cosmoshub-4&end_time=2021-04-05T02:00:00.00Z&account=cosmos13axkauxjxulmvjyskppf8kxec56fyl96njm8qq&validators=cosmosvaloper1lzhlnpahvznwfv4jmay2tgaha5kmz5qxerarrl
```

## Example Response

```javascript
[{
  "start": 5699521,
  "end": 5711391,
  "time": "2021-04-01T02:00:00Z",
  "validator": "cosmosvaloper1lzhlnpahvznwfv4jmay2tgaha5kmz5qxerarrl",
  "rewards": [{
    "text": "14485183.076655587945uatom",
    "currency": "uatom",
    "numeric": 14485183076655587945173239,
    "exp": 18
  }]
}, {
  "start": 5711391,
  "end": 5723284,
  "time": "2021-04-02T02:00:00Z",
  "validator": "cosmosvaloper1lzhlnpahvznwfv4jmay2tgaha5kmz5qxerarrl",
  "rewards": [{
    "text": "14524615.642913129133uatom",
    "currency": "uatom",
    "numeric": 14524615642913129133835499,
    "exp": 18
  }]
}, {
  "start": 5723284,
  "end": 5735178,
  "time": "2021-04-03T02:00:00Z",
  "validator": "cosmosvaloper1lzhlnpahvznwfv4jmay2tgaha5kmz5qxerarrl",
  "rewards": [{
    "text": "14554430.583334477875uatom",
    "currency": "uatom",
    "numeric": 14554430583334477874950230,
    "exp": 18
  }]
}, {
  "start": 5735178,
  "end": 5747087,
  "time": "2021-04-04T02:00:00Z",
  "validator": "cosmosvaloper1lzhlnpahvznwfv4jmay2tgaha5kmz5qxerarrl",
  "rewards": [{
    "text": "14582108.999563571208uatom",
    "currency": "uatom",
    "numeric": 14582108999563571207321173,
    "exp": 18
  }]
}]
```

If you need help with this API or simply want to share with other builders, you can [**join our community today**](https://discord.gg/fszyM7K)!

