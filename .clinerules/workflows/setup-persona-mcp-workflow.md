# Setup Persona MCP Server Workflow

This workflow automates the installation and configuration of the Persona MCP Server for AI Forum labs.

> **To run this workflow**: Type `/setup-persona-mcp` in Cline chat

<workflow_overview>
## Purpose
Install and configure the Persona MCP Server (`silver-persona-mcp-server`) to enable the Bicep Planner and Bicep Implementer personas for infrastructure deployment labs.

## Prerequisites
- Visual Studio Code (or VS Code Insiders)
- .NET 9.0 SDK or later installed (⚠️ **SDK required**, not just Runtime - the SDK includes the `dotnet tool` command)
- Cline extension for VS Code

## What This Workflow Does
1. Verifies .NET 9.0 SDK is installed
2. Asks you to choose installation method (NuGet feed or local package)
3. Installs the `silver-persona-mcp-server` global tool
4. Configures Cline to use the Persona MCP Server
5. Verifies the setup is working
</workflow_overview>

<detailed_sequence_of_steps>

## Step 1: Verify Prerequisites

First, check that .NET 9.0 SDK is installed:

```xml
<execute_command>
<command>dotnet --version</command>
<requires_approval>false</requires_approval>
</execute_command>
```

If .NET is not installed or version is below 9.0, inform the user:

```xml
<ask_followup_question>
<question>.NET 9.0 SDK or later is required but was not detected. Please install it from https://dotnet.microsoft.com/download and restart VS Code, then run this workflow again.

Would you like to continue anyway (if you believe .NET is installed but not in PATH)?</question>
<options>["Continue anyway", "Stop - I'll install .NET first"]</options>
</ask_followup_question>
```

## Step 2: Check for Existing Installation

Check if the Persona MCP Server is already installed:

```xml
<execute_command>
<command>powershell -Command "dotnet tool list -g | Select-String 'SilverMcp.Personas'"</command>
<requires_approval>false</requires_approval>
</execute_command>
```

**If the tool IS already installed**, proceed to Step 2A (Upgrade Path).

**If the tool is NOT installed**, skip to Step 3 (Determine Installation Method).

## Step 2A: Upgrade Path for Existing Installations

If the tool is already installed, the user may have it from an old artifact feed that has been deprecated. They need to:
1. Update the tool from the new feed
2. Manually update their Cline configuration
3. Close ALL VS Code instances before reopening

First, update the tool from the new feed:

```xml
<execute_command>
<command>powershell -Command "dotnet tool update -g SilverMcp.Personas --add-source https://pkgs.dev.azure.com/msazure/One/_packaging/Silver-MCP/nuget/v3/index.json"</command>
<requires_approval>true</requires_approval>
</execute_command>
```

If the update fails or shows authentication errors, try uninstalling and reinstalling:

```xml
<execute_command>
<command>powershell -Command "dotnet tool uninstall -g SilverMcp.Personas; dotnet tool install -g SilverMcp.Personas --add-source https://pkgs.dev.azure.com/msazure/One/_packaging/Silver-MCP/nuget/v3/index.json"</command>
<requires_approval>true</requires_approval>
</execute_command>
```

After updating the tool, provide the user with manual configuration instructions:

```xml
<ask_followup_question>
<question>**🔄 Upgrade Required - Manual Configuration Needed**

The Persona MCP Server has been updated. You now need to update your Cline configuration manually.

**Step 1: Open your `cline_mcp_settings.json` file**

The file is located at:
- **VS Code**: `%APPDATA%\Code\User\globalStorage\saoudrizwan.claude-dev\settings\cline_mcp_settings.json`
- **VS Code Insiders**: `%APPDATA%\Code - Insiders\User\globalStorage\saoudrizwan.claude-dev\settings\cline_mcp_settings.json`

**Step 2: Update the `personas` server configuration**

First, create a `.mcp/personas/` directory in your project if it doesn't exist:
```powershell
New-Item -ItemType Directory -Force -Path ".mcp\personas"
```

Then make sure your `personas` server entry looks like this (replace the path with your project's full path):

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

> **Note**: The `CUSTOM_PERSONAS_PATH` is required. Replace `C:\\path\\to\\your\\repo` with the actual path to your project.

**Step 3: Close ALL Visual Studio Code instances**

⚠️ **IMPORTANT**: You must close **ALL** VS Code windows (including any other projects), not just the current one. Then reopen VS Code.

Have you completed these steps?</question>
<options>["Yes, I've updated the config and closed all VS Code instances", "I need help finding the config file", "I'll use the local package instead"]</options>
</ask_followup_question>
```

