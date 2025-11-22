# SonarQube Assignment - Complete Setup Guide

## 📋 Project Overview
This is a Node.js Express application integrated with SonarQube for automated code quality analysis using GitHub Actions.

## 🎯 Assignment Objectives
- ✅ Set up SonarQube server (Docker)
- ✅ Create sample Node.js project with tests
- ✅ Configure SonarQube analysis
- ✅ Set up GitHub Actions CI/CD
- ✅ Generate code quality reports

---

## 📂 Project Structure
```
sonarqube-assignment/
├── .github/
│   └── workflows/
│       └── sonarqube.yml          # GitHub Actions workflow
├── src/
│   ├── server.js                   # Main Express server
│   └── public/
│       └── index.html              # Static HTML page
├── test/
│   └── server.test.js              # Mocha/Chai tests
├── docker-compose.yml              # SonarQube server setup
├── sonar-project.properties        # SonarQube configuration
├── package.json                    # Node.js dependencies & scripts
└── README.md
```

---

## 🚀 Step-by-Step Setup Instructions

### **Step 1: Prepare the Environment**

#### 1.1 Install Prerequisites
Make sure you have installed:
- **Node.js** (v16 or higher)
- **Docker Desktop** (for running SonarQube)
- **Git** (for version control)

#### 1.2 Start SonarQube Server
```bash
# Navigate to project directory
cd e:\Development\Server\laragon\www\devops\ostad-2025\sonarqube-assignment

# Start SonarQube using Docker Compose
docker-compose up -d

# Check if container is running
docker ps
```

#### 1.3 Access SonarQube Dashboard
1. Open browser: http://localhost:9000
2. Default credentials:
   - **Username:** `admin`
   - **Password:** `admin`
3. You'll be prompted to change the password - set a new one

---

### **Step 2: Configure SonarQube Project**

#### 2.1 Create a New Project
1. In SonarQube dashboard, click **"Create Project"**
2. Choose **"Manually"**
3. Fill in:
   - **Project key:** `sonarqube-assignment`
   - **Display name:** `SonarQube Assignment - Node.js App`
4. Click **"Set Up"**

#### 2.2 Generate Authentication Token
1. Choose **"With GitHub Actions"** as the analysis method
2. Under **"Provide a token"**, click **"Generate a token"**
3. Give it a name: `github-actions-token`
4. Click **"Generate"**
5. **Copy the token** - you'll need it for GitHub Secrets

#### 2.3 Note Your Configuration
Keep these values handy:
- **SONAR_TOKEN:** `<your-generated-token>`
- **SONAR_HOST_URL:** `http://localhost:9000` (for local) or your server URL
- **SONAR_PROJECT_KEY:** `sonarqube-assignment`

---

### **Step 3: Install Dependencies**

```bash
# Install Node.js dependencies
npm install

# Install nyc for test coverage
npm install --save-dev nyc
```

---

### **Step 4: Test Locally**

#### 4.1 Run Tests with Coverage
```bash
# Run tests
npm test

# Run tests with coverage
npm run test:coverage
```

You should see coverage reports in the `coverage/` directory.

#### 4.2 Verify Server
```bash
# Start the server
npm start

# Visit http://localhost:3000 to see your app
```

---

### **Step 5: Set Up GitHub Repository**

#### 5.1 Initialize Git (if not already done)
```bash
git init
git add .
git commit -m "Initial commit with SonarQube integration"
```

#### 5.2 Create GitHub Repository
1. Go to https://github.com/new
2. Create repository: `sonarqube-assignment`
3. **Do NOT** initialize with README (we already have one)

#### 5.3 Push to GitHub
```bash
git remote add origin https://github.com/<your-username>/sonarqube-assignment.git
git branch -M main
git push -u origin main
```

---

### **Step 6: Configure GitHub Secrets**

⚠️ **Important:** For GitHub Actions to work with SonarQube, you need to add secrets.

#### 6.1 Add Repository Secrets
1. Go to your GitHub repository
2. Click **Settings** → **Secrets and variables** → **Actions**
3. Click **"New repository secret"** and add these three secrets:

| Secret Name | Value | Example |
|-------------|-------|---------|
| `SONAR_TOKEN` | Your generated token from SonarQube | `squ_a1b2c3d4e5f6...` |
| `SONAR_HOST_URL` | Your SonarQube server URL | `http://your-server-ip:9000` or use ngrok for local |
| `SONAR_PROJECT_KEY` | Your project key | `sonarqube-assignment` |

#### 6.2 Expose Local SonarQube (If using localhost)

**Option A: Use ngrok (Recommended for testing)**
```bash
# Install ngrok: https://ngrok.com/download
# Start ngrok tunnel
ngrok http 9000

# Copy the HTTPS URL (e.g., https://abc123.ngrok.io)
# Use this as SONAR_HOST_URL in GitHub Secrets
```

