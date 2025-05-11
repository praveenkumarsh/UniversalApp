# 🎨 UniversalApp UI

The frontend for the UniversalApp platform, built with **React**, **Vite**, and **Tailwind CSS**. This single-page application (SPA) interfaces with all backend microservices like authentication, chat, pastebin, file manager, URL shortener, and code compiler via the AcceptorService gateway.

---

## 📸 Screenshots

> _Add screenshots here showing the dashboard, chat interface, pastebin, URL shortener, file manager, and code compiler._

---

## 🚀 Features

- ✨ Fully responsive SPA (Single Page Application)
- 🔐 Integrated with JWT and Google OAuth
- 💬 Real-time chat (WebSocket)
- 📄 PasteBin UI with code highlighting
- 🔗 Short URL generator
- 🗂️ File upload & download interface
- 💻 Online code compiler with language switcher
- 🌙 Dark mode support

---

## 📁 Project Structure

```bash
UniversalAppUI/
├── public/                 # Static assets
├── src/
│   ├── components/         # Reusable components
│   ├── features/           # App-specific pages like Chat, PasteBin etc.
│   ├── context/            # Auth and app context providers
│   ├── routes/             # All routes via React Router
│   ├── App.tsx             # Main app container
│   └── main.tsx            # Vite entry point
├── .env                    # API endpoint configs
├── package.json            # NPM dependencies and scripts
└── tailwind.config.js      # TailwindCSS config
```

---

## 🧪 Local Setup

### Prerequisites

- Node.js >= 18.x
- NPM or Yarn

### Steps

```bash
git clone https://github.com/praveenkumarsh/UniversalAppUI.git
cd UniversalAppUI
npm install
npm run dev
```

Update your `.env` file with:

```env
VITE_API_BASE_URL=http://<your-acceptor-service-ip>:<port>/api
```

---

## 🧪 Testing

```bash
npm run test
```

---

## 🔐 Authentication

- **Login/Signup** handled via `AcceptorService`
- Supports **JWT** & **Google OAuth2.0**
- Auto-login from stored token

---

## 📦 Build

```bash
npm run build
```

Then serve using any static server or host on S3/Netlify/Vercel etc.

---

## 🧩 Related Services

- [AcceptorService README](../AcceptorService/README.md)
- [ChatApp README](../ChatApp/README.md)
- [PasteBin README](../PasteBin/README.md)
- [ShortURL README](../ShortURL/README.md)
- [FileManager README](../FileManager/README.md)
- [CodeCompiler README](../CodeCompiler/README.md)

---

## 📜 License

Licensed under the [MIT License](../LICENSE).