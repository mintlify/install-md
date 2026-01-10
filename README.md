---
title: "The /install.md file"
date: 2026-01-10
description: "A proposal to standardize on using an `/install.md` file to provide human-readable installation instructions that AI agents can execute safely and transparently."
---

## Background

Traditional installation scripts are often hundreds of lines of opaque shell commands that users pipe directly to bash without inspection. While convenient, this approach poses serious security risks and makes it difficult to audit what will actually happen on your system.

AI agents like Claude are increasingly capable of understanding natural language instructions and executing complex multi-step operations. However, they still require installation scripts to be executed through shell commands, inheriting the same security and transparency problems.

## Proposal

![install.md logo](logo.png){.lightbox width=150px .floatr}

We propose adding an `/install.md` markdown file to software projects to provide human-readable, AI-executable installation instructions. Instead of piping a shell script to bash, users can pipe an install.md file to an AI agent:

```bash
# Old way (opaque, hard to audit)
curl -fsSL https://example.com/install | bash

# New way (transparent, auditable)
curl -fsSL https://example.com/install.md | claude
```

The install.md file contains plain English instructions that describe what needs to happen, making it easy for both humans and AI agents to understand. Because the instructions are descriptive rather than prescriptive (shell commands), they:

- Are easier to audit for malicious intent
- Compress complex logic into concise, readable prose
- Can adapt to different environments without complex conditionals
- Remain accessible to non-technical users

## Format

The `install.md` file uses standard Markdown with a specific structure to provide clear, actionable installation instructions. The file should be located at `/install.md` in the root of a project's web presence.

A well-formed install.md file contains:

- An H1 with the name of the software being installed
- A blockquote with a brief summary of what the software does
- Clear, sequential installation instructions written in natural language
- Information about prerequisites, environment detection, and configuration
- Post-installation steps and verification instructions

### Example

Here's an example of an install.md file for a hypothetical tool:

```markdown
# Bun

> Bun is a fast JavaScript runtime, bundler, test runner, and package manager.

Install bun for me.

Detect my OS and CPU architecture, then download the appropriate bun binary zip from GitHub releases (oven-sh/bun). Use the baseline build if my CPU doesn't support AVX2. For Linux, use the musl build if I'm on Alpine. If I'm on an Intel Mac running under Rosetta, get the ARM version instead.

Extract the zip to ~/.bun/bin, make the binary executable, and clean up the temp files.

Update my shell config (.zshrc, .bashrc, .bash_profile, or fish config.fish depending on my shell) to export BUN_INSTALL=~/.bun and add the bin directory to my PATH. Use the correct syntax for my shell.

Try to install shell completions. Tell me what to run to reload my shell config.
```

## Advantages

### Security and Auditability

Traditional installation scripts can be hundreds of lines of complex shell code. Consider this typical pattern:

```bash
curl -fsSL https://example.com/install | bash
```

The script being executed might contain:
- Complex conditionals and error handling
- Nested function definitions
- System-specific workarounds
- Potentially harmful operations hidden in the noise

With install.md, the same installation becomes:

```markdown
Download the binary for my platform, extract it to ~/.local/bin,
and add that directory to my PATH.
```

This compression of logic into natural language makes intentions immediately clear and malicious behavior much harder to hide.

### Platform Adaptability

Shell scripts must explicitly handle every platform variation:

```bash
if [[ "$OSTYPE" == "linux-gnu"* ]]; then
    # Linux specific
elif [[ "$OSTYPE" == "darwin"* ]]; then
    # macOS specific
    if [[ $(uname -m) == "arm64" ]]; then
        # Apple Silicon
    else
        # Intel Mac
    fi
# ... many more cases
fi
```

An install.md instruction delegates this complexity to the AI agent:

```markdown
Detect my OS and architecture, then download the appropriate binary.
```

### Error Handling and Context

Shell scripts handle errors with explicit checks:

```bash
if ! command -v curl &> /dev/null; then
    echo "curl is required but not installed."
    exit 1
fi
```

Natural language instructions let the AI agent apply contextual intelligence:

```markdown
Download the release archive using curl, wget, or whatever download tool is available.
```

## Usage with AI Agents

Currently, install.md files can be used with AI assistants by copying the content and asking them to execute the instructions. The vision is to enable direct execution:

```bash
curl -fsSL https://example.com/install.md | claude
```

This requires:
1. A command-line interface for AI agents that can read from stdin
2. Appropriate safety guards and user confirmation before executing system-modifying operations
3. Clear output showing what actions are being taken

## Creating Effective install.md Files

When writing an install.md file:

- Use clear, direct language
- Organize instructions sequentially
- Specify environment detection needs upfront
- Include prerequisite checks
- Describe post-installation verification steps
- Mention common gotchas or platform-specific considerations
- Provide fallback options for common failure scenarios
- Keep the file concise (under 100 lines for most installations)

Avoid:
- Overly generic instructions that lack necessary detail
- Assumptions about the user's environment
- Jargon or unexplained technical terms
- Instructions that combine too many operations without clear steps

## Comparison with Existing Standards

### vs. Installation Scripts

Traditional shell scripts (`install.sh`) are:
- Platform-specific and require explicit handling of all edge cases
- Opaque and difficult to audit without shell scripting expertise
- Brittle and prone to failure in unexpected environments

install.md files are:
- Platform-agnostic with intelligence delegated to the AI agent
- Human-readable and easy to audit for intent
- Adaptable to various environments through natural language understanding

### vs. Package Managers

Package managers (apt, brew, npm, etc.) are:
- Excellent for their specific ecosystems
- Require the package to be published to a registry
- Handle dependency management and updates

install.md files are:
- Complementary to package managers (can describe package manager installation)
- Useful for software not in registries or requiring custom setup
- Focused on initial installation and setup, not ongoing management

### vs. Documentation

Traditional installation documentation is:
- Written for human readers to execute manually
- Often platform-specific with separate sections
- Can become outdated or inconsistent

install.md files are:
- Written for AI agents to execute (but readable by humans)
- Platform-agnostic with conditional logic expressed naturally
- Single source of truth that's also executable

## Community and Contributions

The install.md specification is open for community input. We welcome:

- Examples of install.md files for popular software
- Tools and integrations for processing install.md files
- Improvements to the specification
- Discussion of best practices and patterns

Visit the [GitHub repository](https://github.com/mintlify/install-md) to contribute or join the conversation.

## Future Directions

As AI agents become more capable and integrated into development workflows, we envision:

- Native support for install.md in AI coding assistants
- A registry or directory of install.md files for popular software
- Tools to validate and test install.md files across platforms
- Integration with package managers and CI/CD pipelines
- Standardized shebang support (`#!/usr/bin/env claude`) for executable markdown

The goal is to make software installation both more secure (through transparency) and more accessible (through natural language), while maintaining the convenience of automated installation.

## License

This specification and all associated documentation are released under the Apache License 2.0. See [LICENSE](LICENSE) for details.
