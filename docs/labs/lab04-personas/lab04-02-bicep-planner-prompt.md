# Lab 3: Planning Azure Deployment with Bicep Planner

## Overview
In this lab, you'll use the `bicep-planner` persona to create a comprehensive Azure infrastructure deployment plan for the application you built in the previous labs. The planner will analyze your application requirements and create a detailed, machine-readable plan that the implementer persona will use in the next lab.

---

## Instructions
1. Apply the `bicep-planner` persona first
2. Fill in the placeholders below (marked with `[YOUR_...]`)
3. Copy and execute the prompt

### How to Apply the Persona
```
Apply the bicep-planner persona
```

---

## Prompt

```
## Purpose
Create a comprehensive Azure infrastructure deployment plan for my application. The plan should define all Azure resources needed to host and run the application in a production-ready configuration.

## Rules
- Focus on infrastructure planning only—no actual Bicep code yet
- Use Azure Verified Modules (AVM) where available
- Consider cost-effective options suitable for a demo/learning environment
- Account for my application's specific technology stack and runtime requirements

## Input

**Application Details:**
- Application Name: [YOUR_APP_NAME - e.g., "WeatherDashboard", "FoodTracker"]
- Application Type: [YOUR_APP_TYPE - e.g., "web application", "API", "static site"]
- Programming Language/Framework: [YOUR_LANGUAGE - e.g., "Python Flask", "Node.js Express", "React", "C# ASP.NET Core"]
- Runtime Requirements: [YOUR_RUNTIME - e.g., "Python 3.11", "Node 20 LTS", ".NET 8"]

**Hosting Preferences (choose one):**
- [ ] Azure App Service (Web Apps)
- [ ] Azure Container Apps
- [ ] Azure Static Web Apps (for static/SPA sites)
- [ ] Azure Functions (for serverless)
- [ ] Let the planner recommend based on my app

**Additional Requirements (check all that apply):**
- [ ] Database needed: [TYPE - e.g., "SQL", "CosmosDB", "PostgreSQL"]
- [ ] Storage needed for files/blobs
- [ ] Custom domain support
- [ ] Application Insights monitoring

## Steps
1. Analyze my application requirements based on the language and framework
2. Research appropriate Azure services for hosting this type of application
3. Identify Azure Verified Modules for the required resources
4. Document resource specifications with parameters and dependencies
5. Create implementation phases ordered by dependencies
6. Generate architecture diagram showing resource relationships
7. Write the complete plan to `.bicep-planning-files/INFRA.[goal].md`

## Metrics
**Expected Output:**
- A complete infrastructure plan saved to `.bicep-planning-files/INFRA.[YOUR_APP_NAME].md`
- Resource specifications with AVM module references and versions
- Clear implementation phases with task breakdowns
- Architecture diagram showing all resources and connections

**Next Step:** Once the plan is complete, proceed to Lab 4 and switch to the `bicep-implementer` persona to generate the actual Bicep templates.
```

---

## Common Application Examples

Use these as reference for filling in your application details:

### Python Flask Weather App
```
Application Name: WeatherDashboard
Application Type: web application
Programming Language/Framework: Python Flask
Runtime Requirements: Python 3.11
Hosting: Azure App Service
Additional: Application Insights monitoring
```

### React Food Tracker
```
Application Name: FoodTracker
Application Type: Single Page Application (SPA)
Programming Language/Framework: React with Vite
Runtime Requirements: Node 20 (build only, static hosting)
Hosting: Azure Static Web Apps
Additional: CosmosDB for data storage
```

### Node.js Country Explorer API
```
Application Name: CountryExplorer
Application Type: REST API
Programming Language/Framework: Node.js Express
Runtime Requirements: Node 20 LTS
Hosting: Azure Container Apps
Additional: Application Insights monitoring
```

### C# ASP.NET Core Web App
```
Application Name: TaskManager
Application Type: web application with API
Programming Language/Framework: C# ASP.NET Core
Runtime Requirements: .NET 8
Hosting: Azure App Service
Additional: Azure SQL Database, Application Insights
