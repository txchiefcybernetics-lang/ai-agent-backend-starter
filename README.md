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
  -d '{"message": "What is tradexpress.me?"}'
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

export const tx = {
  auth: {
    validateSubkey: async (serviceToken: string) => {
      const response = await fetch('https://subkey.tradexpress.co/api/auth/verify', {
        method: 'POST',
        headers: { 
          'Content-Type': 'application/json',
          'X-Subkey-Token': serviceToken 
        }
      });
      return response.json();
    }
  }
};
