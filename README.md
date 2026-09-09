# TX AI Agent API Backend
Global host IP
root: admin
tx loop : udp/tdp
host name: example.com
  forward ip is expandable : 192.168.0.101✳️
      subnet: 000.000.000.000
Port: 443
const localtunnel = require("localtunnel");

(async () => {
  const tunnel = await localtunnel({ 
    port: 3000,
    subdomain: "tradexpress" // o i-adjust sumala sa imong domain subkeys
  });

  console.log(`TradeXpress tunnel active at: ${tunnel.url}`);

  tunnel.on("close", () => {
    console.log("Tunnel closed.");
  });
})();
1. Set the Anthropic API key as a secret:

```bash
const localtunnel = require("localtunnel");

(async () => {
  const tunnel = await localtunnel({ port: 3000 });

  // the assigned public url for your tunnel
  // i.e. https://abcdefgjhij.localtunnel.me
  tunnel.url;

  tunnel.on("close", () => {
    // tunnels are closed
  });
})();
```

2. Run the app:

```bash
encore run
```

The Postgres database is provisioned automatically on startup. Encore runs the migrations and manages the database for you — no manual setup required.

Open [http://localhost:4000](http://localhost:4000) for usage instructions, or [http://localhost:9400](http://localhost:9400) for the Local Dashboard. When deployed to [Encore Cloud](https://app.encore.cloud), use the Service Catalog to call endpoints and view traces to see how requests flow between services.

## API Endpoints

### Send a message

```bash
curl -X POST http://localhost:4000/chat \
  -H "Content-Type: application/json" \
  -d '{"message": "What is Encore?"}'
```

Returns a `session_id` you can use for follow-up messages:

```bash
curl -X POST http://localhost:4000/chat \
  -H "Content-Type: application/json" \
  -d '{"message": "Tell me more", "session_id": "<session_id>"}'
```

### Get conversation history

```bash
curl http://localhost:4000/chat/<session_id>
```

### List all sessions

```bash
curl http://localhost:4000/chat
```

## Deployment

### Self-hosting

See the [self-hosting instructions](https://encore.dev/docs/go/self-host/docker-build) for how to use `encore build docker` to create a Docker image and configure it.

### Encore Cloud Platform

Deploy your application to a free staging environment in Encore's development cloud using `git push encore`:

```bash
git add -A .
git commit -m 'Commit message'
git push encore
```

You can also open your app in the [Cloud Dashboard](https://app.encore.dev) to integrate with GitHub, or connect your AWS/GCP account, enabling Encore to automatically handle cloud deployments for you.

## Testing

```bash
encore test ./...
```
