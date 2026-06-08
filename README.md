# Symbiose — Adaptive AI interaction framework

**Agnostic, portable, adaptive — the system lives in files, not in the tool.**

![GitHub](https://img.shields.io/badge/status-stable-green)
![License](https://img.shields.io/badge/license-MIT-blue)

## ⬇️ [Download Symbiose](https://github.com/WianBroes/Symbiose-EN/archive/refs/heads/master.zip)

---

## What is it?

An **adaptive framework** that **learns from you** across sessions.
Drop it in a folder, launch your AI tool inside it, and the system:

- 🔄 **Remembers** context between sessions
- 🧠 **Adapts** progressively to your way of working
- 🔌 **Works with** PI, Claude Code, Codex CLI, Cursor, Continue.dev…
- 📦 **Is resettable** — ready to hand off to another user

> **Core idea:** the system lives in `.md` files, not in the tool.
> Switch tools mid-way without losing anything.

---

## 🚀 Quick start

**1. Get the files**
Click **Download ZIP** at the top of this page and unzip the folder.
*(or `git clone` if you know what that means)*

**2. Open it with your AI tool**
Launch your AI tool (Claude Code, PI, Cursor, Codex CLI…) in the Symbiose folder.

**3. Say "yo"**
The system takes over — it configures itself, asks your name, and you're off.

**No config, no dependencies, no installation.**

---

## 📖 How it works

| Step | What happens |
|------|-------------|
| **1. You arrive** | You say "yo" — the system starts automatically |
| **2. First time** | It scans your setup, asks your name, creates your profile |
| **3. You work** | Give instructions in natural language. The AI announces each action. |
| **4. You close** | You say "close" or "we're done" → everything is saved for next session |

---

## 🧠 Why use it?

**Without Symbiose:** Every new session starts from scratch. The AI knows nothing about you, your projects, your preferences. You repeat yourself constantly.

**With Symbiose:**
- Memory persists → the AI is **more relevant every session**
- Profile refines → the AI **adapts to your pace and style**
- Context transfers → **no loss between sessions**
- The more you use it, **the better it works**

---

## 📂 What's in the folder

```
Symbiose/
├── AGENTS.md          ← AI instructions (entry point)
├── _SYSTEM/           ← system files (readable and editable)
│   ├── memory/        ← AI memory about you
│   └── profile/       ← your profile
├── pi-extensions/     ← optional extensions for PI
└── 00_📥Inbox/        ← notes passed between sessions
```

Everything is `.md` — you can open, read and modify any file.

---

## 🔌 Extensions

Some AI tools don't have all capabilities natively. Extensions are available in `pi-extensions/`:

| Extension | For who | What it adds |
|-----------|---------|--------------|
| **web-search** | PI | DuckDuckGo search + web page reading |

See `pi-extensions/web-search/README.md` for installation.

---

## 🔧 Customization

The system is built to be modified:

1. **Your profile** → edit `_SYSTEM/profile/README.md`
2. **The rules** → edit `_SYSTEM/CORE.md`
3. **Start over** → delete `_SYSTEM/.init_done`

---

## 🤝 Contribute

An idea or a fix? Open an **Issue** on GitHub to discuss it.
If you know git: fork → modify → Pull Request.

📋 [CHANGELOG](CHANGELOG.md) — history of fixes and additions.

---

## 📜 License

MIT — Free to use, modify and share.

---

**Built to last. Designed to evolve. Ready to share.**

---
*by [Wian Broes](https://github.com/WianBroes)*
