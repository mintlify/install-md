# firecrawl

> Documentation and setup instructions for firecrawl

I want you to install Firecrawl for me. Execute all the steps below autonomously.

OBJECTIVE: Install the Firecrawl SDK and verify it works by scraping a webpage.

DONE WHEN: You have successfully scraped a URL and received markdown content back from the Firecrawl API.

## TODO

- [ ] Install the Firecrawl SDK (Python or Node)
- [ ] Set up the API key as an environment variable
- [ ] Create a test script that scrapes a webpage
- [ ] Run the script and verify markdown output is returned

## Installation

You need to install the Firecrawl SDK. Choose Python or Node based on your project:

**Python:**
```bash
pip install firecrawl-py
```

**Node:**
```bash
npm install @mendable/firecrawl-js
```

## API Key Setup

You must set your Firecrawl API key as an environment variable. The API key is required for all requests.

**On macOS/Linux:**
```bash
export FIRECRAWL_API_KEY="fc-YOUR-API-KEY"
```

**On Windows:**
```powershell
$env:FIRECRAWL_API_KEY="fc-YOUR-API-KEY"
```

Note: You need to obtain an API key from https://firecrawl.dev/app/api-keys before proceeding.

## Create Test Script

Your task is to create a test script that scrapes a webpage and outputs the result.

**Python - create `test_firecrawl.py`:**
```python
import os
from firecrawl import Firecrawl

firecrawl = Firecrawl(api_key=os.environ.get("FIRECRAWL_API_KEY"))

# Scrape a website
doc = firecrawl.scrape("https://firecrawl.dev", formats=["markdown"])
print(doc)
```

**Node - create `test_firecrawl.js`:**
```javascript
import Firecrawl from '@mendable/firecrawl-js';

const firecrawl = new Firecrawl({ apiKey: process.env.FIRECRAWL_API_KEY });

const doc = await firecrawl.scrape('https://firecrawl.dev', { formats: ['markdown'] });
console.log(doc);
```

## Run the Test

You must execute the test script to verify the installation works:

**Python:**
```bash
python test_firecrawl.py
```

**Node:**
```bash
node test_firecrawl.js
```

The response should contain a `markdown` field with the scraped content and a `metadata` object with page information.

## Additional Features

Once installation is verified, you can use these additional capabilities:

**Crawl entire websites:**
```python
docs = firecrawl.crawl(url="https://docs.firecrawl.dev", limit=10)
```

**Search the web:**
```python
results = firecrawl.search(query="firecrawl", limit=3)
```

**Extract structured data with JSON mode:**
```python
from pydantic import BaseModel

class CompanyInfo(BaseModel):
    company_mission: str
    is_open_source: bool

result = firecrawl.scrape(
    'https://firecrawl.dev',
    formats=[{"type": "json", "schema": CompanyInfo.model_json_schema()}]
)
```

## MCP Integration (Optional)

If you're using Claude Code, Cursor, or Windsurf, you can add Firecrawl as an MCP server:

**Claude Code:**
```bash
claude mcp add firecrawl -e FIRECRAWL_API_KEY=your-api-key -- npx -y firecrawl-mcp
```

**Cursor - add to MCP settings:**
```json
{
  "mcpServers": {
    "firecrawl": {
      "command": "npx",
      "args": ["-y", "firecrawl-mcp"],
      "env": {
        "FIRECRAWL_API_KEY": "your_api_key_here"
      }
    }
  }
}
```

EXECUTE NOW: Complete the above TODO list to achieve: Successfully scraped a URL and received markdown content back from the Firecrawl API.

---

> If you think the above is not enough to accomplish the task, you can find navigation and other pages relevant to this product by using the llms.txt file at: https://docs.firecrawl.dev/llms.txt