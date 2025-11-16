# Custom AI Agents: Complete Guide

This guide provides comprehensive information on creating, testing, and deploying custom AI agents in the `.github-private` repository.

## Table of Contents

1. [Overview](#overview)
2. [Agent Profile Structure](#agent-profile-structure)
3. [Creating Your First Agent](#creating-your-first-agent)
4. [Testing Agents](#testing-agents)
5. [Releasing Agents](#releasing-agents)
6. [Best Practices](#best-practices)
7. [Troubleshooting](#troubleshooting)

## Overview

Custom AI agents extend GitHub Copilot with specialized knowledge and capabilities tailored to your organization's needs. They are defined as Markdown files with YAML frontmatter and stored in the `.github/agents` directory.

### Why Use Custom Agents?

- **Consistency**: Ensure all team members follow the same patterns and practices
- **Efficiency**: Automate repetitive tasks with specialized knowledge
- **Quality**: Encode best practices and organizational standards
- **Onboarding**: Help new team members learn your codebase faster
- **Specialization**: Create experts for specific domains or frameworks

## Agent Profile Structure

### Basic Template

```markdown
---
name: Agent Name
description: One-line description of what the agent does
tools:
  - shell
  - other-tool
---

# Agent Name Header

You are [role description].

## Core Responsibilities

[What the agent should do]

## Guidelines

[How the agent should behave]

## Examples

[Concrete examples of the agent's work]
```

### YAML Frontmatter Fields

#### `name` (required)
The display name of your agent. This is what users will see when selecting the agent.

```yaml
name: Documentation Specialist
```

#### `description` (required)
A brief, clear description of the agent's purpose. Keep it under 100 characters.

```yaml
description: Expert in creating and improving README files and documentation
```

#### `tools` (optional)
List of tools the agent can access. Common options:
- `shell`: Access to shell commands
- Custom MCP servers (if configured)

```yaml
tools:
  - shell
```

### Markdown Content

The Markdown content after the frontmatter contains the agent's instructions and personality. This is where you define:

1. **Role and Expertise**: What the agent specializes in
2. **Responsibilities**: Specific tasks the agent handles
3. **Guidelines**: How the agent should approach problems
4. **Examples**: Concrete examples of good outputs
5. **Constraints**: What the agent should NOT do

## Creating Your First Agent

### Step 1: Identify a Need

Think about repetitive tasks or specialized knowledge in your team:
- Do you have specific coding standards?
- Are there complex onboarding procedures?
- Do you use specialized frameworks?
- Are there common review patterns?

### Step 2: Create the Agent File

Create a new Markdown file in `.github/agents/`:

```bash
touch .github/agents/my-custom-agent.md
```

### Step 3: Write the Profile

Start with the template above and customize it:

```markdown
---
name: API Developer
description: Expert in building RESTful APIs with our organization's standards
tools:
  - shell
---

# API Developer Agent

You are an expert API developer familiar with our organization's API design standards and best practices.

## Core Responsibilities

- Design RESTful API endpoints following our conventions
- Implement proper error handling and status codes
- Write OpenAPI/Swagger documentation
- Ensure consistent response formats

## API Design Standards

### URL Structure
- Use plural nouns: `/api/v1/users` not `/api/v1/user`
- Use kebab-case: `/api/v1/user-profiles`
- Version in URL: `/api/v1/`

### Response Format
All responses must follow this structure:
```json
{
  "data": { /* response data */ },
  "meta": {
    "timestamp": "ISO-8601",
    "version": "1.0"
  }
}
```

### Error Handling
- Use standard HTTP status codes
- Include error details in response body
- Log errors with correlation IDs

## Examples

[Include specific examples from your codebase]
```

### Step 4: Commit the Agent

```bash
git add .github/agents/my-custom-agent.md
git commit -m "Add API Developer custom agent"
git push
```

## Testing Agents

### Local Testing

Agents in `.github-private` are automatically available to organization members with access to the repository.

### Testing Methods

#### 1. GitHub Copilot Chat (VSCode/IDE)
1. Open GitHub Copilot Chat
2. Look for the agent selector (@ symbol)
3. Select your custom agent
4. Test with various prompts

#### 2. GitHub Copilot CLI
```bash
# If using Copilot CLI with agent support
gh copilot suggest --agent my-custom-agent "create an API endpoint"
```

#### 3. In Pull Requests
Tag the agent in PR comments to get specialized reviews.

### Testing Checklist

- [ ] Agent responds appropriately to its domain
- [ ] Agent follows the guidelines you specified
- [ ] Agent declines out-of-scope requests gracefully
- [ ] Output quality matches expectations
- [ ] Agent uses tools correctly (if applicable)

## Releasing Agents

### From Testing to Production

Once your agent is thoroughly tested in `.github-private`:

1. **Validate** the agent works as expected
2. **Document** any special usage instructions
3. **Move** the agent file to organization-level `agents` directory
4. **Announce** the new agent to your team

### Organization-Wide Deployment

To make an agent available across all repositories:

1. Create/access your organization's main agents repository
2. Copy the agent file to `agents/` directory (not `.github/agents/`)
3. Commit and merge to the default branch
4. The agent becomes available org-wide

## Best Practices

### Writing Effective Agent Profiles

#### 1. Be Specific
❌ Bad: "You are a helpful coding assistant."
✅ Good: "You are a Python expert specializing in FastAPI development following our organization's microservices patterns."

#### 2. Provide Examples
Include concrete examples of good outputs:
```markdown
## Example Output

When asked to create an endpoint, format it like this:
[concrete example]
```

#### 3. Set Clear Boundaries
```markdown
## Out of Scope
- Database schema changes (requires DBA review)
- Authentication logic (use the Security Agent)
- Infrastructure changes (use the DevOps Agent)
```

#### 4. Include Context
Reference your organization's:
- Style guides
- Architecture decisions
- Common patterns
- Tool preferences

#### 5. Iterate Based on Feedback
- Monitor how the agent is used
- Collect feedback from users
- Update and refine regularly

### Security Considerations

1. **Don't Include Secrets**: Never put passwords, API keys, or sensitive data in agent profiles
2. **Limit Tool Access**: Only grant tools the agent truly needs
3. **Review Generated Code**: Agents are assistants, not replacements for code review
4. **Control Access**: Keep sensitive agents in `.github-private` if needed

### Performance Tips

1. **Keep Instructions Focused**: Longer profiles take more tokens
2. **Use Clear Structure**: Well-organized profiles perform better
3. **Prioritize Information**: Put most important info first
4. **Avoid Redundancy**: Don't repeat yourself

## Troubleshooting

### Agent Not Appearing

- **Check file location**: Must be in `.github/agents/` directory
- **Check filename**: Must be `.md` extension
- **Check permissions**: User must have access to `.github-private` repo
- **Check frontmatter**: YAML must be valid

### Agent Not Following Instructions

- **Be more specific**: Vague instructions lead to vague behavior
- **Add examples**: Show concrete examples of desired behavior
- **Check prompt length**: Very long profiles might be truncated
- **Test iteratively**: Start simple, add complexity gradually

### Agent Making Mistakes

- **Refine guidelines**: Add specific rules for common mistakes
- **Add negative examples**: Show what NOT to do
- **Set constraints**: Explicitly state limitations
- **Update based on usage**: Learn from real-world use

### YAML Syntax Errors

Common mistakes:
```yaml
# Wrong - missing quotes for special characters
description: Expert in API's and RESTful services

# Correct
description: "Expert in API's and RESTful services"

# Wrong - incorrect list syntax
tools:
- shell
- other

# Correct
tools:
  - shell
  - other
```

## Advanced Topics

### Multiple Agents Working Together

Design agents that complement each other:
- "Code Writer" + "Code Reviewer" + "Test Generator"
- "Frontend Expert" + "Backend Expert" + "DevOps Specialist"

### Using External Tools

Agents can access MCP (Model Context Protocol) servers for:
- Database access
- External API calls
- Custom tooling integration

### Dynamic Agents

Consider creating agents for:
- New projects (scaffold agent)
- Legacy code (migration agent)
- Specific releases (feature-specific agent)

## Resources

- [GitHub Official Documentation](https://docs.github.com/en/copilot)
- [Example Agent Profiles](.github/agents/)
- [Community Best Practices](https://github.com/topics/github-copilot)

## Getting Help

- Open an issue in this repository
- Discuss in team channels
- Contact your GitHub administrator

---

*Happy agent building! 🤖*