**Option B: Use a Cloud SonarQube Instance**
- Use SonarCloud (https://sonarcloud.io) - Free for public repos
- Or deploy SonarQube on a cloud server (AWS, Azure, DigitalOcean)

---

### **Step 7: Trigger GitHub Actions Workflow**

#### 7.1 Make a Code Change
```bash
# Make any small change to trigger the workflow
echo "# Test change" >> README.md
git add .
git commit -m "Trigger SonarQube analysis"
git push
```

#### 7.2 Monitor Workflow
1. Go to GitHub repository → **Actions** tab
2. Click on the latest workflow run
3. Watch the "SonarQube Analysis" job execute

#### 7.3 Workflow Steps
The workflow will:
1. ✅ Checkout code
2. ✅ Set up Node.js environment
3. ✅ Install dependencies
4. ✅ Run tests with coverage
5. ✅ Execute SonarQube scanner
6. ✅ Check quality gate status

---

### **Step 8: Verify SonarQube Report**

#### 8.1 View Dashboard
1. Go to SonarQube: http://localhost:9000 (or your server URL)
2. Click on **"Projects"**
3. Select **"SonarQube Assignment - Node.js App"**

#### 8.2 Check Metrics
You should see:
- **Bugs:** Number of bug issues
- **Vulnerabilities:** Security issues
- **Code Smells:** Maintainability issues
- **Coverage:** Test coverage percentage
- **Duplications:** Duplicate code blocks
- **Security Hotspots:** Areas needing security review

#### 8.3 Quality Gate
- Check if the project passed the Quality Gate
- Review any failed conditions

---

## 📸 Screenshots to Submit

Take screenshots of:

1. **SonarQube Dashboard Overview**
   - Shows project summary with metrics

2. **Code Issues Tab**
   - Shows bugs, code smells, vulnerabilities

3. **Coverage Report**
   - Shows test coverage percentage

4. **GitHub Actions Workflow**
   - Shows successful workflow run

5. **Quality Gate Status**
   - Shows pass/fail status

---

## 🔧 Troubleshooting

### Issue: GitHub Actions can't connect to SonarQube
**Solution:**
- Ensure SONAR_HOST_URL is publicly accessible (use ngrok for local)
- Check firewall settings
- Verify SONAR_TOKEN is correct

### Issue: Tests failing
**Solution:**
```bash
# Run tests locally first
npm test

# Check test output
npm run test:coverage
```

### Issue: SonarQube container won't start
**Solution:**
```bash
# Check Docker logs
docker logs sonarqube

# Restart container
docker-compose down
docker-compose up -d

# Increase Docker memory (min 2GB recommended)
```

### Issue: Coverage report not showing
**Solution:**
- Ensure `nyc` is installed: `npm install --save-dev nyc`
- Check coverage file exists: `coverage/lcov.info`
- Verify path in `sonar-project.properties`

---

## 📊 Expected Results

After successful setup, you should have:

✅ **Local SonarQube server** running on port 9000  
✅ **GitHub repository** with code  
✅ **GitHub Actions workflow** running automatically on push  
✅ **SonarQube analysis report** with quality metrics  
✅ **Test coverage report** integrated  
✅ **Quality Gate** evaluation  

---

## 📝 Submission Checklist

- [ ] GitHub repository link
- [ ] SonarQube dashboard screenshot (main overview)
- [ ] Code metrics screenshot (bugs, code smells, coverage)
- [ ] GitHub Actions workflow screenshot (successful run)
- [ ] Quality Gate status screenshot

---

## 🔗 Useful Commands

```bash
# Start SonarQube
docker-compose up -d

# Stop SonarQube
docker-compose down

# View SonarQube logs
docker logs -f sonarqube

# Install dependencies
npm install

# Run tests
npm test

# Run tests with coverage
npm run test:coverage

# Start application
npm start

# Git commands
git add .
git commit -m "Your message"
git push
```

---

## 📚 Additional Resources

- [SonarQube Documentation](https://docs.sonarqube.org/)
- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [SonarScanner for JavaScript](https://docs.sonarqube.org/latest/analysis/scan/sonarscanner/)
- [Mocha Testing Framework](https://mochajs.org/)
- [NYC Code Coverage](https://github.com/istanbuljs/nyc)

---

## 🎓 What You've Learned

1. ✅ Setting up SonarQube with Docker
2. ✅ Configuring code quality analysis
3. ✅ Creating CI/CD pipelines with GitHub Actions
4. ✅ Implementing automated testing with coverage
5. ✅ Interpreting code quality metrics
6. ✅ Using Quality Gates for code standards

---

## 👤 Author

**Your Name**  
GitHub: [@your-username](https://github.com/your-username)

---

## 📄 License

This project is for educational purposes as part of the SonarQube assignment.

---

**Good luck with your assignment! 🚀**
