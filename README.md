# Welcome to React Router!

A modern, production-ready template for building full-stack React applications using React Router.

[![Open in StackBlitz](https://developer.stackblitz.com/img/open_in_stackblitz.svg)](https://stackblitz.com/github/remix-run/react-router-templates/tree/main/default)

## Features# 🏠 Roomify

> AI-powered 2D floor plan to photorealistic 3D render — instantly.

Roomify lets you upload any 2D architectural floor plan and transforms it into a **photorealistic, top-down 3D visualization** using Google Gemini's image generation model — all within a clean, modern web UI. Projects are saved per-user via Puter's cloud infrastructure, so your work is always there when you come back.

---

## ✨ Features

| Feature | Description |
|---|---|
| 🖼️ Floor Plan Upload | Drag-and-drop or click to upload JPG/PNG floor plans |
| 🤖 AI 3D Rendering | Converts 2D plans to photorealistic top-down renders via Gemini 2.5 Flash |
| 🔄 Before / After Slider | Side-by-side comparison of original and rendered output |
| 💾 Project Storage | Per-user project history saved to Puter KV + hosted image storage |
| 🔐 Auth | Sign in / sign out via Puter OAuth |
| 📥 Export | Download your rendered image with one click |
| 🐳 Docker Ready | Multi-stage Dockerfile for production deployments |

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Framework | React 19 + React Router v7 (SSR) |
| Language | TypeScript |
| Styling | TailwindCSS v4 |
| Build Tool | Vite |
| AI | Puter.js → Gemini 2.5 Flash (`txt2img`) |
| Auth & Storage | [Puter.js](https://puter.com) (KV store + hosting) |
| Backend Worker | Puter Worker (serverless routing) |
| Icons | Lucide React |
| Compare UI | react-compare-slider |

---

## 📂 Project Structure

```
roomify/
├── app/
│   ├── app.css                 # Global styles & Tailwind theme
│   ├── root.tsx                # App shell, auth state, outlet context
│   ├── routes.ts               # Route definitions
│   └── routes/
│       ├── home.tsx            # Landing page + upload + project grid
│       └── visualizer.$id.tsx  # Render view + before/after compare
├── components/
│   ├── Navbar.tsx              # Top navigation with auth controls
│   ├── Upload.tsx              # Drag-and-drop file uploader
│   └── ui/
│       └── Button.tsx          # Reusable button component
├── lib/
│   ├── ai.action.ts            # Gemini image generation logic
│   ├── constants.ts            # App-wide constants & render prompt
│   ├── puter.action.ts         # Puter auth, project CRUD
│   ├── puter.hosting.ts        # Image upload to Puter static hosting
│   ├── puter.worker.ts         # Serverless worker route handlers
│   └── utils.ts                # Image conversion, URL helpers
├── type.d.ts                   # Global TypeScript interfaces
├── Dockerfile                  # Multi-stage production Docker build
├── vite.config.ts
└── react-router.config.ts
```

---

## ⚙️ Getting Started

### Prerequisites

- Node.js `>= 20`
- A [Puter](https://puter.com) account (free) for auth and storage
- A deployed Puter Worker (set its URL in `.env.local`)

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/roomify.git
cd roomify
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Configure Environment

Create a `.env.local` file in the root:

```env
VITE_PUTER_WORKER_URL=https://your-worker-url.puter.work/
```

> 👉 Deploy `lib/puter.worker.ts` as a Puter Worker to get this URL.  
> The worker handles project save/list/get via Puter KV.

### 4. Start Development Server

```bash
npm run dev
```

App will be available at `http://localhost:5173`.

---

## 🏗️ Building for Production

```bash
npm run build
npm run start
```

Or with Docker:

```bash
docker build -t roomify .
docker run -p 3000:3000 roomify
```

The multi-stage Dockerfile separates dev dependencies, production dependencies, and the final runtime image for a lean container.

---

## 🔄 How It Works

```
User uploads floor plan (JPG/PNG)
        ↓
Image converted to base64
        ↓
Saved to Puter KV + hosted on Puter static hosting
        ↓
puter.ai.txt2img() called with Gemini 2.5 Flash
        ↓
AI prompt: "Convert 2D floor plan → photorealistic top-down 3D render"
        ↓
Rendered image saved back to Puter storage
        ↓
Visualizer displays result + before/after slider
```

---

## 🌐 Deployment

Roomify is a standard Node.js SSR app and can be deployed anywhere that supports Docker or Node:

- **Docker** — `docker build` + `docker run` (see above)
- **Fly.io** — `fly launch`
- **Railway** — connect repo and deploy
- **Google Cloud Run** — push image to GCR and deploy
- **AWS ECS / Azure Container Apps** — standard container deployment

---

## 📸 Screenshots

> _Add your app screenshots here_

---

## 🚀 Planned Improvements

- [ ] 🪑 Furniture style selector (modern, minimalist, industrial)
- [ ] 🎨 Room-by-room material customization
- [ ] 🌐 Public project gallery / community feed
- [ ] 📤 Share rendered project via link
- [ ] 📱 Improved mobile layout

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).

---

## 👨‍💻 Author

**Aarav Kumar**  
🔗 GitHub: [@aarav12e](https://github.com/aarav12e)

---

> ⭐ If you found this useful, please **star the repo** and share it!

- 🚀 Server-side rendering
- ⚡️ Hot Module Replacement (HMR)
- 📦 Asset bundling and optimization
- 🔄 Data loading and mutations
- 🔒 TypeScript by default
- 🎉 TailwindCSS for styling
- 📖 [React Router docs](https://reactrouter.com/)

## Getting Started

### Installation

Install the dependencies:

```bash
npm install
```

### Development

Start the development server with HMR:

```bash
npm run dev
```

Your application will be available at `http://localhost:5173`.

## Building for Production

Create a production build:

```bash
npm run build
```

## Deployment

### Docker Deployment

To build and run using Docker:

```bash
docker build -t my-app .

# Run the container
docker run -p 3000:3000 my-app
```

The containerized application can be deployed to any platform that supports Docker, including:

- AWS ECS
- Google Cloud Run
- Azure Container Apps
- Digital Ocean App Platform
- Fly.io
- Railway

### DIY Deployment

If you're familiar with deploying Node applications, the built-in app server is production-ready.

Make sure to deploy the output of `npm run build`

```
├── package.json
├── package-lock.json (or pnpm-lock.yaml, or bun.lockb)
├── build/
│   ├── client/    # Static assets
│   └── server/    # Server-side code
```

## Styling

This template comes with [Tailwind CSS](https://tailwindcss.com/) already configured for a simple default starting experience. You can use whatever CSS framework you prefer.

---

Built with ❤️ using React Router.
