# Claude API Proxy (Cloudflare Workers)

This project creates a **secure proxy** for Anthropic's Claude API using **Cloudflare Workers**.
It acts as a backend that can be safely called from front-end environments like **Squarespace**, without exposing your API key.

---

## Features

- Safe Claude API calls from static sites (e.g. Squarespace)
- Serverless, scalable, and fast (runs at the edge)
- Minimal setup, max flexibility

---

## Setup

### 1. Prerequisites

- Node.js & npm
- Cloudflare account
- Install Wrangler:

```bash
npm install -g wrangler
```

---

### 2. Clone & Deploy

```bash
git clone https://github.com/YOUR_USERNAME/claude-wrapper-worker.git
cd claude-wrapper-worker
wrangler login
wrangler secret put ANTHROPIC_API_KEY
wrangler deploy
```

After deployment, you'll get a URL like:

```
https://claude-wrapper.YOUR_NAMESPACE.workers.dev
```

---

## Using in Squarespace

1. Open a **Code Block** or **Code Injection** in your Squarespace site.
2. Paste the following JavaScript:

```html
<script>
async function askClaude(message) {
  const response = await fetch("https://claude-wrapper.YOUR_NAMESPACE.workers.dev", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify({
      messages: [{ role: "user", content: message }]
    })
  });
  const data = await response.json();
  console.log(data);
}
</script>
```

3. You can now call `askClaude("Your question here")` from buttons, forms, etc.

---

## Development Notes

- All logic is in `src/index.js`
- Replace `"claude-2.1"` with `"claude-3"` or other versions as needed
- This project is minimal by design—add auth, logging, or rate limits as needed

---

## Security Tips

- Restrict CORS (`Access-Control-Allow-Origin`) to your own domain
- Use CAPTCHA or tokens if you expose it publicly

---

## License

MIT
