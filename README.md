# 🎯 SonarQube Assignment - Node.js Express App

[![SonarQube Analysis](https://github.com/your-username/sonarqube-assignment/actions/workflows/sonarqube.yml/badge.svg)](https://github.com/your-username/sonarqube-assignment/actions/workflows/sonarqube.yml)

A Node.js Express application integrated with SonarQube for automated code quality analysis using GitHub Actions.

## 📋 About The Application

This application has 2 routes:
- `/` - Shows a hello world page
- `/api` - Returns a JSON response

**Default Port:** 3000

## Prerequisites

- Node.js v18+ (or v22)
- Docker Desktop (for SonarQube)
- Git

## 🚀 Quick Start

### 1. Install Dependencies
```bash
npm install 
```

### 2. Start SonarQube Server (New)
```bash
docker-compose up -d
```
Access at: http://localhost:9000 (Default: admin/admin)

### 3. Run Application
```bash
npm start
```
Visit: http://localhost:3000

### 4. Run Tests
```bash
npm test                 # Run tests
npm run test:coverage    # Run with coverage report
npm run check            # Legacy test command
```

## 📊 SonarQube Integration

### Project Structure
```
├── .github/workflows/sonarqube.yml    # CI/CD pipeline
├── src/
│   ├── server.js                       # Express server
│   └── public/index.html               # Static page
├── test/server.test.js                 # Test cases
├── docker-compose.yml                  # SonarQube setup
├── sonar-project.properties            # SonarQube config
└── package.json                        # Dependencies
```

### Required GitHub Secrets
Add these in **Settings → Secrets → Actions**:

| Secret | Description | Example |
|--------|-------------|---------|
| `SONAR_TOKEN` | SonarQube authentication token | `squ_a1b2c3...` |
| `SONAR_HOST_URL` | SonarQube server URL | `http://your-ip:9000` |
| `SONAR_PROJECT_KEY` | Project identifier | `sonarqube-assignment` |

### SonarQube Metrics
- 🐛 **Bugs** - Logic errors
- 🔒 **Vulnerabilities** - Security issues  
- 💡 **Code Smells** - Maintainability issues
- 📈 **Coverage** - Test coverage percentage
- 🔄 **Duplications** - Code duplication

## 🚢 Deployment Process

### Using PM2
1. **Cleanup**: Removes existing process if running
   ```bash
   pm2 delete node-app || true
   ```

2. **Start Application**: Launches with absolute path
   ```bash
   pm2 start "./src/server.js" --name node-app
   ```

3. **Save Process List**: Persists PM2 configuration
   ```bash
   pm2 save
   ```

## 🛠️ Useful Commands

```bash
# Docker (SonarQube)
docker-compose up -d          # Start SonarQube
docker-compose down           # Stop SonarQube
docker logs sonarqube         # View logs

# Development
npm start                     # Start server
npm test                      # Run tests
npm run test:coverage         # Coverage report

# Git
git add .
git commit -m "message"
git push
```

## 📚 Complete Setup Guide

For detailed SonarQube setup instructions, see **[SONARQUBE_SETUP.md](./SONARQUBE_SETUP.md)**

## 🎓 Assignment Completion Checklist

✅ SonarQube server setup with Docker  
✅ Sample Node.js project with tests  
✅ SonarQube configuration file  
✅ GitHub Actions workflow  
✅ Automated code quality analysis  
✅ Test coverage integration  
✅ Quality Gate evaluation  

## 🔗 Links

- **SonarQube Dashboard:** http://localhost:9000
- **GitHub Repository:** https://github.com/your-username/sonarqube-assignment
- **Live App:** http://localhost:3000

---

**Made with ❤️ for DevOps Assignment 2025**



