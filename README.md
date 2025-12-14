# cf_ai_chat_agent

An AI-powered chat application built on Cloudflare's platform, featuring Llama 3.3 for natural language processing, real-time chat interface, and persistent state management.

## Project Overview

This application demonstrates a complete AI-powered chat system built entirely on Cloudflare infrastructure:

- **LLM**: Llama 3.3 70B (via Workers AI - `@cf/meta/llama-3.3-70b-instruct-fp8-fast`)
- **Workflow/Coordination**: Cloudflare Workers for serverless compute
- **User Input**: React-based chat interface with real-time streaming
- **Memory/State**: Durable Objects with SQLite for persistent chat history

## Features

- 💬 Real-time AI chat with streaming responses
- 🧠 Powered by Llama 3.3 70B on Workers AI (free tier)
- 🔄 Persistent chat history using Durable Objects
- 🛠️ Tool system with human-in-the-loop confirmation
- 📅 Task scheduling (one-time, delayed, and recurring)
- 🌓 Dark/Light theme support
- 🎨 Modern, responsive UI built with React

## Architecture

```
┌─────────────────┐
│  React Frontend │  ← User input via chat interface
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ Cloudflare      │  ← Workflow coordination
│ Workers         │
└────────┬────────┘
         │
         ├──────────────┐
         ▼              ▼
┌─────────────┐  ┌──────────────┐
│ Workers AI  │  │   Durable    │
│ (Llama 3.3) │  │   Objects    │  ← State/Memory
└─────────────┘  └──────────────┘
```

## Prerequisites

- [Cloudflare account](https://dash.cloudflare.com/sign-up)
- Node.js 18+ and npm

## Running Locally

1. **Clone the repository**
   ```bash
   git clone https://github.com/MatthewBarghout/cf_ai_chat_agent.git
   cd cf_ai_chat_agent
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Start the development server**
   ```bash
   npm start
   ```

4. **Open your browser**

   Navigate to `http://localhost:5173/`

That's it! No API keys needed - Workers AI is free on Cloudflare.

## Deploying to Cloudflare

1. **Login to Cloudflare**
   ```bash
   npx wrangler login
   ```

2. **Deploy**
   ```bash
   npm run deploy
   ```

3. **Access your app**

   Your app will be deployed to `https://cloudflare-agent.<your-subdomain>.workers.dev`

## Project Structure

```
├── src/
│   ├── app.tsx        # React chat UI
│   ├── server.ts      # Chat agent logic (Workers AI integration)
│   ├── tools.ts       # Tool definitions for agent
│   ├── utils.ts       # Helper functions
│   └── styles.css     # UI styling
├── wrangler.jsonc     # Cloudflare Workers configuration
└── package.json       # Dependencies
```

## Key Components

### 1. LLM Integration (src/server.ts)
Uses Workers AI with Llama 3.3 for natural language processing:
```typescript
const workersai = createWorkersAI({ binding: this.env.AI });
const model = workersai("@cf/meta/llama-3.3-70b-instruct-fp8-fast");
```

### 2. State Management (wrangler.jsonc)
Durable Objects with SQLite for persistent chat history:
```jsonc
"durable_objects": {
  "bindings": [{
    "name": "Chat",
    "class_name": "Chat"
  }]
}
```

### 3. Chat Interface (src/app.tsx)
React-based UI with real-time streaming and tool confirmations

## Technical Highlights

- **Zero-cost AI inference** using Cloudflare Workers AI free tier
- **Global edge deployment** for low-latency responses
- **Persistent state** with Durable Objects SQLite storage
- **Real-time streaming** for smooth user experience
- **Tool integration** with human-in-the-loop confirmations

## Development

Run tests:
```bash
npm test
```

Type checking:
```bash
npm run types
```

Format code:
```bash
npm run format
```

## License

MIT

## Resources

- [Cloudflare Workers AI Documentation](https://developers.cloudflare.com/workers-ai/)
- [Cloudflare Agents Documentation](https://developers.cloudflare.com/agents/)
- [Durable Objects Documentation](https://developers.cloudflare.com/durable-objects/)
