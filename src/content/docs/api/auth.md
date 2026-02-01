---
title: API Authentication
description: How to authenticate with ClawFi API
---

# API Authentication

Most ClawFi functionality works without authentication using public APIs (Dexscreener, GoPlus). Premium features require an API key.

## Public Access (No Auth)

These features work without an API key:

- ✅ Market data (via Dexscreener)
- ✅ Token search
- ✅ Trending tokens
- ✅ Security checks (via GoPlus)
- ✅ Honeypot detection
- ✅ Basic signals

## Premium Features (API Key Required)

- 🔐 Historical data
- 🔐 Webhook subscriptions
- 🔐 Watchlist sync
- 🔐 Custom alerts
- 🔐 Higher rate limits
- 🔐 Priority support

## Getting an API Key

API keys are available through:

1. **ClawFi Dashboard** - Sign up at clawfi.ai
2. **Contact** - team@clawfi.ai

## Using the API Key

### With SDK

```typescript
import { ClawFi } from '@clawfi/sdk';

const clawfi = new ClawFi({
  apiKey: 'your-api-key-here',
});
```

### With HTTP Requests

Include the key in the Authorization header:

```bash
curl -H "Authorization: Bearer YOUR_API_KEY" \
  https://api.clawfi.ai/analyze/ethereum/0x...
```

### In Extension

1. Open extension popup
2. Click settings icon
3. Enter API key in the field
4. Click Save

## Rate Limits

| Tier | Requests/min | Features |
|------|--------------|----------|
| Public | 100 | Basic features |
| Free | 500 | + Watchlist |
| Pro | 2000 | + Webhooks, History |
| Enterprise | Unlimited | + Priority, SLA |

## Security Best Practices

- ✅ Never commit API keys to git
- ✅ Use environment variables
- ✅ Rotate keys periodically
- ✅ Use separate keys for dev/prod

```typescript
// Good - from environment
const clawfi = new ClawFi({
  apiKey: process.env.CLAWFI_API_KEY,
});

// Bad - hardcoded
const clawfi = new ClawFi({
  apiKey: 'sk_live_abc123...',  // Don't do this!
});
```

## Fallback Mode

The SDK automatically falls back to public APIs if:
- No API key provided
- API key is invalid
- ClawFi API is unavailable

This ensures basic functionality always works.