If user needs help finding the config file:

```xml
<execute_command>
<command>powershell -Command "explorer \"$env:APPDATA\""</command>
<requires_approval>false</requires_approval>
</execute_command>
```

Then guide them to navigate to `Code\User\globalStorage\saoudrizwan.claude-dev\settings\` (or `Code - Insiders\...` for Insiders).

After user confirms they've updated and restarted, skip to Step 9 (Verify Personas Are Available).

## Step 3: Determine Installation Method

Ask about the installation source:

```xml
<ask_followup_question>
<question>How would you like to install the Persona MCP Server?

- **NuGet Feed**: Install from the msazure Azure DevOps artifact feed (requires msazure access)
- **Local Package**: Install from a `.nupkg` file you have on disk</question>
<options>["NuGet Feed (I have msazure access)", "Local Package (I have the .nupkg file)"]</options>
</ask_followup_question>
```

## Step 3A: Install from NuGet Feed

If user selected NuGet Feed, run:

```xml
<execute_command>
<command>powershell -Command "if (dotnet tool list -g | Select-String 'SilverMcp.Personas') { dotnet tool update -g SilverMcp.Personas --add-source https://pkgs.dev.azure.com/msazure/One/_packaging/Silver-MCP/nuget/v3/index.json } else { dotnet tool install -g SilverMcp.Personas --add-source https://pkgs.dev.azure.com/msazure/One/_packaging/Silver-MCP/nuget/v3/index.json }"</command>
<requires_approval>true</requires_approval>
</execute_command>
```

## Step 3B: Install from Local Package

If user selected Local Package, first ask for the path:

```xml
<ask_followup_question>
<question>Please provide the full path to the folder containing `SilverMcp.Personas.*.nupkg`.

Example: `C:\Downloads\persona-mcp-lab` or `C:\Users\me\Desktop\lab-files`</question>
</ask_followup_question>
```

Then install from that location. **Important**: Replace `USER_PROVIDED_PATH` with the actual path from the user's response:

```xml
<execute_command>
<command>powershell -Command "Push-Location 'USER_PROVIDED_PATH'; if (dotnet tool list -g | Select-String 'SilverMcp.Personas') { dotnet tool update -g SilverMcp.Personas --add-source . } else { dotnet tool install -g SilverMcp.Personas --add-source . }; Pop-Location"</command>
<requires_approval>true</requires_approval>
</execute_command>
```

## Step 4: Verify Installation

Confirm the tool was installed:

```xml
<execute_command>
<command>powershell -Command "dotnet tool list -g | Select-String 'SilverMcp.Personas'"</command>
<requires_approval>false</requires_approval>
</execute_command>
```

If the output shows `silvermcp.personas`, proceed to Step 5. If not found, ask:

```xml
<ask_followup_question>
<question>The tool installation could not be verified. This might be because:
1. The installation failed (check error messages above)
2. The PATH needs to be refreshed (restart VS Code)

