# browserbase

> Documentation and setup instructions for browserbase

I want you to install Browserbase for me. Execute all the steps below autonomously.

OBJECTIVE: Set up Browserbase with the Functions SDK to deploy serverless browser automation workflows.

DONE WHEN: Local development server is running at `http://127.0.0.1:14113` and you can successfully invoke a function that scrapes Hacker News headlines.

## TODO

- [ ] Initialize a new Browserbase Functions project using the CLI
- [ ] Configure environment variables with Browserbase credentials
- [ ] Start the local development server
- [ ] Test the function by invoking it via curl
- [ ] Verify the function returns scraped data successfully

## Step 1: Initialize the Functions Project

You need to create a new Browserbase Functions project using the SDK CLI. This will set up a TypeScript project with all required dependencies and a starter function.

```bash
pnpm dlx @browserbasehq/sdk-functions init my-functions-project
```

Then enter the project directory:

```bash
cd my-functions-project
```

## Step 2: Configure Environment Variables

You must populate the `.env` file with your Browserbase credentials. Open the `.env` file and add:

```bash
BROWSERBASE_PROJECT_ID=your_project_id
BROWSERBASE_API_KEY=your_api_key
```

Note: The user needs to obtain these credentials from https://www.browserbase.com/settings - this is a manual step requiring web access.

## Step 3: Review the Starter Function

The CLI creates a template function in `index.ts` that connects to a browser session, navigates to Hacker News, and extracts the top 3 results. The function is already defined and ready to use.

## Step 4: Start the Development Server

You need to start the local development server to test your function:

```bash
pnpm bb dev index.ts
```

The server will start on `http://127.0.0.1:14113` and watch for file changes.

## Step 5: Test the Function

You must invoke your function locally to verify it works. In a separate terminal, run:

```bash
curl -X POST http://127.0.0.1:14113/v1/functions/my-function/invoke \
  -H "Content-Type: application/json"
```

This will create a Browserbase session, run the automation locally, and return the scraped Hacker News headlines as JSON.

For readable output, pipe through jq:

```bash
curl -X POST http://127.0.0.1:14113/v1/functions/my-function/invoke \
  -H "Content-Type: application/json" | jq
```

## Step 6: Publish to Browserbase Cloud (Optional)

Once your function works locally, you can publish it to Browserbase's cloud infrastructure:

```bash
pnpm bb publish index.ts
```

This bundles your project and deploys it. The output will include a Function ID and invoke URL for calling your deployed function via API.

To invoke a deployed function:

```bash
curl --request POST \
     --url https://api.browserbase.com/v1/functions/YOUR_FUNCTION_ID/invoke \
     --header 'Content-Type: application/json' \
     --header 'x-bb-api-key: YOUR_API_KEY' \
     --data '{"params": {}}'
```

EXECUTE NOW: Complete the above TODO list to achieve: Local development server running at `http://127.0.0.1:14113` with successful function invocation returning scraped Hacker News data.

---

> If you think the above is not enough to accomplish the task, you can find navigation and other pages relevant to this product by using the llms.txt file at: https://docs.browserbase.com/llms.txt