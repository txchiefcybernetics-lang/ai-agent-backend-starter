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

// tx object implementation with input configuration for tradexpress.co
export const tx = {
  input: {
    sessionKey: "",
    message: ""
  },
  chat: {
    sendMessage: async function() {
      const response = await fetch('https://api.tradexpress.co/api/chat', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ 
          message: this.input.message, 
          sessionKey: this.input.sessionKey 
        })
      });
      return response.json();
    }
  }
};

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
git commit -m 'Update TradeXpress core routing and proxy config'
git push origin main
```

You can also open your app in the [Cloud Dashboard](https://app.encore.dev) to integrate with GitHub, or connect your AWS/GCP account, enabling Encore to automatically handle cloud deployments for you.

## Testing

```bash
encore test ./...
```