Would you like to:
- Retry the installation
- Continue to configuration (if you believe it installed successfully)
- Stop and troubleshoot</question>
<options>["Retry installation", "Continue to configuration", "Stop and troubleshoot"]</options>
</ask_followup_question>
```

## Step 5: Create Custom Personas Directory

The Persona MCP Server requires a `CUSTOM_PERSONAS_PATH` environment variable. Create a `.mcp/personas/` directory in the project root:

First, get the current working directory path:

```xml
<execute_command>
<command>powershell -Command "(Get-Location).Path"</command>
<requires_approval>false</requires_approval>
</execute_command>
```

Then create the `.mcp/personas/` directory:

```xml
<execute_command>
<command>powershell -Command "New-Item -ItemType Directory -Force -Path '.mcp\personas'"</command>
<requires_approval>true</requires_approval>
</execute_command>
```

Store the full path to use in the configuration. The path will be `<current_directory>\.mcp\personas`.

This directory allows you to:
- Create project-specific personas stored in your repository
- Share custom personas with your team via git
- Override built-in personas with project-specific versions

## Step 6: Locate Cline Settings File

Determine where Cline settings are stored and get the full path:

```xml
<execute_command>
<command>powershell -Command "$vscodePath = \"$env:APPDATA\\Code\\User\\globalStorage\\saoudrizwan.claude-dev\\settings\"; $vscodeInsidersPath = \"$env:APPDATA\\Code - Insiders\\User\\globalStorage\\saoudrizwan.claude-dev\\settings\"; if (Test-Path $vscodePath) { Write-Host $vscodePath } elseif (Test-Path $vscodeInsidersPath) { Write-Host $vscodeInsidersPath } else { Write-Host 'Settings directory not found - Cline may not be installed' }"</command>
<requires_approval>false</requires_approval>
</execute_command>
```

## Step 6: Read Current Cline Configuration

Read the current Cline MCP settings file. Use the path from Step 5 output.

**For VS Code (regular):**
```xml
<execute_command>
<command>powershell -Command "Get-Content \"$env:APPDATA\\Code\\User\\globalStorage\\saoudrizwan.claude-dev\\settings\\cline_mcp_settings.json\" -ErrorAction SilentlyContinue"</command>
<requires_approval>false</requires_approval>
</execute_command>
```

**For VS Code Insiders:**
```xml
<execute_command>
<command>powershell -Command "Get-Content \"$env:APPDATA\\Code - Insiders\\User\\globalStorage\\saoudrizwan.claude-dev\\settings\\cline_mcp_settings.json\" -ErrorAction SilentlyContinue"</command>
<requires_approval>false</requires_approval>
</execute_command>
```

## Step 7: Update Cline Configuration

Update the Cline configuration file to add the `personas` server with the required `CUSTOM_PERSONAS_PATH`.

Replace `CUSTOM_PERSONAS_PATH` below with the full path from Step 5 (e.g., `C:\path\to\your\repo\.mcp\personas`).

The configuration should look like this:
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

---

**PowerShell commands to create/update the configuration:**

**If file is empty or doesn't exist:**

**For VS Code:**
```xml
<execute_command>
<command>powershell -Command "$customPath = 'CUSTOM_PERSONAS_PATH'; $config = @{ mcpServers = @{ personas = @{ type = 'stdio'; command = 'silver-persona-mcp-server'; args = @(); env = @{ CUSTOM_PERSONAS_PATH = $customPath }; disabled = $false; timeout = 60 } } }; $config | ConvertTo-Json -Depth 10 | Set-Content \"$env:APPDATA\\Code\\User\\globalStorage\\saoudrizwan.claude-dev\\settings\\cline_mcp_settings.json\""</command>
<requires_approval>true</requires_approval>
</execute_command>
```

**For VS Code Insiders:**
```xml
<execute_command>
<command>powershell -Command "$customPath = 'CUSTOM_PERSONAS_PATH'; $config = @{ mcpServers = @{ personas = @{ type = 'stdio'; command = 'silver-persona-mcp-server'; args = @(); env = @{ CUSTOM_PERSONAS_PATH = $customPath }; disabled = $false; timeout = 60 } } }; $config | ConvertTo-Json -Depth 10 | Set-Content \"$env:APPDATA\\Code - Insiders\\User\\globalStorage\\saoudrizwan.claude-dev\\settings\\cline_mcp_settings.json\""</command>
<requires_approval>true</requires_approval>
</execute_command>
```

**If file exists with other servers**, read the existing content, parse it as JSON, add the `personas` server to `mcpServers`, and write back:

**For VS Code:**
```xml
<execute_command>
<command>powershell -Command "$customPath = 'CUSTOM_PERSONAS_PATH'; $settingsPath = \"$env:APPDATA\\Code\\User\\globalStorage\\saoudrizwan.claude-dev\\settings\\cline_mcp_settings.json\"; $config = Get-Content $settingsPath -Raw | ConvertFrom-Json; if (-not $config.mcpServers) { $config | Add-Member -NotePropertyName 'mcpServers' -NotePropertyValue @{} }; $config.mcpServers | Add-Member -NotePropertyName 'personas' -NotePropertyValue @{ type = 'stdio'; command = 'silver-persona-mcp-server'; args = @(); env = @{ CUSTOM_PERSONAS_PATH = $customPath }; disabled = $false; timeout = 60 } -Force; $config | ConvertTo-Json -Depth 10 | Set-Content $settingsPath"</command>
<requires_approval>true</requires_approval>
</execute_command>
```

**For VS Code Insiders:**
```xml
<execute_command>
<command>powershell -Command "$customPath = 'CUSTOM_PERSONAS_PATH'; $settingsPath = \"$env:APPDATA\\Code - Insiders\\User\\globalStorage\\saoudrizwan.claude-dev\\settings\\cline_mcp_settings.json\"; $config = Get-Content $settingsPath -Raw | ConvertFrom-Json; if (-not $config.mcpServers) { $config | Add-Member -NotePropertyName 'mcpServers' -NotePropertyValue @{} }; $config.mcpServers | Add-Member -NotePropertyName 'personas' -NotePropertyValue @{ type = 'stdio'; command = 'silver-persona-mcp-server'; args = @(); env = @{ CUSTOM_PERSONAS_PATH = $customPath }; disabled = $false; timeout = 60 } -Force; $config | ConvertTo-Json -Depth 10 | Set-Content $settingsPath"</command>
<requires_approval>true</requires_approval>
</execute_command>
```

## Step 8: Restart Prompt

```xml
<ask_followup_question>
<question>Configuration complete! 🎉

