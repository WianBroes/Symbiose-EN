# Symbiose — Adaptive AI Interaction Framework

**Agnostic, portable, adaptive — the system lives in the files, not in the tool.**

![GitHub](https://img.shields.io/badge/status-stable-green)
![License](https://img.shields.io/badge/license-MIT-blue)

## ⬇️ [Download Symbiose](https://github.com/WianBroes/Symbiose-EN/archive/refs/heads/master.zip)

---

## What is it?

An **adaptive framework** that **learns from you** across sessions.
Drop it in a folder, launch your AI tool inside, and the system:

- 🔄 **Remembers** context between sessions
- 🧠 **Adapts** progressively to your way of working
- 🔌 **Works with** PI, Claude Code, Codex CLI, Cursor, Continue.dev…
- 📦 **Is shareable** — reset-ready for another user

> **Core idea:** the system lives in `.md` files, not in the tool.
> Switch AI tools mid-course without losing anything.

---

## 🚀 Quick start

**1. Get the files**
Click **Download ZIP** at the top of this page and unzip the folder.
*(or `git clone` if you know what that is)*

**2. Open it with your AI tool**
Launch your AI tool (Claude Code, PI, Cursor, Codex CLI…) inside the Symbiose folder.

**3. Say "yo"**
The system takes over — it sets itself up, asks your name, and you're ready to go.

**No config, no dependencies, no installation.**

---

## 📖 How it works

| Step | What happens |
|------|-------------|
| **1. You arrive** | Say "yo" — system starts automatically |
| **2. First time** | It scans your setup, asks your name, creates your profile |
| **3. You work** | Give instructions in plain language. The AI announces each action. |
| **4. You close** | Say "close" or "we're done" → everything saved for next session |

---

## 🧠 Why use it?

**Without Symbiose:** Every new session is a blank slate. The AI knows nothing about you, your projects, your preferences. You repeat the same things endlessly.

**With Symbiose:**
- Memory persists → AI is **more relevant every session**
- Profile sharpens → AI **adapts to your rhythm and style**
- Context transfers → **no loss between sessions**
- The more you use it, **the better it gets**

---

## 📂 What's in the folder

```
Symbiose/
├── AGENTS.md          ← AI instructions (entry point)
├── _SYSTEM/           ← system files (readable and editable)
│   ├── memory/        ← AI memory about you
│   └── profile/       ← your profile
└── 00_📥 Inbox/       ← notes passed from one session to the next
```

Everything is `.md` — you can open, read, and edit any file.

---

## 🔧 Customization

The system is designed to be modified:

1. **Your profile** → edit `_SYSTEM/profile/README.md`
2. **The rules** → edit `_SYSTEM/CORE.md`
3. **Start fresh** → delete `_SYSTEM/.init_done`

---

## 🤝 Contributing

Have an idea or a fix? Open an **Issue** on GitHub to discuss it.
If you know git: fork → edit → Pull Request.

---

## 📜 License

MIT — Free to use, modify, and share.

---

**Built to last. Designed to evolve. Ready to share.**

---
*by [Wian Broes](https://github.com/WianBroes)*
