---
description: Manage Allowed Origins for your DataHub Apps to prevent CORS errors
---

# Configuring CORS whitelist

## What is CORS?

**Cross-Origin Resource Sharing (**[**CORS**](https://developer.mozilla.org/en-US/docs/Glossary/CORS)**)** is an HTTP-header-based mechanism that allows a server to indicate any other [_origin_](https://developer.mozilla.org/en-US/docs/Glossary/Origin) (domain, scheme, or port) than its own from which a browser should permit the loading of resources.&#x20;

#### Allowed Origins

Access-Control-Allow-Origin headers, _Allowed Origins,_ could have one or many domain addresses that you may whitelist in DataHub to comply with the default CORS policy: you need to whitelist all domains that could be a part of a cross-origin request.

#### CORS request example

An example of a cross-origin request: the front-end JavaScript code served from `https://domain-a.com` uses XMLHttpRequest to make a request for `https://domain-b.com/data.json`. For security reasons, browsers restrict cross-origin HTTP requests initiated from scripts.&#x20;

#### CORS error example

CORS Errors are common when you’re working with APIs and it’s important to handle them effectively due to security reasons.

```shell
Access to fetch at 'https://solana--mainnet--rpc.datahub.figment.io/' 
from origin 'http://localhost:3000' has been blocked by CORS policy: 
Response to preflight request doesn't pass access control check: No 
'Access-Control-Allow-Origin' header is present on the requested 
resource. If an opaque response serves your needs, set the request's 
mode to 'no-cors' to fetch the resource with CORS disabled.
```

## **Add Allowed Origin**

1. Navigate to your App settings.
2. In the Allowed Origins section, add a domain address, that includes protocol, hostname, and optionally port. Example: `http://localhost:9000` or `wss://uniswap.org`
3. Click Save and save your changes to the Allowed Origins list. If you see errors upon saving you need to fix them first and click Save to revalidate and save.

## **Delete Allowed Origin**

1. Navigate to your App settings.
2. In the Allowed Origins section, delete a domain address.
3. Click Save and save your changes to the Allowed Origins list.&#x20;
