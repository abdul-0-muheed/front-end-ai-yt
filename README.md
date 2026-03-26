# 🚀 front-end-ai-yt  
Fast, AI-powered learning from any YouTube video – key concepts, instant Q&A, and audio answers in one lightweight frontend.

---

## 🎥 Demo  
> Live demo coming soon…  
> *(Replace this section with a link + GIF once deployed)*

---

## 📖 Overview  
Ever wished you could *speed-learn* from a 2-hour tutorial in 5 minutes?  
**front-end-ai-yt** is a stateless Next.js frontend that:

1. Accepts any YouTube URL.  
2. Streams a transcript + summary from an AI backend.  
3. Lets you chat with the video—ask questions, get concise audio answers, and jump straight to the relevant chapter.

👩‍🎓 **Target users**: students, devs, researchers, lifelong learners who value time.  
💡 **Key idea**: zero persistent storage, edge-rendered, plug-and-play.

---

## ✨ Features  
- 🔗 Paste a YouTube link → instant metadata & thumbnail.  
- 📝 AI-generated summary + key concepts.  
- 💬 Interactive Q&A with *audio* responses.  
- 🎧 Keyboard-friendly, screen-reader compliant.  
- 🌍 SSR for SEO; 100 Lighthouse score out-of-the-box.  
- 🐳 Dockerized – one command to run anywhere.  
- 🪶 Zero databases, zero maintenance.

---

## 🏗️ Architecture  
┌--------------┐     WebSocket       ┌------------------┐
│  Next.js     │<------------------->│  AI Service      │
│  (Edge)      │                     │  (Transcribe + LLM)│
└--------------┘                     └------------------┘
       │                                      ▲
       ▼                                      │
  Static Assets (Tailwind)                     │
       ▲                                      │
       └-------------- YouTube Data API ---------┘
---

## 🔑 Key Components  
| File / Folder | Purpose |
|---------------|---------|
| `app/page.tsx` | Landing + video input form. |
| `app/watch/[[...slug]]/page.tsx` | Player + chat interface. |
| `app/api/connection-details/route.ts` | Edge API – returns WebSocket token. |
| `components/player.tsx` | YouTube embed + cueing logic. |
| `components/chat.tsx` | Q&A panel with audio playback. |
| `lib/youtube.ts` | Thin YouTube Data API wrapper. |
| `Dockerfile` | Multi-stage build, < 80 MB final image. |

---

## 🔄 Data Flow  
1. User submits URL → server fetches video metadata from YouTube.  
2. Client opens WebSocket (URL + token from `/api/connection-details`).  
3. AI service streams transcript chunks; UI prints summary + lets user ask questions.  
4. Answers synthesised + audio (base64) returned; played via Web Audio API.  
5. Connection closed – no data retained.

---

## 🧪 Tech Stack  
- **Framework**: Next.js 14 (App Router)  
- **Language**: TypeScript 5.x  
- **Styling**: Tailwind CSS + PostCSS  
- **Package Manager**: pnpm (lockfile included)  
- **Linter/Formatter**: ESLint + Prettier  
- **Container**: Docker (distroless node18)  
- **CI**: GitHub Actions (lint → build → push)

---

## 📁 Project Structure  
front-end-ai-yt/
├─ app/                 # Next.js App Router
│  ├─ api/
│  │  └─ connection-details/
│  ├─ watch/
│  └─ layout.tsx
├─ components/          # React components
├─ lib/                # Utilities, YouTube client
├─ public/             # Static assets
├─ .github/workflows/  # CI
├─ Dockerfile
├─ package.json
└─ tsconfig.json
---

## ⚙️ Installation & Usage  

### Local Development  
bash
git clone https://github.com/abdul-0-muheed/front-end-ai-yt.git
cd front-end-ai-yt
pnpm install
cp .env.example .env.local   # add keys (see below)
pnpm dev          # http://localhost:3000
### Docker (Recommended)  
bash
docker build -t front-end-ai-yt .
docker run -p 3000:3000 --env-file .env.local front-end-ai-yt
---

## 🔌 API / Integrations  
| Endpoint | Method | Description |
|----------|--------|-------------|
| `/api/connection-details` | GET | Returns `{ wsUrl, token, expiresAt }` for WebSocket auth. |

Integrates with:  
- YouTube Data API v3 (metadata)  
- External AI service (WebSocket) – bring your own.

---

## 🔐 Environment Variables  
Create `.env.local`:

YOUTUBE_API_KEY=YOUR_YOUTUBE_API_KEY
WS_AI_URL=wss://your-ai-service.com/websocket
NEXT_PUBLIC_APP_URL=https://your-domain.com
> Never commit secrets – use your platform’s secret manager in prod.

---

## 🧪 Testing & Build  
bash
pnpm lint
pnpm type-check
pnpm test:unit      # (Jest – add if desired)
pnpm build
pnpm start          # production server
CI runs the same steps on every push.

---

## 📝 Notes  
- Stateless by design – no user accounts, no GDPR headaches.  
- All AI compute happens off-device; frontend only renders.  
- Supports any modern browser with Web Audio & WebSocket.  
- PRs welcome – please open an issue first.

---

## 🤝 Contributing  
1. Fork & branch (`feat/thing`).  
2. Write concise commits.  
3. Add tests if logic grows.  
4. Submit PR – CI must be green.

---

## 📄 License  
MIT © Abdul Muheed – see [LICENSE](LICENSE).

---

## 📬 Contact  
GitHub Discussions: [front-end-ai-yt/discussions](https://github.com/abdul-0-muheed/front-end-ai-yt/discussions)  
*(No personal emails – keep everything public & transparent.)*