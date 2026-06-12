# Deployment Information

## Public URL
https://day12agent-production.up.railway.app

## Platform
Railway

## Test Commands

### Health Check
```bash
curl https://day12agent-production.up.railway.app/health
# Expected: {"status":"ok","uptime_seconds":...}
```

### API Test (with authentication)
```bash
curl https://day12agent-production.up.railway.app/ask -X POST \
  -H "X-API-Key: my-secret-key-123" \
  -H "Content-Type: application/json" \
  -d '{"question": "Hello"}'
# Expected: {"question":"Hello","answer":"..."}
```

### Auth required (no key)
```bash
curl https://day12agent-production.up.railway.app/ask -X POST \
  -H "Content-Type: application/json" \
  -d '{"question": "Hello"}'
# Expected: 401 Unauthorized
```

## Environment Variables Set
- `AGENT_API_KEY`
- `ENVIRONMENT=production`

## Screenshots
*(Thêm screenshots vào folder `screenshots/` trước khi nộp)*
