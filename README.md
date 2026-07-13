# Puppetry — AI Talking Head Video API, SDK & MCP Server

[![npm sdk](https://img.shields.io/npm/v/%40puppetry.com%2Fsdk?label=%40puppetry.com%2Fsdk)](https://www.npmjs.com/package/@puppetry.com/sdk)
[![npm mcp-server](https://img.shields.io/npm/v/%40puppetry.com%2Fmcp-server?label=%40puppetry.com%2Fmcp-server)](https://www.npmjs.com/package/@puppetry.com/mcp-server)
[![MCP Registry](https://img.shields.io/badge/MCP_Registry-com.puppetry%2Fmcp--server-blue)](https://registry.modelcontextprotocol.io)

Turn any **portrait photo + a script into a talking-head AI video** — from your
code, your AI agent, or your terminal. [Puppetry](https://www.puppetry.com) is a
**text-to-video and lip-sync API** with hundreds of AI voices in 29 languages.

Works with **Claude Desktop, OpenAI Codex CLI, Cursor**, and any
[MCP](https://modelcontextprotocol.io) client — or directly via the
**TypeScript SDK** and REST API.

## Quick start (MCP server)

Get an API key at [puppetry.com/developer](https://www.puppetry.com/developer)
(keys look like `pk_live_…`; plans include monthly API video credits).

**Claude Desktop** — add to `claude_desktop_config.json`
([example](examples/claude-desktop.json)):

```json
{
  "mcpServers": {
    "puppetry": {
      "command": "npx",
      "args": ["-y", "@puppetry.com/mcp-server"],
      "env": { "PUPPETRY_API_KEY": "pk_live_..." }
    }
  }
}
```

**OpenAI Codex CLI** — add to `~/.codex/config.toml`
([example](examples/codex-config.toml)):

```toml
[mcp_servers.puppetry]
command = "npx"
args = ["-y", "@puppetry.com/mcp-server"]
env = { PUPPETRY_API_KEY = "pk_live_..." }
```

**Cursor** — same JSON as Claude Desktop in `.cursor/mcp.json`.

Then ask your agent: *"Make this photo say 'Welcome to our launch!' in a warm
English voice."* It lists voices, creates the video job, polls until rendered,
and returns the video URL.

### MCP tools

`puppetry_create_video_from_text` · `puppetry_create_video_from_audio` ·
`puppetry_lipsync` · `puppetry_list_voices` · `puppetry_create_audio_upload_url`
· `puppetry_get_job_status` · `puppetry_get_quota`

## Quick start (TypeScript SDK)

```bash
npm install @puppetry.com/sdk
```

```ts
import { Puppetry } from "@puppetry.com/sdk";

const puppetry = new Puppetry({ apiKey: process.env.PUPPETRY_API_KEY! });

const job = await puppetry.videos.createFromText({
  image_url: "https://example.com/portrait.png",
  text: "Hello from Puppetry.",
  voice_id: "puppetry-af_heart",
});
const video = await job.waitForCompletion();
console.log(video.video_url); // hosted MP4
```

The SDK also exports `PUPPETRY_AGENT_TOOLS` (a ready-made tool manifest for
LLM function calling) and an MCP stdio handler.

## REST API

- Full OpenAPI spec: https://www.puppetry.com/openapi.json
- Flat variant for GPT builders: https://www.puppetry.com/openapi-gpt.json
- Agent guide + curl quickstarts: https://www.puppetry.com/for-agents
- `llms.txt`: https://www.puppetry.com/llms.txt

## Pricing

Video jobs are credit-backed: subscriptions include monthly API video credits
(Studio 10/month), and top-up packs start at $4.99 for 5 videos. When credits
run out, the API's 402 response includes a `checkout_url` your agent can hand
to its user. Voice/TTS uses plan characters (100k/month with Studio).

## Use cases

AI avatar videos · product demo narrators · personalized outreach videos ·
educational explainers · multilingual talking-head localization ·
agent-generated video replies.

> This repository hosts documentation, client configuration examples, and
> registry manifests. Package artifacts ship on npm; the service is
> [puppetry.com](https://www.puppetry.com). Support: support@puppetry.com
