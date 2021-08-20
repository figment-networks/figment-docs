# 1. Connect to the Solana Devnet

## Connecting with `@solana/web3.js`

In the following tutorials, we're going to interact with the Solana blockchain \(and in particular its Devnet network\) using the `@solana/web3.js` library. It's a convenient way to interface with the RPC API when building a Javascript application \(under the hood it implements Solana's RPC methods and exposes them as Javascript objects\). The documentation for the library is [here](https://solana-labs.github.io/solana-web3.js/). We will explore it together as we add features to our app.

The first thing we need to do is connect to the Solana blockchain. The JS library exposes a class for this named... [Connection](https://solana-labs.github.io/solana-web3.js/classes/Connection.html). It has a constructor that will return an `connection` instance, on which you can call a looong list of methods \(they're on the right sidebar of the previous link\).

{% embed url="https://youtu.be/57A1BlLktcI?list=PLkgTdjgP1aUAiqqbvVi3b0sSdxByd5KSX" caption="Connect to the Solana Devnet Cluster" %}

## The challenge

{% hint style="info" %}
In `src/components/Connect.jsx`, implement `getConnection` by creating a `Connection` instance and getting the API's version. Render it on the webpage.

**Need some help?** Check out those two links

**→** [**Creating a `Connection` instance**](https://solana-labs.github.io/solana-web3.js/classes/Connection.html#constructor)  
**→** [Getting the API's version](https://solana-labs.github.io/solana-web3.js/classes/Connection.html#getversion)
{% endhint %}

Take a few minutes to figure this out.

You can also[ **join us on Discord**](https://discord.gg/fszyM7K) if you have questions.

Still not sure how to do this? No problem! The solution is below so you don't get stuck.

## The solution

{% tabs %}
{% tab title="Challenge" %}
{% code title="src/components/Connect.jsx" %}
```jsx
const getConnection = () => {
  const url = getNodeRpcURL();

  // Create a connection
  // Get the API version
  // and save it to the component's state
}
```
{% endcode %}
{% endtab %}

{% tab title="Solution" %}
{% code title="src/components/Connect.jsx" %}
```javascript
const getConnection = () => {
  const url = getNodeRpcURL();

  // Create a connection
  const connection = new Connection(url);

  // Get the API version
  connection.getVersion()
    .then(version => {
      // and save it to the component's state  
      setVersion(version);
    })
    .catch(error => console.log(error))
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

**What happened in the code above?**

* We created a `connection` instance of the `Connection` class using the `new` constructor
* We then call `getVersion` on that `connection` instance. The docs state that `connection.getVersion()` returns a Promise so we chain `.then()` and a `.catch()` to respectively handle the case where the promise is fulfilled and rejected.
* If the promise is fulfilled, we get a `version` object back, that we can store in our functional component's local state, using the `setVersion` exposed by the React hook `useState`.

Once you have the code above saved, the webpage should automatically reload \(React's hot reloading!\) and you should see:

![](../../../.gitbook/assets/screen-shot-2021-06-14-at-10.47.58-pm%20%282%29%20%283%29%20%282%29.png)

## Next

We're going to use this `connection` instance every time we need to connect to Solana. We're going to want to move some tokens around but first we need an account to hold tokens. That's what we'll do next!

