---
description: Learn what Secret APIs are available via DataHub and how to use them
---

# 🎮 RPC & REST API

## Time to play

Secret exposes both the Tendermint RPC and the Secret REST API which are both necessary for the development of applications on the Secret network.

If you're using secret CLI, configure DataHub RPC endpoints using secret CLI by following these steps -

```bash
# Install a local proxy server
echo "deb [trusted=yes] https://apt.fury.io/caddy/ /" |                                              
        sudo tee -a /etc/apt/sources.list.d/caddy-fury.list &&
        sudo apt-get update &&
        sudo apt-get install -y caddy

# Set its config
echo 'http://localhost:1234
 
reverse_proxy {
        to https://secret-2--rpc--full.datahub.figment.io
        header_up Authorization <YOUR_DATAHUB_API_KEY>
        header_up Host secret-2--rpc--full.datahub.figment.io
}' | sudo tee /etc/caddy/Caddyfile

# Apply the new config
sudo systemctl restart caddy

# Point secretcli to your local proxy
secretcli config node http://localhost:1234

#Note - Just make sure to set <YOUR_DATAHUB_API_KEY> to your API key.
```

Learn about the APIs available via Secret [**DataHub**](https://datahub.figment.io/sign_up?service=secret) below.

{% page-ref page="tendermint-rpc.md" %}

{% page-ref page="secret-rest-api.md" %}

