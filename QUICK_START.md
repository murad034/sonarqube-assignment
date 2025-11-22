# 🎯 Quick Start Guide - Next Steps

## What Has Been Set Up

✅ **docker-compose.yml** - SonarQube server configuration
✅ **sonar-project.properties** - SonarQube project settings  
✅ **.github/workflows/sonarqube.yml** - GitHub Actions CI/CD
✅ **package.json** - Updated with test coverage scripts
✅ **Test files** - Fixed to match actual responses
✅ **.gitignore** - Added coverage and SonarQube directories

## 🚀 Next Steps (Follow in Order)

### Step 1: Install NYC for Coverage
```powershell
npm install
```

### Step 2: Test Locally First
```powershell
# Run tests to make sure everything works
npm test

# Run with coverage
npm run test:coverage
```

### Step 3: Start SonarQube Server
```powershell
# Make sure Docker Desktop is running, then:
docker-compose up -d

# Wait 2-3 minutes for SonarQube to start
# Check logs: docker logs -f sonarqube
```

### Step 4: Configure SonarQube
1. Open http://localhost:9000
2. Login: admin / admin (change password when prompted)
3. Click "Create Project" → "Manually"
4. Project key: `sonarqube-assignment`
5. Display name: `SonarQube Assignment - Node.js App`
6. Click "Set Up"
7. Choose "With GitHub Actions"
8. Generate token and **SAVE IT**

### Step 5: Create GitHub Repository
```powershell
# Initialize git (if not already done)
git init
git add .
git commit -m "Add SonarQube integration"

# Create repo on GitHub, then:
git remote add origin https://github.com/YOUR-USERNAME/sonarqube-assignment.git
git branch -M main
git push -u origin main
```

### Step 6: Add GitHub Secrets
Go to: `GitHub Repo → Settings → Secrets and variables → Actions`

Add these 3 secrets:

1. **SONAR_TOKEN**
   - Value: Your token from Step 4

2. **SONAR_HOST_URL**
   - For local: Use ngrok (see below)
   - For cloud: Your server URL

3. **SONAR_PROJECT_KEY**
   - Value: `sonarqube-assignment`

### Step 7: Expose Local SonarQube (if using localhost)

**Option A: Use ngrok (Recommended)**
```powershell
# Download ngrok from https://ngrok.com/download
# Run:
ngrok http 9000

# Copy the HTTPS URL (e.g., https://abc123.ngrok.io)
# Use this URL as SONAR_HOST_URL in GitHub Secrets
```

**Option B: Use SonarCloud**
- Sign up at https://sonarcloud.io (free for public repos)
- Follow their integration guide

### Step 8: Trigger GitHub Actions
```powershell
# Make any change to trigger workflow
git add .
git commit -m "Trigger SonarQube analysis"
git push
```

### Step 9: Verify Results

1. **GitHub Actions**
   - Go to: `GitHub Repo → Actions`
   - Watch the workflow run

2. **SonarQube Dashboard**
   - Go to: http://localhost:9000
   - Click on your project
   - View the analysis results

### Step 10: Take Screenshots

Take screenshots of:
1. SonarQube Dashboard (main overview)
2. Code metrics (bugs, code smells, coverage)
3. GitHub Actions successful run
4. Quality Gate status

---

## 📝 Important Notes

### If Using Local SonarQube (localhost:9000)
⚠️ **GitHub Actions CANNOT access localhost directly**

You MUST use one of these:
- **ngrok** to create a public tunnel
- **SonarCloud** (free for public repos)
- Deploy SonarQube to a cloud server

### Coverage Not Showing?
Make sure:
- `nyc` is installed: `npm install`
- Tests run successfully: `npm test`
- Coverage file exists: `coverage/lcov.info`

### Workflow Failing?
Check:
- All 3 GitHub Secrets are set correctly
- SONAR_HOST_URL is publicly accessible
- SONAR_TOKEN is valid
- Project key matches in all files

---

## 🔧 Troubleshooting Commands

```powershell
# Check Docker status
docker ps

# View SonarQube logs
docker logs -f sonarqube

# Restart SonarQube
docker-compose down
docker-compose up -d

# Test locally before pushing
npm test
npm run test:coverage

# Check if coverage file exists
Test-Path coverage/lcov.info
```

---

## 📋 Submission Checklist

Before submitting, ensure you have:

- [ ] GitHub repository with all code
- [ ] GitHub Actions workflow running successfully
- [ ] SonarQube analysis completed
- [ ] Screenshot: SonarQube dashboard overview
- [ ] Screenshot: Code metrics (bugs, smells, coverage)
- [ ] Screenshot: GitHub Actions success
- [ ] Screenshot: Quality Gate status
- [ ] Repository is public or instructor has access

---

## 🎓 What Each File Does

| File | Purpose |
|------|---------|
| `docker-compose.yml` | Runs SonarQube server in Docker |
| `sonar-project.properties` | Configures what SonarQube analyzes |
| `.github/workflows/sonarqube.yml` | Automates analysis on every push |
| `package.json` | Contains test and coverage scripts |
| `SONARQUBE_SETUP.md` | Detailed setup instructions |

---

## 🆘 Need Help?

1. Read `SONARQUBE_SETUP.md` for detailed instructions
2. Check SonarQube logs: `docker logs sonarqube`
3. Verify GitHub Actions logs in the Actions tab
4. Ensure all secrets are set correctly

---

**You're all set! Follow the steps above to complete your assignment. Good luck! 🚀**
