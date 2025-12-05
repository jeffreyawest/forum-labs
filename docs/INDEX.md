# Agentic Programming Workshop - Document Index

## Overview
This workshop teaches participants about agentic programming through hands-on labs with AI coding assistants (GitHub Copilot, Cline).

## Quick Links

### Main Documents
- [**AGENDA.md**](./AGENDA.md) - Complete workshop agenda, timing, and overview

### Lab Guides
| Lab | Title | Duration | Focus |
|-----|-------|----------|-------|
| [Lab 1](./labs/lab-01-vibe-coding.md) | Vibe Coding | 45 min | Iterative prompting |
| [Lab 2](./labs/lab-02-spec-driven.md) | Spec-Driven Development | 45 min | Specifications & context |
| [Lab 3](labs/lab03-mcp/lab-03-mcp-servers.md) | MCP Servers | 45 min | Tool integration |
| [Lab 4](labs/lab05-your-code/lab-05-plan-mode.md) | PLAN Mode & Memory | 35 min | Exploration & context stores |

### Supporting Materials
- [Weather App Spec](./specs/weather-app-spec.md) - Complete specification for Labs 1 & 2
- [Reference Implementation](../src/weather-app/) - Target weather app

## Workshop Summary

### Lab 1: Vibe Coding
Experience iterative AI development. Build a weather app with only high-level prompts to understand the challenges of unstructured prompting.

### Lab 2: Spec-Driven Development  
Build the same app with detailed specifications and context files. Compare time, iterations, and quality with Lab 1.

### Lab 3: MCP Servers
Create a custom MCP server to expose weather data as AI tools. Configure existing MCP servers (ADO, GitHub).

### Lab 4: PLAN Mode & Memory Banks
Use PLAN mode for codebase exploration. Build memory banks for project continuity across AI sessions.

## Key Learning Outcomes
1. Vibe coding vs. structured development trade-offs
2. Context engineering and specification writing
3. MCP protocol and server development
4. Effective use of AI planning modes
5. Building persistent context stores

---

## Original Requirements (Reference)

> The following was the original brief for this workshop:

1. Vibe coding a Weather Lookup app - given a stated goal, have the participants try to iteratively prompt Copilot or Cline to reproduce that result. The intent is to show that its possible, but iterative prompting without specific details takes more effort than providing a spec up-front. In the next lab, we will have them to the same with a spec.

2. Agentic Coding with Specs and Engineered Context - The goal here is to provide them a spec (possibly SpecKit) and/or set of context files in Markdown and have a Plan created with Cline's "deep-planning" tool, then have a better/faster/more-deterministic outcome

3. Create an MCP server and/or Configure/Use MCP Servers w/ Cline or Copilot - Given an API, or Storage Container of information (Context), create a context-providing MCP server with a set of operations. Also, configure the Microsoft ADO and/or AskESChat

4. Use Copilot/Cline in PLAN mode in your codebase, ask informed questions, create a memory bank / context store.
