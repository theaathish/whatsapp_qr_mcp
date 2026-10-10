# 🏠 Local Development Setup

## Important: Two Package Files

This project uses **two different package.json files**:

### 📦 `package.json` (Current)
- **Purpose:** Vercel deployment only
- **Contains:** Minimal dependencies (@vercel/node, typescript)
- **Do NOT use for local development**

### 📦 `package.local.json`  
- **Purpose:** Local development and actual WhatsApp functionality
- **Contains:** All dependencies (whatsapp-web.js, MCP SDK, queue, etc.)
- **Use this for running locally**

## 🚀 Quick Start for Local Development

### Step 1: Use the Full Dependencies

```bash
# Rename to use full dependencies
mv package.json package.vercel.json
mv package.local.json package.json
```

### Step 2: Install Dependencies

```bash
npm install
```

### Step 3: Build

```bash
npm run build
```

### Step 4: Run

```bash
npm start
```

### Step 5: Configure Claude Desktop

See [CONNECT_WHATSAPP.md](CONNECT_WHATSAPP.md) for full instructions.

## 🔄 Switching Back for Vercel

If you want to push changes that Vercel will deploy:

```bash
# Restore Vercel-friendly package.json
mv package.json package.local.json
mv package.vercel.json package.json
git add package.json package.local.json
git commit -m "Update"
git push
```

## 🤔 Why Two Files?

### The Problem
- **Vercel** = Serverless, can't run WhatsApp Web (no Chrome/Puppeteer)
- **Local** = Full server, can run everything

### The Solution
- **Vercel package.json** = Minimal deps, just serves documentation
- **Local package.json** = Full deps, runs WhatsApp functionality

## 📁 What to Use When

| Task | Package File | Command |
|------|-------------|---------|
| Local development | `package.local.json` → `package.json` | `npm install && npm start` |
| Vercel deployment | `package.json` (current) | Auto-handled by Vercel |
| Update dependencies | Edit `package.local.json` | Then rename and test |

## 🆘 Troubleshooting

### "Cannot find module 'whatsapp-web.js'"

**Cause:** You're using the Vercel package.json locally

**Fix:**
```bash
mv package.json package.vercel.json
mv package.local.json package.json
npm install
```

### "Module not found" errors on Vercel

**Cause:** You accidentally pushed package.local.json as package.json

**Fix:**
```bash
git checkout package.json  # Get the Vercel version
git push
```

## 📚 More Info

- **Local Development:** Use `package.local.json`
- **Vercel Deployment:** Uses `package.json` (automatic)
- **Full Guide:** See [CONNECT_WHATSAPP.md](CONNECT_WHATSAPP.md)
- **Why This Setup:** See [WHY_VERCEL_FAILS.md](WHY_VERCEL_FAILS.md)

---

**TL;DR:** For local use, swap the package files. Current setup is for Vercel.
