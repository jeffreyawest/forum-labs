# Agentic Programming Workshop

## Workshop Overview

This hands-on workshop teaches participants the principles and practices of **Agentic Programming** - leveraging AI coding assistants (GitHub Copilot, Cline) to accelerate software development through intelligent prompting, context engineering, and tool integration.

### Learning Objectives

By the end of this workshop, participants will be able to:

1. ✅ Understand the difference between "vibe coding" and structured agentic development
2. ✅ Create effective specifications and context files for deterministic AI outputs
3. ✅ Configure and use MCP (Model Context Protocol) servers for enhanced context
4. ✅ Use PLAN mode effectively for codebase exploration and informed development
5. ✅ Build and maintain context stores/memory banks for ongoing projects

---

## Agenda

| Time | Duration | Session | Description |
|------|----------|---------|-------------|
| 0:00 | 15 min | **Introduction** | Welcome, objectives, and environment setup verification |
| 0:15 | 45 min | **Lab 1: Vibe Coding** | Iterative prompting to build a Weather App |
| 1:00 | 10 min | **Break** | |
| 1:10 | 45 min | **Lab 2: Spec-Driven Development** | Same app with specs and engineered context |
| 1:55 | 15 min | **Debrief: Labs 1 vs 2** | Compare approaches, discuss learnings |
| 2:10 | 10 min | **Break** | |
| 2:20 | 45 min | **Lab 3: MCP Servers** | Create and configure MCP servers |
| 3:05 | 10 min | **Break** | |
| 3:15 | 35 min | **Lab 4: PLAN Mode & Memory** | Intelligent codebase exploration |
| 3:50 | 10 min | **Wrap-up** | Q&A, resources, next steps |

**Total Duration: ~4 hours**

---

## Prerequisites

### Required Software
- [ ] VS Code (latest version)
- [ ] GitHub Copilot extension (with active subscription)
- [ ] Cline extension (latest version)
- [ ] Node.js 18+ (for MCP server lab)
- [ ] Git

### Recommended Setup
- [ ] OpenWeatherMap API key (free tier) - [Get one here](https://openweathermap.org/api)
- [ ] Azure DevOps access (for MCP configuration)
- [ ] Python 3.10+ (optional, for alternative implementations)

### Environment Verification
Run this in your terminal to verify setup:
```bash
node --version    # Should be 18+
code --version    # VS Code installed
git --version     # Git installed
```

---

## Labs Overview

### 🌊 Lab 1: Vibe Coding - The Iterative Approach
**Goal:** Experience the challenges of unstructured AI-assisted development

Build a Weather App using only high-level prompts. Discover how iterative prompting without specifications leads to:
- More back-and-forth iterations
- Inconsistent results
- Missing requirements
- Style/design drift

📄 [Lab 1 Guide](./labs/lab-01-vibe-coding.md)

---

### 📋 Lab 2: Agentic Coding with Specs
**Goal:** Experience structured, deterministic AI-assisted development

Build the **same Weather App** using:
- Detailed specifications (SpecKit format)
- Engineered context files
- Cline's "Deep Planning" feature
- Structured prompts

Compare time, iterations, and output quality with Lab 1.

📄 [Lab 2 Guide](./labs/lab-02-spec-driven.md)

---

### 🔌 Lab 3: MCP Server Development
**Goal:** Extend AI capabilities through custom context providers

Learn to:
- Create an MCP server from scratch
- Expose API data as AI-accessible tools
- Configure existing MCP servers (ADO, AskESChat)
- Understand the MCP protocol

📄 [Lab 3 Guide](labs/lab03-mcp/lab-03-mcp-servers.md)

---

### 🧠 Lab 4: PLAN Mode & Memory Banks
**Goal:** Master intelligent codebase exploration and context management

Learn to:
- Use Copilot/Cline in PLAN mode
- Ask informed questions about codebases
- Create and maintain memory banks
- Build persistent context stores

📄 [Lab 4 Guide](labs/lab05-your-code/lab-05-plan-mode.md)

---

## Key Concepts

### What is Agentic Programming?

**Agentic Programming** is a development paradigm where AI assistants act as intelligent agents that:
- Understand context deeply
- Make informed decisions
- Execute multi-step tasks
- Maintain state and memory
- Access external tools and data sources

### The Spectrum of AI-Assisted Development

```
┌─────────────────────────────────────────────────────────────────────┐
│                                                                      │
│   VIBE CODING          STRUCTURED            AGENTIC                │
│   (Lab 1)              (Lab 2)               (Labs 3-4)             │
│                                                                      │
│   "Make it work"       "Here's the spec"     "Here's the context,   │
│                                               tools, and goals"      │
│                                                                      │
│   ❌ Unpredictable     ✅ Deterministic      ✅ Intelligent          │
│   ❌ Iterative         ✅ First-time right   ✅ Adaptive             │
│   ❌ Inconsistent      ✅ Consistent         ✅ Context-aware        │
│                                                                      │
└─────────────────────────────────────────────────────────────────────┘
```

### The Context Engineering Pyramid

```
                    ┌─────────────┐
                    │   TOOLS     │  ← MCP Servers, APIs
                    │   (Lab 3)   │
                    ├─────────────┤
                    │   MEMORY    │  ← Context stores, history
                    │   (Lab 4)   │
                    ├─────────────┤
                    │    SPECS    │  ← Requirements, constraints
                    │   (Lab 2)   │
                    ├─────────────┤
                    │   PROMPTS   │  ← Instructions, goals
                    │   (Lab 1)   │
                    └─────────────┘
```

---

## Resources

### Documentation
- [GitHub Copilot Docs](https://docs.github.com/en/copilot)
- [Cline Documentation](https://github.com/cline/cline)
- [MCP Protocol Specification](https://modelcontextprotocol.io/)
- [OpenWeatherMap API](https://openweathermap.org/api)

### Sample Code
- [Weather App Reference](../src/weather-app/) - The target implementation for Labs 1 & 2

### Further Learning
- Context Engineering best practices
- SpecKit specification format
- Advanced MCP server patterns

---

## Instructor Notes

### Timing Adjustments
- Labs can be shortened by 10-15 min each for a 3-hour workshop
- Lab 3 (MCP) can be split into "Create" and "Configure" for flexibility
- Include buffer time for environment issues

### Common Issues
1. **API Key Problems**: Have backup keys ready
2. **Extension Issues**: Verify extensions before starting
3. **Permission Errors**: Check workspace trust settings

### Discussion Points
- After Lab 1: "What was frustrating? What worked?"
- After Lab 2: "How did the experience differ?"
- After Lab 3: "Where would MCP servers help in your work?"
- After Lab 4: "How would you apply this to your codebase?"

