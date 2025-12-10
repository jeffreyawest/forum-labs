# Lab 4: Implementing Bicep Templates with Bicep Implementer

## Overview
In this lab, you'll use the `bicep-implementer` persona to generate production-ready Azure Bicep templates based on the infrastructure plan you created in Lab 3. The implementer will read your plan and create modular, validated Bicep code following Azure best practices.

---

## Prerequisites
- Completed Lab 3 with a plan saved in `.bicep-planning-files/`
- Bicep CLI installed (for validation commands)

---

## Instructions
1. Ensure you have completed Lab 3 and have a plan in `.bicep-planning-files/`
2. Apply the `bicep-implementer` persona
3. Fill in the placeholders below (marked with `[YOUR_...]`)
4. Copy and execute the prompt

### How to Apply the Persona
```
Apply the bicep-implementer persona
```

---

## Prompt

```
## Purpose
Implement production-ready Azure Bicep templates based on the infrastructure plan created in the previous lab. The templates should be modular, secure, and follow Azure best practices.

## Rules
- Follow the implementation plan in `.bicep-planning-files/`
- Use Azure Verified Modules as specified in the plan
- No hardcoded secrets—use secure parameters or Key Vault references
- All templates must pass `bicep build`, `bicep lint`, and `bicep format` validation
- Remove any unused parameters or variables

## Input

**Plan Location:** `.bicep-planning-files/INFRA.[YOUR_APP_NAME].md`

**Output Configuration:**
- Output Path: [YOUR_OUTPUT_PATH - default: `infra/bicep/[YOUR_APP_NAME]`]

**Environment Parameters:**
- Environment Name: [YOUR_ENV - e.g., "dev", "demo", "lab"]
- Azure Region: [YOUR_REGION - e.g., "eastus", "westus2", "westeurope"]
- Resource Name Prefix: [YOUR_PREFIX - e.g., "lab", "demo", your initials]

## Steps
1. Read the implementation plan from `.bicep-planning-files/INFRA.[YOUR_APP_NAME].md`
2. Create the output directory structure
3. Implement the main Bicep template with proper parameters
4. Create any required child modules as specified in the plan
5. Run `bicep restore` to fetch Azure Verified Modules
6. Validate with `bicep build --stdout --no-restore`
7. Format with `bicep format`
8. Lint with `bicep lint` and fix any warnings
9. Verify no unused code and clean up artifacts

## Metrics
**Expected Output:**
- Complete Bicep templates in `infra/bicep/[YOUR_APP_NAME]/`
- Main template (`main.bicep`) with all resources or module references
- All validation commands passing with no errors or warnings
- Ready for deployment (though deployment is optional for this lab)

**Verification Commands (run these to verify):**
```bash
bicep build infra/bicep/[YOUR_APP_NAME]/main.bicep --stdout --no-restore
bicep lint infra/bicep/[YOUR_APP_NAME]/main.bicep
```

**Optional Next Step:** If you want to actually deploy, run:
```bash
az deployment group create --resource-group [YOUR_RG] --template-file infra/bicep/[YOUR_APP_NAME]/main.bicep
```
```

---

## Example Filled-In Prompt

Here's what the prompt might look like for a Python Flask weather app:

```
## Purpose
Implement production-ready Azure Bicep templates based on the infrastructure plan created in the previous lab. The templates should be modular, secure, and follow Azure best practices.

## Rules
- Follow the implementation plan in `.bicep-planning-files/`
- Use Azure Verified Modules as specified in the plan
- No hardcoded secrets—use secure parameters or Key Vault references
- All templates must pass `bicep build`, `bicep lint`, and `bicep format` validation
- Remove any unused parameters or variables

## Input

**Plan Location:** `.bicep-planning-files/INFRA.WeatherDashboard.md`

**Output Configuration:**
- Output Path: `infra/bicep/weather-dashboard`

**Environment Parameters:**
- Environment Name: demo
- Azure Region: eastus
- Resource Name Prefix: lab

## Steps
1. Read the implementation plan from `.bicep-planning-files/INFRA.WeatherDashboard.md`
2. Create the output directory structure
3. Implement the main Bicep template with proper parameters
4. Create any required child modules as specified in the plan
5. Run `bicep restore` to fetch Azure Verified Modules
6. Validate with `bicep build --stdout --no-restore`
7. Format with `bicep format`
8. Lint with `bicep lint` and fix any warnings
9. Verify no unused code and clean up artifacts

## Metrics
**Expected Output:**
- Complete Bicep templates in `infra/bicep/weather-dashboard/`
- Main template (`main.bicep`) with all resources or module references
- All validation commands passing with no errors or warnings
- Ready for deployment (though deployment is optional for this lab)
```

---

## Troubleshooting

### "Module not found" errors
Run `bicep restore` before building:
```bash
bicep restore infra/bicep/[YOUR_APP_NAME]/main.bicep
```

### Linting warnings
The implementer persona will automatically address warnings. If you see any after completion, ask:
```
Fix the linting warnings in the Bicep templates
```

### Validation failures
Ask the agent to diagnose and fix:
```
The bicep build command failed with errors. Please diagnose and fix the issues.
