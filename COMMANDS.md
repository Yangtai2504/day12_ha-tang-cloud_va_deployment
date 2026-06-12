# Commands Cheat Sheet — Day 12 Lab

---

## Part 1 — Localhost vs Production

### Develop version
```bash
cd 01-localhost-vs-production/develop
python -m venv .venv && .venv\Scripts\activate
pip install -r requirements.txt
python app.py
```
```bash
# Terminal mới
curl "http://localhost:8000/ask?question=Hello" -X POST
```

### Production version
```bash
cd 01-localhost-vs-production/production
copy .env.example .env
pip install -r requirements.txt
python app.py
```
```bash
# Terminal mới
curl http://localhost:8000/ask -X POST -H "Content-Type: application/json" -d "{\"question\": \"Hello\"}"
curl http://localhost:8000/health
curl http://localhost:8000/ready
```

---

## Part 2 — Docker

### Exercise 2.2: Build & run develop image
```bash
cd "c:\VinAI\Lab coding\day12_ha-tang-cloud_va_deployment"
docker build -f 02-docker/develop/Dockerfile -t agent-develop .
docker run -p 8000:8000 agent-develop
```
```bash
# Terminal mới
curl http://localhost:8000/ask -X POST -H "Content-Type: application/json" -d "{\"question\": \"What is Docker?\"}"
docker images agent-develop
```

### Exercise 2.3: Build production (multi-stage) & so sánh size
```bash
docker build -f 02-docker/production/Dockerfile -t agent-production .
docker images | findstr agent
```

### Exercise 2.4: Docker Compose stack
```bash
cd 02-docker/production
docker compose up
```
```bash
# Terminal mới
curl http://localhost/health
curl http://localhost/ask -X POST -H "Content-Type: application/json" -d "{\"question\": \"Explain microservices\"}"
```

---

## Part 3 — Cloud Deployment (Railway)

```bash
cd "c:\VinAI\Lab coding\day12_ha-tang-cloud_va_deployment\03-cloud-deployment\railway"
railway login
railway init
railway variables set AGENT_API_KEY=my-secret-key-123
railway variables set ENVIRONMENT=production
railway up
railway domain
```
```bash
# Test public URL (thay YOUR_DOMAIN)
curl https://YOUR_DOMAIN/health
curl https://YOUR_DOMAIN/ask -X POST -H "X-API-Key: my-secret-key-123" -H "Content-Type: application/json" -d "{\"question\": \"Hello\"}"
```

---

## Part 4 — API Security

### Exercise 4.1: API Key authentication
```bash
cd 04-api-gateway/develop
python -m venv .venv && .venv\Scripts\activate
pip install -r requirements.txt
python app.py
```
```bash
# Terminal mới — không có key (expect 401)
curl http://localhost:8000/ask -X POST -H "Content-Type: application/json" -d "{\"question\": \"Hello\"}"
# Có key (expect 200)
curl http://localhost:8000/ask -X POST -H "X-API-Key: secret-key-123" -H "Content-Type: application/json" -d "{\"question\": \"Hello\"}"
```

### Exercise 4.2: JWT authentication
```bash
cd 04-api-gateway/production
pip install -r requirements.txt
python app.py
```
```bash
# Terminal mới — lấy token
curl http://localhost:8000/auth/token -X POST -H "Content-Type: application/json" -d "{\"username\": \"student\", \"password\": \"demo123\"}"

# Dùng token (thay TOKEN bằng giá trị nhận được)
curl http://localhost:8000/ask -X POST -H "Authorization: Bearer TOKEN" -H "Content-Type: application/json" -d "{\"question\": \"Explain JWT\"}"
```

### Exercise 4.3: Rate limiting (gọi 15 lần, quan sát 429)
```bash
for /L %i in (1,1,15) do curl http://localhost:8000/ask -X POST -H "Authorization: Bearer TOKEN" -H "Content-Type: application/json" -d "{\"question\": \"Test\"}"
```

---

## Part 5 — Scaling & Reliability

### Docker Compose scale 3 instances
```bash
cd 05-scaling-reliability/production
docker compose up --scale agent=3
```
```bash
# Terminal mới — quan sát served_by thay đổi giữa các request
for /L %i in (1,1,6) do curl http://localhost/chat -X POST -H "Content-Type: application/json" -d "{\"question\": \"Request %i\"}"
```

### Test stateless
```bash
python test_stateless.py
```

---

## Part 6 — Deploy Final Project

```bash
cd 06-lab-complete
railway up
python check_production_ready.py
```
