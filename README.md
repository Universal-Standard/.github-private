# .github-private

This is a special repository for the **Universal-Standard** organization that enables a powerful, lesser-known GitHub feature: **Custom AI Agents**.

## 🤖 Custom AI Agents Feature

The `.github-private` repository has a unique capability to host custom AI agent profiles that extend GitHub Copilot's functionality with organization-specific expertise and workflows.

### What Are Custom AI Agents?

Custom AI agents are specialized AI assistants that can be configured to understand your team's specific workflows, coding standards, and requirements. They appear as Markdown files with YAML frontmatter in the `.github/agents` directory.

### Key Benefits

- **🔒 Private & Secure**: Agents in `.github-private` are only accessible to organization members
- **🧪 Safe Testing**: Test and iterate on agents privately before releasing org-wide
- **🎯 Specialized Knowledge**: Create agents with domain-specific expertise
- **🔧 Tool Integration**: Agents can access shell commands and external tools
- **📦 Easy Deployment**: Move tested agents to organization-level when ready

## 📁 Repository Structure

```
.github-private/
├── README.md
└── .github/
    └── agents/
        ├── documentation-specialist.md
        ├── code-reviewer.md
        ├── testing-expert.md
        └── kubernetes-specialist.md
```

## 🚀 Available Custom Agents

### 1. Documentation Specialist
**File**: `.github/agents/documentation-specialist.md`

An expert in creating and improving README files and documentation. Use this agent when you need help with:
- Writing comprehensive README files
- Creating API documentation
- Improving documentation clarity
- Adding usage examples

### 2. Code Reviewer
**File**: `.github/agents/code-reviewer.md`

A specialized agent for conducting thorough code reviews with focus on:
- Code quality and maintainability
- Security vulnerabilities
- Performance optimization
- Testing coverage

### 3. Testing Expert
**File**: `.github/agents/testing-expert.md`

Focused on software testing and test-driven development:
- Writing unit and integration tests
- Ensuring test quality
- Following testing best practices
- Multiple language/framework support

### 4. Kubernetes Specialist
**File**: `.github/agents/kubernetes-specialist.md`

Expert in Kubernetes and container orchestration:
- Creating and validating K8s manifests
- Helm chart development
- Security best practices
- Resource optimization

## 📖 How to Use Custom Agents

### Testing Agents (Current Stage)

Agents in this `.github-private` repository are automatically available to organization members for testing:

1. **Via GitHub Copilot Chat**: Select the agent from the agent picker
2. **Via Copilot CLI**: Use `gh copilot` with agent selection
3. **In PRs and Issues**: Reference agents in conversations

### Releasing Agents Organization-Wide

Once an agent is tested and validated:

1. Move the agent profile from `.github-private/.github/agents/` to the organization's main `agents` directory
2. This makes the agent available across all repositories in the organization
3. All organization members can then access the agent

## 🛠️ Creating Your Own Custom Agent

### Agent Profile Structure

Each agent is a Markdown file with YAML frontmatter:

```markdown
---
name: Agent Name
description: Brief description of the agent's purpose
tools:
  - shell
  - other-tool
---

# Agent Name

You are a specialized AI agent focused on [specific domain].

## Core Responsibilities

- List key responsibilities
- Define scope of expertise

## Guidelines

1. Specific rules and principles
2. Best practices to follow
3. Quality standards

## Focus Areas

- Specific topics or tasks
- Technologies or frameworks

[Additional instructions and context...]
```

### Best Practices for Agent Profiles

1. **Clear Scope**: Define what the agent should and shouldn't do
2. **Specific Instructions**: Provide detailed guidelines and examples
3. **Consistency**: Maintain consistent tone and approach
4. **Tools Access**: Only grant necessary tool permissions
5. **Iterative Development**: Start simple, refine based on usage

## 🔍 Example Use Cases

### Onboarding New Developers
Create a "Developer Onboarding" agent that knows your team's setup process, coding standards, and common gotchas.

### Architecture Decisions
Build an "Architecture Advisor" agent familiar with your system design patterns and technology stack.

### Security Compliance
Develop a "Security Auditor" agent that checks code against your organization's security policies.

### Framework-Specific Helpers
Create agents for specific frameworks your team uses (React, Spring Boot, etc.) with your team's conventions.

## 📚 Additional Resources

- [GitHub Docs: Testing and releasing custom agents](https://docs.github.com/en/copilot/how-tos/use-copilot-agents/coding-agent/test-custom-agents)
- [GitHub Docs: Creating custom agents](https://docs.github.com/en/copilot/how-tos/use-copilot-agents/coding-agent/create-custom-agents)
- [GitHub Blog: Copilot CLI](https://github.blog/ai-and-ml/github-copilot-cli-101-how-to-use-github-copilot-from-the-command-line/)

## 🎯 Next Steps

1. Review the example agents in `.github/agents/`
2. Test these agents with your workflows
3. Create custom agents specific to your team's needs
4. Share feedback and iterate on agent designs
5. Release successful agents to the organization

---

**Note**: This feature is part of GitHub Copilot for Business/Enterprise and requires appropriate licensing and permissions.