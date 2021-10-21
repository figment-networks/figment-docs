---
description: Learn how to use the Rewards API on Cosmos
---

# Rewards API

Test out our Rewards API today with [**DataHub**](https://datahub.figment.io/sign\_up?service=cosmos)!

{% swagger baseUrl="https://cosmos--search.datahub.figment.io/rewards" path=" " method="get" summary="rewards" %}
{% swagger-description %}
Rewards enpoint allows users to query daily reward summaries for an account.
{% endswagger-description %}

{% swagger-parameter in="body" name="network" type="string" %}
Network identifier (eg. 

`cosmos`

)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="chain_id" type="string" %}
The chain id (eg. 

`cosmoshub-4`

)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="account" type="string" %}
The account identifier
{% endswagger-parameter %}

{% swagger-parameter in="body" name="start_time" type="string" %}
The start time in UTC. Daily reward summaries will be calculated in 24 hour periods from the start time.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="end_time" type="string" %}
The end time in UTC.
{% endswagger-parameter %}

{% swagger-response status="200" description="Success response" %}
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
{% endswagger-response %}

{% swagger-response status="400" description="Bad parameters sent" %}
```javascript
{
  "error": "Bad parameters sent"
}
```
{% endswagger-response %}

{% swagger-response status="500" description="Internal/Other server error while processing request" %}
```javascript
{
  "error": "Something bad happened" 
}
```
{% endswagger-response %}
{% endswagger %}

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
