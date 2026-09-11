# Service 1 Setup Guide: LinkedIn AI Content Engine & Auto-Scheduler

Is guide me setup step-by-step bataya gaya hai ki client ke liye **LinkedIn Content & AI Image Automation** kaise deploy karein using this codebase.

---

## 🏗️ Architecture Overview

```
[ Scheduled Post Data / Prompt ]
               │
               ▼
[ Google Gemini Imagen 4 ] ──► (Generates post banner image)
               │
               ▼
[ LinkedIn MCP Server ] ──► (Schedules or directly publishes post)
               │
               ▼
[ LinkedIn API ] ──► Live on Client's Profile!
```

---

## 🚀 Setup Steps for Client

### Step 1: Client LinkedIn Developer App Setup
1. Client se unke LinkedIn Developer account me App create karwaye (ya screen share par karein).
2. Enable Products:
   - **Share on LinkedIn**
   - **Sign In with LinkedIn using OpenID Connect**
3. Auth settings me redirect URL set karein: `http://localhost:8585/callback`
4. Client's **Client ID** & **Client Secret** copy karein.

### Step 2: Get Gemini Free API Key
1. Go to [Google AI Studio](https://aistudio.google.com).
2. Click **Create API Key** (100% Free).

### Step 3: Deployment (Free Hosting via Render or Local Daemon)

Create a `.env` file on the deployed instance:
```env
LINKEDIN_CLIENT_ID=your_client_id
LINKEDIN_CLIENT_SECRET=your_client_secret
GEMINI_API_KEY=your_gemini_key
```

Run scheduler daemon:
```bash
npx linkedin-mcp-server --scheduler
```

### Step 4: Ready-made Post Creation Script

Client ko simple prompt / template dein, ya AI se post content generate karke schedule payload send karein:

```json
{
  "text": "Excited to share how micro-automations are changing the game for tech founders! #AI #Automation #Efficiency",
  "scheduled_at": "2026-03-05T08:00:00Z",
  "gemini_prompt": "Clean modern tech workspace with futuristic holographic AI icons, high resolution corporate style"
}
```

---

## 💡 Value Pitch to Client:
*"We set up a dedicated LinkedIn AI Scheduler that automatically generates custom branded banners and publishes your scheduled thoughts without you lifting a finger."*
