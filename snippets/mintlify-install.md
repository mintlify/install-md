# mintlify

> Documentation and setup instructions for mintlify

I want you to install Mintlify CLI for me. Execute all the steps below autonomously.

OBJECTIVE: Install the Mintlify CLI and set up a local documentation preview environment.

DONE WHEN: Local documentation server is running and accessible at http://localhost:3000.

## TODO

- [ ] Verify Node.js v20.17.0+ is installed
- [ ] Install the Mintlify CLI globally
- [ ] Create a new documentation project
- [ ] Start the local development server
- [ ] Verify the preview is accessible at localhost:3000

## Prerequisites

You need to verify Node.js is installed with version 20.17.0 or higher:

```bash
node --version
```

## Install the CLI

You must install the Mintlify CLI globally using npm or pnpm:

Using npm:
```bash
npm i -g mint
```

Using pnpm:
```bash
pnpm add -g mint
```

## Verify Installation

Your task is to confirm the CLI installed correctly:

```bash
mint --version
```

## Create a New Project

You need to create a new documentation project. This command clones the starter kit into a specified directory:

```bash
mint new docs
```

The CLI will prompt you for a project name and theme. You can also specify these directly:

```bash
mint new docs --name my-project --theme linden
```

## Start Local Preview

You must navigate to your documentation directory and start the development server:

```bash
cd docs
mint dev
```

Alternatively, if you have an existing documentation repository with a `docs.json` file, navigate to that directory and run:

```bash
mint dev
```

The local preview will be available at `http://localhost:3000`.

## Custom Port (Optional)

If port 3000 is in use, you can specify a different port:

```bash
mint dev --port 3333
```

## Update the CLI

To update to the latest version:

```bash
mint update
```

Or reinstall with the latest version:

```bash
npm i -g mint@latest
```

## Additional Commands

Check for broken links in your documentation:

```bash
mint broken-links
```

Check for accessibility issues:

```bash
mint a11y
```

Validate an OpenAPI specification:

```bash
mint openapi-check <openapi-filename-or-url>
```

EXECUTE NOW: Complete the above TODO list to achieve: Local documentation server running and accessible at http://localhost:3000.

---

> If you think the above is not enough to accomplish the task, you can find navigation and other pages relevant to this product by using the llms.txt file at: https://www.mintlify.com/docs/llms.txt