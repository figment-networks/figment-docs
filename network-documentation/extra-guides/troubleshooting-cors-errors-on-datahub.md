---
description: Find ready to use proxy to troubleshoot the CORS errors on DataHub
---

# Troubleshooting CORS Errors on DataHub

CORS Errors are common when you’re working with APIs but it’s very important to handle them effectively due to several security reasons.

What does it look like?

```
Access to fetch at 'https://solana--mainnet--rpc.datahub.figment.io/' from origin 'http://localhost:3000' has been blocked by CORS policy: Response to preflight request doesn't pass access control check: No 'Access-Control-Allow-Origin' header is present on the requested resource. If an opaque response serves your needs, set the request's mode to 'no-cors' to fetch the resource with CORS disabled.
```

What it is? - **Cross-Origin Resource Sharing** ([CORS](https://developer.mozilla.org/en-US/docs/Glossary/CORS)) is an [HTTP](https://developer.mozilla.org/en-US/docs/Glossary/HTTP)-header based mechanism that allows a server to indicate any other [origin](https://developer.mozilla.org/en-US/docs/Glossary/Origin) (domain, scheme, or port) than its own from which a browser should permit loading of resources. CORS also relies on a mechanism by which browsers make a “preflight” request to the server hosting the cross-origin resource, in order to check that the server will permit the actual request. In that preflight, the browser sends headers that indicate the HTTP method and headers that will be used in the actual request.

An example of a cross-origin request: the front-end JavaScript code served from `https://domain-a.com` uses [`XMLHttpRequest` ](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest)to make a request for `https://domain-b.com/data.json` .

For security reasons, browsers restrict cross-origin HTTP requests initiated from scripts. For example, `XMLHttpRequest` and the [Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch\_API) follow the [same-origin policy](https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin\_policy). This means that a web application using those APIs can only request resources from the same origin the application was loaded from unless the response from other origins includes the right CORS headers.

![](https://aws1.discourse-cdn.com/standard11/uploads/figment1/optimized/1X/7e4d667009459c52a882b48c29a3bbe39c36db7b\_2\_690x479.png)

The CORS mechanism supports secure cross-origin requests and data transfers between browsers and servers. Modern browsers use CORS in APIs such as `XMLHttpRequest` or [Fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch\_API) to mitigate the risks of cross-origin HTTP requests. _Source -_ [Mozilla MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)

How to handle them when working with Figment’s DataHub?

There are two major ways to handle CORS errors effectively so you don’t expose your API keys and credentials on the Client-Side.

1. **Use a proxy** - One solution for making cross-origin requests is to use a CORS proxy to make it seem as though you’re making the request from a location that’s allowed.

There are multiple [**CORS proxies** ](https://gist.github.com/jimmywarting/ac1be6ea0297c16c477e17f8fbe51347)(Must Check) out there that you can use for free. Some of them are

* [cors-anywhere](https://github.com/Rob--W/cors-anywhere)
* [Crossorigin.me ](http://crossorigin.me)is easy to use — you simply prepend [https://crossorigin.me/ ](https://crossorigin.me)to your request URL (Not Recommended for Production).
* Cloudflare Workers - [CORS header proxy ](https://developers.cloudflare.com/workers/examples/cors-header-proxy)Doc.
  * [CORS Header Proxy Template](https://github.com/cloudflare/template-registry/blob/f2a21ff87a4f9c60ce1d426e9e8d2e6807b786fd/templates/javascript/cors\_header\_proxy.js)
  * [**Cloudflare worker Template by Figment**](https://gist.github.com/ajcronk/d97fc7e5f1f1d9754753b28e8dd187b1)
  * [**Cloudflare worker Template by Figment (Support Websockets)**](https://gist.github.com/mkornatz/d7daca0203260340ffff7e85399a48db)
* [**nginx proxy Template**](https://gist.github.com/mkornatz/24e573923d6340b1aca8487225eb65e2)

1. **Use a serverless function** - Using a serverless function is another more effective way to handle the CORS errors and proxy our requests and here in this we build our own functions or micro-infrastructure to call a web service and interact using APIs. Azure, AWS & GCP are most popular for running serverless functions.\
   Sharing some examples of serverless functions built and shared by our community members.

i. Azure Function for CORS proxy by [Florian Uhde](https://github.com/floAr) - Check the [Gist HERE](https://gist.github.com/floAr/95db6ed96b1b0cf70a0513698a3979f7)

```javascript
const axios = require('axios');
const decode = require('unescape');

module.exports = async function (context, req) {
    var route = decode(context.bindingData.route || req.params.restOfPath);
    let params = req.query
    delete params['code']
    const request = {
        url: 'https://secret-2--lcd--full.datahub.figment.io/apikey/xxxxxxxxxxxxxxxx/' + route,
        method: req.method,
        data: req.rawBody,
        params: params
    }
    const response = await axios(request)
    context.res = {
        body: response.data
    };
}
```

ii. AWS Lambda Function for CORS proxy by [Austin Woetze](https://github.com/AustinWoetzel)- Check the [Gist HERE](https://gist.github.com/AustinWoetzel/da808287f35effd2419ef44ed8593054)

```javascript
const axios = require('axios');

exports.handler = async (event) => {

   const route = event.path
   const request = {
        url: 'https://secret-2--lcd--full.datahub.figment.io/apikey/xxxxxxxxxxxxxxxxxxxxxxxx' + route,
        method: event.httpMethod,
        data:{}
    }
    const response = await axios(request)

    var res = {
        "statusCode": 200,
        "headers": {
            "Access-Control-Allow-Origin":"*"
        },
        "body": (JSON.stringify(response.data)),
        "isBase64Encoded": false
    };
    return res;

};
```

iii. Template if you want to host your own nginx server - [**DataHub CORS Development Proxy**](https://github.com/figment-networks/datahub-cors-dev-proxy)

If you have any other solution for the same feel free to share it with us on our [discord server](https://figment.io/devchat). Thanks in advance, we appreciate your contribution.

_References -_

1. [Mozilla MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)
2. [Big Commoerce Devloper Blog](https://medium.com/bigcommerce-developer-blog/lets-talk-about-cors-84800c726919)
