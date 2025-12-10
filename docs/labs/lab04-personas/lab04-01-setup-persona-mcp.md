# Lab Setup: Installing the Persona MCP Server

This guide will help you install and configure the Persona MCP Server to use the Bicep Planner and Bicep Implementer personas in Lab 4.

## Prerequisites

Before starting, ensure you have:

- **Visual Studio Code** (or VS Code Insiders)
- **.NET 9.0 SDK** or later - [Download here](https://dotnet.microsoft.com/download)
  - ⚠️ **Important**: You need the **SDK**, not just the Runtime
  - The SDK includes the `dotnet tool` command used for installation
- **Cline extension** for VS Code

### Verify Prerequisites

Open PowerShell and run:

```powershell
# Check .NET SDK is installed (should show 9.0.x or higher)
dotnet --version

# Verify the dotnet tool command works
dotnet tool list -g
```

If `dotnet` is not recognized, install the .NET 9.0 SDK from the link above and restart PowerShell.

---

## 🚀 Quick Setup (Recommended)

**If you already have Cline installed**, you can use the automated setup workflow:

### Step 1: Install the Workflow File

Copy the workflow file to your Cline workflows directory:

```powershell
# Create the workflows directory if it doesn't exist
New-Item -ItemType Directory -Force -Path ".clinerules\workflows"

# Copy the workflow file (run this from the folder where you extracted the zip)
Copy-Item "setup-persona-mcp-workflow.md" -Destination ".clinerules\workflows\setup-persona-mcp.md"
```

> **Note**: Run these commands from your project's root directory (the folder where your code is).

### Step 2: Run the Workflow

1. Open your project in VS Code
2. Open Cline
3. Type: `/setup-persona-mcp`
4. Follow the prompts - Cline will handle installation and configuration automatically!

The workflow will:
- ✅ Verify .NET is installed
- ✅ Ask you to choose installation method (NuGet feed or local package)
- ✅ Install the Persona MCP Server tool
- ✅ Configure Cline to use the server
- ✅ Verify everything is working

---

## 🔄 Already Have Persona MCP Installed?

If you previously installed the Persona MCP Server, you may need to update it. The artifact feed location has changed recently.

### Check Your Current Version

```powershell
dotnet tool list -g | Select-String 'SilverMcp.Personas'
```

### Update to Latest Version

```powershell
# Update from the new feed
dotnet tool update -g SilverMcp.Personas --add-source https://pkgs.dev.azure.com/msazure/One/_packaging/Silver-MCP/nuget/v3/index.json
```

If the update fails with authentication errors, uninstall and reinstall:

```powershell
dotnet tool uninstall -g SilverMcp.Personas
dotnet tool install -g SilverMcp.Personas --add-source https://pkgs.dev.azure.com/msazure/One/_packaging/Silver-MCP/nuget/v3/index.json
```

### Update Your Cline Configuration

After updating the tool, verify your `cline_mcp_settings.json` has the correct configuration:

**Location:**
- **VS Code**: `%APPDATA%\Code\User\globalStorage\saoudrizwan.claude-dev\settings\cline_mcp_settings.json`
- **VS Code Insiders**: `%APPDATA%\Code - Insiders\User\globalStorage\saoudrizwan.claude-dev\settings\cline_mcp_settings.json`

**Required Configuration:**

The `CUSTOM_PERSONAS_PATH` environment variable is required. First, create a `.mcp/personas/` directory in your project:

```powershell
New-Item -ItemType Directory -Force -Path ".mcp\personas"
```

Then update your configuration with the full path:

```json
{
  "mcpServers": {
    "personas": {
      "type": "stdio",
      "command": "silver-persona-mcp-server",
      "args": [],
      "env": {
        "CUSTOM_PERSONAS_PATH": "C:\\path\\to\\your\\repo\\.mcp\\personas"
      },
      "disabled": false,
      "timeout": 60
    }
  }
}
```

> **Important**: Replace `C:\\path\\to\\your\\repo` with the actual full path to your project directory.

### ⚠️ Close ALL VS Code Instances

After updating, you **must close ALL Visual Studio Code windows** (not just the current one) and reopen VS Code for the changes to take effect.

---

## Manual Installation

If you prefer to install manually or the workflow isn't available, follow these steps:

### Installation Options

| Method | Use When |
|--------|----------|
| **Option A: NuGet Feed** | You have access to the msazure Azure DevOps artifact feed |
| **Option B: Local Package** | You received a zip file containing the NuGet package |

---

### Option A: Install from NuGet Feed

Use this method if you have access to the msazure Azure DevOps artifact feed.

#### Step 1: Install the Global Tool

Run this PowerShell command:

```powershell
# Install or update the Persona MCP Server global tool
if (dotnet tool list -g | Select-String 'SilverMcp.Personas') { 
    dotnet tool update -g SilverMcp.Personas --add-source https://pkgs.dev.azure.com/msazure/One/_packaging/Silver-MCP/nuget/v3/index.json
} else { 
    dotnet tool install -g SilverMcp.Personas --add-source https://pkgs.dev.azure.com/msazure/One/_packaging/Silver-MCP/nuget/v3/index.json
}
```

#### Step 2: Verify Installation

```powershell
dotnet tool list -g | Select-String 'SilverMcp.Personas'
```

You should see `silvermcp.personas` in the output.

---

### Option B: Install from Local Package

Use this method if you received the zip file with the NuGet package included.

#### Step 1: Extract the Zip File

Extract the provided zip file to a location on your machine. You should see:
- `SilverMcp.Personas.1.4.0.nupkg` - The NuGet package
- Lab prompt files (`.md` files)

#### Step 2: Install the Global Tool from Local Package

Open PowerShell and navigate to the folder containing the `.nupkg` file, then run:

```powershell
# Navigate to the folder with the nupkg file
cd "C:\path\to\extracted\zip"

# Install from local package
dotnet tool install -g SilverMcp.Personas --add-source .
```

> **Note**: The `--add-source .` tells dotnet to look in the current directory for the package.

#### Step 3: Verify Installation

```powershell
dotnet tool list -g | Select-String 'SilverMcp.Personas'
```

You should see `silvermcp.personas` in the output.

---

### Configuration (Manual)

After installation, configure Cline to use the Persona MCP Server.

1. **Open Cline Settings**:
   - Open Cline in VS Code
   - Click "MCP Servers" at the top
   - Click the "Configure" tab
   - Click "Configure MCP Servers" button to open `cline_mcp_settings.json`

2. **Create Custom Personas Directory**:

Create a `.mcp/personas/` directory in your project root:

```powershell
New-Item -ItemType Directory -Force -Path ".mcp\personas"
```

3. **Add Persona Server Configuration**:

Add the following configuration, replacing the path with your project's full path:

```json
{
  "mcpServers": {
    "personas": {
      "type": "stdio",
      "command": "silver-persona-mcp-server",
      "args": [],
      "env": {
        "CUSTOM_PERSONAS_PATH": "C:\\path\\to\\your\\repo\\.mcp\\personas"
      },
      "disabled": false,
      "timeout": 60
    }
  }
}
```

> **Important**: The `CUSTOM_PERSONAS_PATH` is required. Replace `C:\\path\\to\\your\\repo` with the actual full path to your project directory.

3. **Restart VS Code** completely (not just reload window)

---

## Verification

Verify the Persona MCP Server is working:

1. **Check Server Status**:
   - Open Cline and look for "personas" in the MCP servers list (it should show a green indicator)

2. **Test Connection**:
   - Ask Cline: `List all available personas`
   - You should see a list including `bicep-planner` and `bicep-implementer`

3. **Verify Tools Are Available**:
   - The following tools should be available:
     - `list_personas` - List all personas
     - `search_personas` - Search for personas by keyword
     - `apply_persona` - Apply a persona to your conversation

---

## Using Personas in the Labs

Once setup is complete, you can use the personas. **Important**: Start a new chat for each persona!

### Starting with Bicep Planner

1. Click the **"+"** button in Cline to start a new chat
2. Say: `Apply the bicep-planner persona`
3. Follow the prompts in `lab4-bicep-planner-prompt.md`

### Switching to Bicep Implementer

When ready for implementation:
1. Click the **"+"** button to start another new chat
2. Say: `Apply the bicep-implementer persona`
3. Follow the prompts in `lab4-bicep-implementer-prompt.md`

> **Why start a new chat?** Fresh conversations give the persona your full context window and avoid noise from previous work.

---

## Troubleshooting

### "Tool not found" Error

If the `silver-persona-mcp-server` command is not found:

1. Verify the tool is installed:
   ```powershell
   dotnet tool list -g
   ```

2. Check that the .NET tools path is in your PATH:
   - Windows: `%USERPROFILE%\.dotnet\tools`
   - Restart PowerShell/Terminal after installation

3. Try reinstalling:
   ```powershell
   dotnet tool uninstall -g SilverMcp.Personas
   # Then reinstall using Option A or B above
   ```

### Server Won't Start / Tools Not Appearing

1. Restart VS Code completely (not just reload window)
2. Check the Cline Output panel for error messages
3. Ensure .NET 9.0 SDK is installed:
   ```powershell
   dotnet --version
   ```

### Configuration File Issues

- Ensure JSON syntax is valid (VS Code will highlight errors)
- Verify there are no trailing commas in JSON objects
- Check that the server name matches exactly: `personas`

### Access Denied / Feed Authentication Issues

If using Option A and you get authentication errors:
- Use Option B (local package) instead
- Ask the lab facilitator for the zip file with the local package

---

## Next Steps

Once the Persona MCP Server is running:

1. **Lab 4 - Planning**: Use the `bicep-planner` persona with `lab4-bicep-planner-prompt.md`
2. **Lab 4 - Implementation**: Use the `bicep-implementer` persona with `lab4-bicep-implementer-prompt.md`
