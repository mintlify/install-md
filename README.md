# install.md

A proposal to standardize software installation using task-oriented markdown files that AI agents execute autonomously.

## The Problem

When you ask an AI agent to install software today, you have no idea what context it receives—it might search the web, find outdated docs, or hallucinate commands. With install.md, developers define exactly what instructions the agent gets.

## The Solution

![install.md logo](logo.png)

Add an `/install.md` markdown file to your project with task-oriented installation instructions. install.md files are **direct commands**, not documentation—structured to trigger immediate autonomous execution.

```bash
# Pipe directly to an AI agent
curl -fsSL https://example.com/install.md | claude

# Or paste into any coding assistant like Claude Code or Cursor
```

## Why install.md?

- **Verifiable**: Developers and users know exactly what context the AI agent receives. Test it yourself, iterate on it, trust it.
- **Adaptable**: AI agents adapt instructions to your environment—detecting your OS, package manager, project structure, and more.
- **Verifies success**: install.md files include success criteria so the agent knows when installation is complete and working.
- **Human-readable**: See exactly what will happen before it happens. Modify the instructions yourself if needed.

## Benefits

**For developers**: Define installation once, it adapts to every environment. Encode edge cases and troubleshooting knowledge. Control exactly what context the LLM receives.

**For users**: A single command installs software, or paste the file into any LLM. Human-readable instructions you can review before execution. Adapts to your specific environment automatically.

**For agents**: Instructions live in a predictable location. Structured format with clear success criteria. Clean markdown input, not HTML.

## Format

The `install.md` file uses standard Markdown with a required structure designed to trigger autonomous execution:

1. **H1 Title** - Lowercase, hyphenated identifier (e.g., `# firecrawl`)
2. **Blockquote Summary** - Brief description of what the software does
3. **Conversational Opening** - "I want you to install [product] for me. Execute all the steps below autonomously."
4. **OBJECTIVE** - Concise goal statement
5. **DONE WHEN** - Specific, measurable success condition (e.g., "server running at localhost:3000")
6. **TODO Section** - Markdown checkboxes (3-7 items) listing core tasks
7. **Detailed Steps** - Sequential instructions with explicit commands
8. **EXECUTE NOW Closing** - "EXECUTE NOW: Complete the above TODO list to achieve: [restate DONE WHEN]"
9. **llms.txt Reference** - Optional link to llms.txt for additional context

Use task language throughout: "You need to...", "You must...", "Your task is to..."

### Examples

Live install.md files from production documentation:

- [Firecrawl](https://docs.firecrawl.dev/install.md) - Web scraping API for LLMs
- [Mintlify](https://mintlify.com/docs/install.md) - Documentation platform
- [Trigger.dev](https://trigger.dev/docs/install.md) - Background jobs framework
- [Browserbase](https://docs.browserbase.com/install.md) - Browser automation platform
- [Resend](https://resend.com/docs/install.md) - Email API

## What to Include

- All shell commands needed for the core workflow
- Installation commands for relevant platforms/package managers
- Verification commands (--version, health checks)
- Commands to create and run a minimal working example

## What to Omit

- Troubleshooting sections (save for llms.txt)
- Optional/advanced features
- GUI-only steps (unless required before any local functionality)
- Alternative installation methods (pick the most reliable one)
- Lengthy explanations (show commands, not concepts)

## Relationship to llms.txt

install.md works naturally with [llms.txt](https://llmstxt.org/). While llms.txt helps LLMs understand your software broadly, install.md tells them specifically how to install it. Your install.md can link to your llms.txt so the agent can reference it for troubleshooting or additional context.

## Existing Standards

install.md complements existing installation methods:

- **Shell scripts** (`install.sh`) execute identically regardless of environment. install.md provides instructions that AI agents interpret and adapt.
- **Package managers** remain preferred for simple package installation. install.md handles what they don't: custom configuration, multi-step setup, cross-platform installation, and verification.

install.md is useful for complex installations, SDK integrations that modify code, and setups where verification and success criteria matter.

## Integrations

- [Mintlify](https://mintlify.com) - Documentation platform with built-in install.md support. Mintlify-hosted docs automatically generate and serve install.md files.

## Resources

- [Full documentation](https://installmd.org) - Format specification, examples, and guides
- [Skills for AI tools](https://installmd.org/essentials/skills) - Generate install.md files in Claude Code, Cursor, and Windsurf

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for how to add examples, improve the docs, or build integrations.
