# trigger

> Trigger.dev is an open source background jobs framework that lets you write reliable workflows in plain async code. Run long-running AI tasks, handle complex background jobs, and build AI agents with built-in queuing, automatic retries, and real-time monitoring. No timeouts, elastic scaling, and zero infrastructure management required.

I want you to install Trigger.dev for me. Execute all the steps below autonomously.

OBJECTIVE: Set up Trigger.dev in an existing Node.js/TypeScript project with a working example task.

DONE WHEN: The `npx trigger.dev@latest dev` command is running, the example task is registered, and you can see the dev server output with URLs to the Trigger.dev dashboard.

## TODO

- [ ] Run the CLI init command to set up Trigger.dev configuration and example task
- [ ] Install the "Hello World" example task when prompted
- [ ] Start the dev server with the CLI dev command
- [ ] Verify the dev server is running and tasks are registered

## Prerequisites

You need to have:
- An existing Node.js project with a `package.json` file
- TypeScript installed in the project
- A Trigger.dev account created at https://cloud.trigger.dev
- A project created in the Trigger.dev dashboard

## Task 1: Initialize Trigger.dev in your project

You must run the CLI init command in the root of your project. This will create the configuration file and example task.

Using npm:
```bash
npx trigger.dev@latest init
```

Using pnpm:
```bash
pnpm dlx trigger.dev@latest init
```

Using yarn:
```bash
yarn dlx trigger.dev@latest init
```

The init command will:
1. Log you into the CLI if not already logged in (opens browser for authentication)
2. Create a `trigger.config.ts` file in the project root
3. Ask where to create the `/trigger` directory
4. Create the `/trigger` directory with an example task at `/trigger/example.ts`

When prompted, you must install the "Hello World" example task.

## Task 2: Start the development server

You need to run the dev command to start the local task server. This watches for changes in your `/trigger` directory and communicates with the Trigger.dev platform.

Using npm:
```bash
npx trigger.dev@latest dev
```

Using pnpm:
```bash
pnpm dlx trigger.dev@latest dev
```

Using yarn:
```bash
yarn dlx trigger.dev@latest dev
```

The dev server will output URLs including a link to the Test page in the dashboard where you can trigger test runs.

## Task 3: Verify the setup

You must confirm the dev server is running successfully. Look for output showing:
- The dev server has started
- Your example task is registered
- URLs to the Trigger.dev dashboard are displayed

The terminal should show task registration and provide links to view runs in the dashboard.

## Optional: Set up concurrent development

If you want to run your app and Trigger.dev dev server together, add these scripts to `package.json`:

```json
{
  "scripts": {
    "trigger:dev": "npx trigger.dev@latest dev",
    "dev": "npx concurrently --kill-others --names \"app,trigger\" --prefix-colors \"yellow,blue\" \"your-app-dev-command\" \"npm run trigger:dev\""
  }
}
```

## Environment variable for triggering tasks

To trigger tasks from your application code, you need to set the `TRIGGER_SECRET_KEY` environment variable. Add it to your `.env.local` or `.env` file:

```bash
TRIGGER_SECRET_KEY=your-dev-secret-key
```

You can find this key in the Trigger.dev dashboard under API Keys (select the DEV secret key).

EXECUTE NOW: Complete the above TODO list to achieve: The `npx trigger.dev@latest dev` command is running, the example task is registered, and you can see the dev server output with URLs to the Trigger.dev dashboard.

---

> If you think the above is not enough to accomplish the task, you can find navigation and other pages relevant to this product by using the llms.txt file at: https://trigger.dev/docs/llms.txt