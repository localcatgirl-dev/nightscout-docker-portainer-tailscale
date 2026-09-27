https
```bash
   tailscale serve --bg http://127.0.0.1:1337
   tailscale serve status -json > /config/serve.json
```

http
```bash
tailscale serve --bg --http=80 http://127.0.0.1:1337
tailscale serve status -json > /config/serve.json
```