---
title: "The /install.md file"
date: 2026-01-10
description: "A proposal to standardise on using an `/install.md` file to provide human-readable installation instructions that AI agents can execute safely and transparently."
---

## Background

Software installation typically relies on shell scripts that users pipe directly to bash without inspection. While convenient, these scripts are often hundreds of lines of opaque commands containing complex conditionals, error handling, and system-specific workarounds that make auditing for malicious behavior extremely difficult.

AI agents are increasingly capable of understanding natural language instructions and executing complex multi-step operations. By providing installation instructions in human-readable prose rather than shell scripts, we can make software installation both more transparent (easy to audit) and more adaptable (AI agents can handle platform variations intelligently).

## Proposal

![install.md logo](logo.png){.lightbox width=150px .floatr}

We propose adding an `/install.md` markdown file to software projects to provide human-readable, AI-executable installation instructions. This file offers clear, sequential instructions that describe what needs to happen rather than prescribing specific shell commands.

install.md is human and AI readable, and uses a simple markdown format that's easy to audit at a glance.

Instead of piping opaque scripts to bash, users could pipe readable markdown to an AI agent:

```bash
# Traditional approach (opaque)
curl -fsSL https://bun.sh/install | bash

# install.md approach (transparent)
curl -fsSL https://bun.sh/install.md | claude
```

The [Mintlify documentation platform](https://mintlify.com) includes built-in support for install.md files. For instance, Mintlify-hosted documentation sites automatically provide an install.md file at `/install.md` that contains installation instructions for the documented software.

This proposal does not include any particular recommendation for how AI agents should process the install.md file, since it will depend on the application and the capabilities of the agent. The key benefit is transparency - users can read and understand what will happen before it happens, and malicious intent is much harder to hide in plain English than in complex shell scripts.

The versatility of install.md files means they can serve many purposes - from helping developers install command-line tools, to guiding users through complex application setup, or even orchestrating multi-component system installations. They're just as useful for simple single-binary installations as they are for elaborate setups requiring configuration, dependencies, and post-installation verification.

## Format

The `install.md` file uses standard Markdown with natural language instructions that describe the installation process. The format prioritizes human readability while remaining unambiguous enough for AI agents to execute reliably.

The install.md file spec is for files located at the root path `/install.md` of a project's website. A file following the spec contains the following sections as markdown, in the specific order:

- An H1 with the name of the software being installed. This is the only required section
- A blockquote with a brief summary of what the software does
- Sequential installation instructions written in natural language, organized into paragraphs describing each major step
- Environment detection guidance (OS, architecture, available tools)
- Post-installation verification steps

Here is a mock example:

```markdown
# Tool Name

> Brief description of what the tool does

Install the tool for me.

Detect my operating system and architecture, then download the appropriate
binary from GitHub releases (username/repo).

Extract the archive to ~/.local/bin and make the binary executable.

Add ~/.local/bin to my PATH if it's not already there.

Verify the installation with: toolname --version
```

The key principle is to describe *what* needs to happen, not *how* to do it with specific commands. This allows AI agents to adapt to different environments, handle edge cases intelligently, and use available tools flexibly.

## Existing standards

install.md is designed to complement existing installation methods. Traditional installation approaches include shell scripts, package managers, and manual documentation. Each has trade-offs that install.md addresses differently.

Shell scripts (`install.sh`, `curl | bash`) are the most direct parallel to install.md. install.md and shell scripts have different purposes---shell scripts provide explicit commands that execute identically regardless of who runs them, while install.md provides instructions that AI agents interpret and adapt to the specific environment. Our expectation is that install.md will mainly be useful when users want transparency and adaptability, particularly for tools distributed outside package manager ecosystems.

Package managers (apt, brew, npm, etc.) remain the preferred installation method when available. This isn't a substitute for install.md since:

- Many tools aren't available in package managers
- Package managers don't handle custom configuration or multi-step setup
- Cross-platform installation often requires users to know which package manager to use
- Some installations require additional steps beyond package installation

## Example

Here's an example of `install.md`, in this case for a hypothetical tool called ripgrep:

```markdown
# ripgrep

> ripgrep is a line-oriented search tool that recursively searches your current directory for a regex pattern.

Install ripgrep for me.

Use the most appropriate installation method for my system:

Package manager (recommended):
- macOS: brew install ripgrep
- Ubuntu/Debian: sudo apt-get install ripgrep
- Fedora: sudo dnf install ripgrep
- Arch: sudo pacman -S ripgrep
- Windows: choco install ripgrep or scoop install ripgrep

If no package manager is available, download the binary:

Detect my OS and architecture, then download the appropriate archive from GitHub releases (BurntSushi/ripgrep). Look for the latest release.

For Linux: Get the .tar.gz file matching my architecture
For macOS: Get the .tar.gz file matching my architecture
For Windows: Get the .zip file

Extract the archive to a temporary directory, then copy the 'rg' binary to a permanent location:
- Linux/macOS: Copy to ~/.local/bin (create if it doesn't exist)
- Windows: Copy to %LOCALAPPDATA%\Programs\ripgrep

Make sure the installation directory is in my PATH. Add it if needed.

Clean up the temporary files.

Verify the installation: rg --version

Optional: Install shell completions if my shell supports them. The completions are in the archive under 'complete/' directory.
```

To create effective `install.md` files, consider these guidelines:

- Use clear, direct language that describes intent
- Provide fallback options for different scenarios
- Include environment detection guidance
- Mention prerequisites and verification steps
- Keep instructions sequential and organized

## Integrations

Various tools and platforms are available to help integrate the install.md specification into your workflow:

- [Mintlify](https://mintlify.com) - Documentation platform with built-in install.md support. Mintlify-hosted docs automatically generate and serve install.md files for documented software.

## Next steps

The `install.md` specification is open for community input. A [GitHub repository](https://github.com/mintlify/install-md) hosts [this informal overview](https://github.com/mintlify/install-md/blob/main/README.md), allowing for version control and public discussion. A [community discussion board](https://github.com/mintlify/install-md/discussions) is available for sharing implementation experiences and discussing best practices.