**IMPORTANT**: You must restart VS Code completely (not just reload the window) for the MCP server to be recognized.

Please:
1. Close VS Code completely
2. Reopen VS Code
3. Open Cline
4. Return to this conversation

Have you restarted VS Code?</question>
<options>["Yes, I've restarted and I'm back", "I'll restart now"]</options>
</ask_followup_question>
```

## Step 9: Verify Personas Are Available

After user confirms restart, test the personas server by calling the list_personas tool:

```xml
<use_mcp_tool>
<server_name>personas</server_name>
<tool_name>list_personas</tool_name>
<arguments>{}</arguments>
</use_mcp_tool>
```

If the tool call succeeds and shows `bicep-planner` and `bicep-implementer`, the setup is complete. If the tool call fails, troubleshoot:

```xml
<ask_followup_question>
<question>The personas server doesn't appear to be responding. Let's troubleshoot:

1. Check if the server appears in Cline's MCP Servers list
2. Look for any error messages in the Cline output panel

What do you see?</question>
<options>["Server shows but has an error", "Server not in list", "Server shows and is green/connected", "I see an error message"]</options>
</ask_followup_question>
```

## Step 10: Setup Complete

```xml
<attempt_completion>
<result>
✅ **Setup Complete!**

The Persona MCP Server is now configured and ready to use.

**Available Personas for Labs:**
- `bicep-planner` - Creates infrastructure deployment plans  
- `bicep-implementer` - Implements Bicep templates from plans

---

## 🎯 Next Steps: Start a New Chat

**Important**: Before using the personas, start a fresh Cline conversation:

1. Click the **"+"** button in Cline to start a new chat
2. In the new chat, say: `Apply the bicep-planner persona`
3. Follow the prompts in `lab4-bicep-planner-prompt.md`

When you're ready for implementation:
1. Start another new chat
2. Say: `Apply the bicep-implementer persona`
3. Follow the prompts in `lab4-bicep-implementer-prompt.md`

Starting fresh ensures the persona has your full attention without setup noise!
</result>
</attempt_completion>
```

</detailed_sequence_of_steps>

<usage_instructions>

## How to Use This Workflow

### For Cline Users
1. Type `/setup-persona-mcp` in the Cline chat
2. Answer the prompts about installation method (NuGet feed or local package)
3. Follow the automated installation steps
4. Restart VS Code when prompted
5. Verify the personas are available
6. Start using the bicep-planner and bicep-implementer personas!

## Troubleshooting

### "Tool not found" Error
If `silver-persona-mcp-server` command is not found:
1. Verify installation: `dotnet tool list -g`
2. Check PATH includes: `%USERPROFILE%\.dotnet\tools`
3. Restart PowerShell/VS Code after installation

### Server Won't Start
1. Restart VS Code completely (not just reload)
2. Check the Cline/Copilot output panel for errors
3. Verify .NET 9.0 SDK: `dotnet --version`

### Authentication Issues (NuGet Feed)
If you get authentication errors with the NuGet feed:
- Use the Local Package option instead
- Ask the lab facilitator for the `.nupkg` file

### Configuration Not Working
- Ensure JSON syntax is valid (no trailing commas)
- Verify server name is exactly `personas`
- Check file is saved to correct location

## Next Steps After Setup

1. **Lab 4 - Planning**: Use `lab4-bicep-planner-prompt.md` with the `bicep-planner` persona
2. **Lab 4 - Implementation**: Use `lab4-bicep-implementer-prompt.md` with the `bicep-implementer` persona

## Quick Commands

```
# Check if tool is installed
dotnet tool list -g | Select-String 'SilverMcp.Personas'

# Reinstall tool (NuGet feed)
dotnet tool uninstall -g SilverMcp.Personas
dotnet tool install -g SilverMcp.Personas --add-source https://pkgs.dev.azure.com/msazure/One/_packaging/Silver-MCP/nuget/v3/index.json

# Reinstall tool (local package)
dotnet tool uninstall -g SilverMcp.Personas
cd "path\to\nupkg"
dotnet tool install -g SilverMcp.Personas --add-source .
```

</usage_instructions>
