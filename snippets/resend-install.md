# resend

> Documentation and setup instructions for resend

I want you to install Resend for me. Execute all the steps below autonomously.

OBJECTIVE: Set up Resend email API integration with a working email-sending capability.

DONE WHEN: You can successfully send a test email using the Resend API and receive a successful response with an email ID.

## TODO

- [ ] Install the Resend SDK
- [ ] Set up API key configuration
- [ ] Create a test email script
- [ ] Send a test email and verify the response

## Prerequisites

Before starting, you need a Resend API key. The user must provide this as an environment variable `RESEND_API_KEY`. If not available, inform the user they need to obtain one from https://resend.com/api-keys.

## Install the Resend SDK

You need to install the Resend SDK for your project. Choose the appropriate package manager:

```bash
npm install resend
```

Or with other package managers:

```bash
# Using yarn
yarn add resend

# Using pnpm
pnpm add resend

# Using bun
bun add resend
```

For Python projects:

```bash
pip install resend
```

## Configure API Authentication

You must set up the API key for authentication. The API key format is `re_xxxxxxxxx`.

Create or update your environment configuration:

```bash
export RESEND_API_KEY="re_xxxxxxxxx"
```

## Create a Test Email Script

Your task is to create a minimal script to verify the installation works. Create a file called `send-email.js`:

```javascript
import { Resend } from 'resend';

const resend = new Resend(process.env.RESEND_API_KEY);

async function main() {
  const { data, error } = await resend.emails.send({
    from: 'onboarding@resend.dev',
    to: ['delivered@resend.dev'],
    subject: 'Hello World',
    html: '<strong>It works!</strong>',
  });

  if (error) {
    console.error('Error:', error);
    return;
  }

  console.log('Email sent successfully!');
  console.log('Email ID:', data.id);
}

main();
```

For Python, create `send_email.py`:

```python
import resend
import os

resend.api_key = os.environ.get("RESEND_API_KEY")

params = {
    "from": "onboarding@resend.dev",
    "to": ["delivered@resend.dev"],
    "subject": "Hello World",
    "html": "<strong>It works!</strong>",
}

email = resend.Emails.send(params)
print(f"Email sent successfully! ID: {email['id']}")
```

## Send Test Email

You must execute the test script to verify everything works:

```bash
node send-email.js
```

Or for Python:

```bash
python send_email.py
```

A successful response looks like:

```json
{
  "id": "49a3999c-0ce1-4ea6-ab68-afcd6dc2e794"
}
```

## API Reference

The base URL for all API requests is:

```
https://api.resend.com
```

All requests require an Authorization header:

```
Authorization: Bearer re_xxxxxxxxx
```

## Verify with cURL (Alternative)

You can also verify the setup works using cURL directly:

```bash
curl -X POST 'https://api.resend.com/emails' \
  -H 'Authorization: Bearer '$RESEND_API_KEY'' \
  -H 'Content-Type: application/json' \
  -d '{
    "from": "onboarding@resend.dev",
    "to": ["delivered@resend.dev"],
    "subject": "Hello World",
    "html": "<strong>It works!</strong>"
  }'
```

EXECUTE NOW: Complete the above TODO list to achieve: Successfully send a test email using the Resend API and receive a successful response with an email ID.

---

> If you think the above is not enough to accomplish the task, you can find navigation and other pages relevant to this product by using the llms.txt file at: https://resend.com/docs/llms.txt