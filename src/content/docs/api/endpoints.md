---
title: API Endpoints
description: ClawFi API endpoint reference
---

# API Endpoints

Base URL: `https://api.clawfi.ai`

## Token Analysis

### Analyze Token
```
GET /analyze/:chain/:address
```

Full token analysis including market data, signals, and contract info.

**Response:**
```json
{
  "token": {
    "address": "0x...",
    "chain": "ethereum",
    "name": "Token Name",
    "symbol": "TKN",
    "price": 0.001234,
    "marketCap": 1000000
  },
  "market": {
    "price": 0.001234,
    "priceChange": { "h24": 5.5 },
    "volume": { "h24": 50000 },
    "liquidity": 100000
  },
  "signals": [...],
  "riskScore": 25,
  "timestamp": 1234567890
}
```

### Get Token
```
GET /token/:chain/:address
```

Quick token info only.

## Signals

### Get Token Signals
```
GET /signals/:chain/:address
```

Returns risk signals for a specific token.

### Get Recent Signals
```
GET /signals/recent?limit=50
```

Returns recent signals across all tokens.

### Subscribe to Signals
```
POST /signals/subscribe
```

**Body:**
```json
{
  "webhookUrl": "https://your-server.com/webhook",
  "filters": {
    "chains": ["ethereum", "base"],
    "severity": ["high", "critical"]
  }
}
```

## Market Data

### Get Market Data
```
GET /market/:chain/:address
```

### Get Trending Tokens
```
GET /trending
GET /trending/:chain
```

## Security

### Contract Analysis
```
GET /security/:chain/:address
```

### Honeypot Check
```
GET /security/honeypot/:chain/:address
```

**Response:**
```json
{
  "isHoneypot": false,
  "reason": null
}
```

## Holders

### Get Holder Analysis
```
GET /holders/:chain/:address
```

### Get Top Holders
```
GET /holders/:chain/:address/top?limit=100
```

## Watchlist

### Add to Watchlist
```
POST /watchlist
```

**Body:**
```json
{
  "chain": "ethereum",
  "address": "0x..."
}
```

### Get Watchlist
```
GET /watchlist
```

### Remove from Watchlist
```
DELETE /watchlist/:id
```

## Search

### Search Tokens
```
GET /search?q=pepe
```

## Error Responses

```json
{
  "success": false,
  "error": "Error message",
  "timestamp": 1234567890
}
```

## Status Codes

| Code | Meaning |
|------|---------|
| 200 | Success |
| 400 | Bad request |
| 401 | Unauthorized |
| 404 | Not found |
| 429 | Rate limited |
| 500 | Server error |
