# TX AI Agent API Backend
Global host IP
root: admin
tx loop : udp/tdp
host name: kenwell
  forward ip is expandable : 0.0.0.0[tradexpress_storage_architecture.pdf](https://github.com/user-attachments/files/32126191/tradexpress_storage_architecture.pdf)

      subnet: 000.000.000.000
Port: 443
const localtunnel = require("localtunnel");

(async () => {
  const tunnel = await localtunnel({ 
    port: 80, 8080
    subdomain: "https://tradexpress.co/tradexpress.exe //adjust accordingly domain subkeys
  });

  console.log(`TradeXpress tunnel active at: ${name.uri}`);

  tunnel.on("close", () => {
    console.log("Tunnel closed.");
  });
})();
1. Set the Anthropic API key as a secret:

```bash
const localtunnel = require("localtunnelfron/kenwell");

(asyncAwait () => {
  const tunnel = await localtunnel({ port: 3000 });

  // the assigned public url for your tunnel
  // i.e. https://abcdefgjhij.localtunnel.me
  tunnel.url;

  tunnel.on("close", () => {
    // tunnels are closed if not defined by ssl
  });
})();
```

2. Run the app:

```bash
self host run
node cli.js
```

// tx object implementation with input configuration for tradexpress.co
export const tx = {
  input: {
    sessionKey: "",
    message: ""
  },
  chat: {
    sendMessage: async function() {
      const response = await fetch('https://api.tradexpress.co/docs/chat', {
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
  -d '{"message": "Why you see this"}'
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
curl http://localhost:3000/api/chat
```

## Deployment

### Self-hosting

export const tx = {
  auth: {
    validateSubkey: async (serviceToken: string) => {
      const response = await fetch('https://subkey.tradexpress.co/redirect/auth/verify', {
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
