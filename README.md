# Nightscout through Docker and Tailscale

(Only tested on Linux)

## Install

- Install Docker Engine: https://docs.docker.com/engine/install/
- Register at Tailscale: https://tailscale.com
- Install Tailscale: https://tailscale.com/docs/install
- Nightscout documentaion: https://nightscout.github.io/vendors/VPS/docker/

Don't forget about your .env
```.env
MY_API_SECRET=<YOUR API SECRET HERE>
MY_TS_KEY=<YOUR TAILSCALE AUTH KEY HERE>
```
- Choose your API SECRET
- Find your TS_AUTH_KEY: https://tailscale.com/docs/features/access-control/auth-keys

## Generating serve.json
Sadly, this will use your tailscale on host not from container and it's the only way it work for me. I don't know how to fix it.

### https
```bash
tailscale serve --bg http://127.0.0.1:1337
sudo tailscale serve status -json > tailscale-config/serve.json
```

### http
```bash
tailscale serve --bg --http=80 http://127.0.0.1:1337
sudo tailscale serve status -json > tailscale-config/serve.json
```

### How it looks
In  my case it generated like this for example

```json
{
  "TCP": {
    "443": {
      "HTTPS": true
    }
  },
  "Web": {
    "<PLACEHOLDER>.<PLACEHOLDER>.ts.net:443": {
      "Handlers": {
        "/": {
          "Proxy": "http://127.0.0.1:1337"
        }
      }
    }
  }
}
```

Now you can join through tailscale address but only from the host not from the docker container.