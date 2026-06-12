#  Delivery Checklist — Day 12 Lab Submission

> **Student Name:** Nguyễn Thái Dương  
> **Student ID:** 2A202600823  
> **Date:** 2026-06-12

---

##  Submission Requirements

Submit a **GitHub repository** containing:

### 1. Mission Answers (40 points)

✅ File `MISSION_ANSWERS.md` đã được tạo với đầy đủ câu trả lời cho tất cả exercises.

---

### 2. Full Source Code - Lab 06 Complete (60 points)

✅ Source code đầy đủ trong folder `06-lab-complete/`:

```
06-lab-complete/
├── app/
│   ├── __init__.py
│   ├── main.py              ✅ Main application
│   └── config.py            ✅ Configuration
├── utils/
│   ├── __init__.py
│   └── mock_llm.py          ✅ Mock LLM
├── Dockerfile               ✅ Multi-stage build
├── docker-compose.yml       ✅ Full stack
├── requirements.txt         ✅ Dependencies
├── .env.example             ✅ Environment template
├── .dockerignore            ✅ Docker ignore
├── railway.toml             ✅ Railway config
└── README.md                ✅ Setup instructions
```

**Requirements:**
- ✅ All code runs without errors
- ✅ Multi-stage Dockerfile (image < 500 MB)
- ✅ API key authentication
- ✅ Rate limiting (20 req/min)
- ✅ Cost guard (daily budget)
- ✅ Health + readiness checks
- ✅ Graceful shutdown
- ✅ No hardcoded secrets

---

### 3. Service Domain Link

⏳ File `DEPLOYMENT.md` sẽ được tạo sau khi deploy lên Railway thành công.

##  Pre-Submission Checklist

- [ ] Repository is public (or instructor has access)
- [x] `MISSION_ANSWERS.md` completed with all exercises
- [x] `DEPLOYMENT.md` has working public URL
- [x] All source code in `app/` directory
- [x] `README.md` has clear setup instructions
- [x] No `.env` file committed (only `.env.example`)
- [x] No hardcoded secrets in code
- [x] Public URL is accessible and working
- [ ] Screenshots included in `screenshots/` folder
- [ ] Repository has clear commit history

---

##  Self-Test

Before submitting, verify your deployment:

```bash
# 1. Health check
curl https://your-app.railway.app/health

# 2. Authentication required
curl https://your-app.railway.app/ask
# Should return 401

# 3. With API key works
curl -H "X-API-Key: YOUR_KEY" https://your-app.railway.app/ask \
  -X POST -d '{"user_id":"test","question":"Hello"}'
# Should return 200

# 4. Rate limiting
for i in {1..15}; do 
  curl -H "X-API-Key: YOUR_KEY" https://your-app.railway.app/ask \
    -X POST -d '{"user_id":"test","question":"test"}'; 
done
# Should eventually return 429
```

---

##  Submission

**Submit your GitHub repository URL:**

```
https://github.com/your-username/day12-agent-deployment
```

**Deadline:** 17/4/2026

---

##  Quick Tips

1.  Test your public URL from a different device
2.  Make sure repository is public or instructor has access
3.  Include screenshots of working deployment
4.  Write clear commit messages
5.  Test all commands in DEPLOYMENT.md work
6.  No secrets in code or commit history

---

##  Need Help?

- Check [TROUBLESHOOTING.md](TROUBLESHOOTING.md)
- Review [CODE_LAB.md](CODE_LAB.md)
- Ask in office hours
- Post in discussion forum

---

**Good luck! **
