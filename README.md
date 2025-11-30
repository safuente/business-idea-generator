# 💡 IdeaGen Pro - AI Business Idea Generator

> Generate innovative business ideas powered by GPT-5 Nano AI

[![Live Demo](https://img.shields.io/badge/demo-live-brightgreen)](https://saas-2con16zya-safuentes-projects.vercel.app)
[![Next.js](https://img.shields.io/badge/Next.js-15-black)](https://nextjs.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.115-009688)](https://fastapi.tiangolo.com/)
[![Clerk](https://img.shields.io/badge/Clerk-Auth%20%26%20Billing-6C47FF)](https://clerk.com/)

## 🚀 Demo

**Live App:** [https://saas-2con16zya-safuentes-projects.vercel.app](https://saas-2con16zya-safuentes-projects.vercel.app)

## 📖 About

IdeaGen Pro is a SaaS application that leverages GPT-5 Nano to generate unique, actionable business ideas for the AI agent economy. Built with Next.js and FastAPI, it features secure authentication, subscription management via Clerk Billing, and real-time streaming AI responses.

## ✨ Features

- 🤖 **AI-Powered Generation** - Uses GPT-5 Nano for creative, relevant business ideas
- ⚡ **Real-time Streaming** - Ideas streamed via Server-Sent Events (SSE)
- 🔐 **Secure Authentication** - Sign-up/sign-in powered by Clerk
- 💳 **Subscription Management** - Premium tier with Clerk Billing
- 🎨 **Modern UI** - Responsive design with dark mode support
- 📱 **Mobile Ready** - Works seamlessly on all devices

## 🛠️ Tech Stack

| Layer | Technology |
|-------|------------|
| **Frontend** | Next.js 15, TypeScript, Tailwind CSS |
| **Backend** | FastAPI (Python), Vercel Serverless Functions |
| **AI Model** | OpenAI GPT-5 Nano |
| **Auth & Billing** | Clerk |
| **Deployment** | Vercel |

## 🏗️ Architecture

```
┌─────────────────┐         ┌─────────────────┐         ┌─────────────────┐
│                 │   JWT   │                 │         │                 │
│   Next.js       │────────▶│   FastAPI       │────────▶│   GPT-5 Nano    │
│   Frontend      │         │   /api          │         │   (OpenAI)      │
│                 │◀────────│                 │◀────────│                 │
└─────────────────┘   SSE   └─────────────────┘         └─────────────────┘
        │
        │ Auth & Billing
        ▼
┌─────────────────┐
│     Clerk       │
│  (JWT + JWKS)   │
└─────────────────┘
```

## 📁 Project Structure

```
saas/
├── api/
│   └── index.py           # FastAPI backend (serverless function)
├── pages/
│   ├── _app.tsx           # Clerk provider setup
│   ├── _document.tsx      # HTML document structure
│   ├── index.tsx          # Landing page
│   └── product.tsx        # Idea generator (subscription protected)
├── public/
├── styles/
│   └── globals.css        # Global styles + Tailwind
├── package.json
└── requirements.txt
```

## 🚀 Getting Started

### Prerequisites

- Node.js 18+
- Python 3.11+
- [Clerk account](https://clerk.com)
- [OpenAI API key](https://platform.openai.com)

### Installation

```bash
# Clone the repository
git clone https://github.com/safuentes/saas.git
cd saas

# Install frontend dependencies
npm install

# Install backend dependencies
pip install -r requirements.txt
```

### Environment Variables

Create a `.env.local` file in the root directory:

```env
# Clerk Authentication
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=pk_test_xxxxx
CLERK_SECRET_KEY=sk_test_xxxxx
CLERK_JWKS_URL=https://your-app.clerk.accounts.dev/.well-known/jwks.json

# OpenAI
OPENAI_API_KEY=sk-xxxxx
```

### Run Locally

```bash
# Development server (frontend + API)
npm run dev
```

Visit [http://localhost:3000](http://localhost:3000)

## 🔐 Authentication Flow

```
1. User visits landing page (/)
2. Signs up/in via Clerk modal
3. Navigates to /product
4. Clerk checks subscription status:
   ├─ No subscription → Shows PricingTable
   └─ Has subscription → Shows IdeaGenerator
5. JWT sent to /api for authenticated requests
```

## 💳 Subscription Tiers

| Feature | Free | Premium ($10/mo) |
|---------|:----:|:----------------:|
| View landing page | ✅ | ✅ |
| AI idea generation | ❌ | ✅ Unlimited |
| Streaming responses | ❌ | ✅ |
| Priority support | ❌ | ✅ |

## 🔧 API Reference

### `GET /api`

Generates a business idea using GPT-5 Nano.

**Authentication:** Required (Bearer JWT)

**Headers:**
```
Authorization: Bearer <clerk_jwt>
```

**Response:** `text/event-stream`

Server-Sent Events stream with Markdown-formatted business idea.

**Example:**
```javascript
const jwt = await getToken();
await fetchEventSource('/api', {
    headers: { Authorization: `Bearer ${jwt}` },
    onmessage(ev) {
        console.log(ev.data);
    }
});
```

## 🚢 Deployment

### Vercel (Recommended)

```bash
# Install Vercel CLI
npm i -g vercel

# Deploy
vercel --prod
```

Configure environment variables in Vercel Dashboard:
- `NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY`
- `CLERK_SECRET_KEY`
- `CLERK_JWKS_URL`
- `OPENAI_API_KEY`

## 🔧 Clerk Setup

1. Create app at [dashboard.clerk.com](https://dashboard.clerk.com)
2. Enable Billing: **Configure → Subscription Plans → Enable Billing**
3. Create plan with key: `premium_subscription`
4. Copy keys to environment variables

## 🐛 Troubleshooting

| Issue | Solution |
|-------|----------|
| PricingTable not rendering | Enable Billing in Clerk Dashboard |
| "Plan not found" error | Verify plan key is exactly `premium_subscription` |
| Auth errors | Check CLERK_JWKS_URL matches your Clerk app |
| SSE not streaming | Ensure JWT is valid and passed in Authorization header |

## 🤝 Contributing

1. Fork the repository
2. Create feature branch (`git checkout -b feature/amazing`)
3. Commit changes (`git commit -m 'Add amazing feature'`)
4. Push to branch (`git push origin feature/amazing`)
5. Open a Pull Request

## 📄 License

MIT License - see [LICENSE](LICENSE) for details.

## 👤 Author

**Santiago Fuente** - [@safuente](https://github.com/safuente)

---

<p align="center">
  Built with ❤️ using Next.js, FastAPI & GPT-5 Nano
</p>