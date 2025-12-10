# 🛡️ DRP Scanner Pro v6

A powerful Google Groups leak detection tool for Digital Risk Protection (DRP) analysis. Built for security researchers and SOCRadar integration.

![Version](https://img.shields.io/badge/version-6.0-coral)
![License](https://img.shields.io/badge/license-MIT-blue)

## ✨ Features

### 🔍 Dual Search Modes
- **🔵 Google Groups Direct** - Search directly in groups.google.com
- **🔴 Google Dorks** - Use `site:groups.google.com` syntax for broader results
- **🟣 Both** - Generate links for both methods simultaneously

### 📊 Asset Categories
- Company Names
- Brand Keywords
- VIP Accounts (Email addresses)
- Domains (Auto-extracted from emails)

### 🔐 Optional Sensitive Keyword Combinations
Toggle on/off sensitive keyword searches with selectable keywords:
- `password`, `credential`, `login`, `internal`, `vpn`
- `token`, `api_key`, `secret`, `confidential`, `private`
- `admin`, `ssh`

### 🚀 Scanner Controls
- **Next** - Open links one by one
- **Slow Mode** - Auto-open with adjustable speed (0.5s - 5s)
- **Fast Mode** - Open all remaining links at once
- Keyboard shortcuts: `Space` / `Enter`

## 📁 Files

| File | Description |
|------|-------------|
| `drp_scanner_v6.html` | Main scanner (English UI, all features) |
| `drp_scanner_pro_v5.html` | Previous version with SOCRadar API integration |
| `*_dorks.txt` | Pre-generated dork lists for specific companies |
| `*_scanner.html` | Company-specific standalone scanners |

## 🚀 Quick Start

1. Open `drp_scanner_v6.html` in your browser
2. Enter **Company Name**
3. Paste raw data from SOCRadar (Brand Keywords, VIP Accounts, etc.)
4. Select **Search Mode** (Groups / Dorks / Both)
5. Toggle **Sensitive Keywords** if needed
6. Click **Parse & Create Scanner**
7. Start scanning!

## 📋 Data Format

Paste data in this format:
```
keyword1
Brand Keyword
ceo@company.com
VIP Account
company.com
Brand Keyword
```

## 🔧 SOCRadar API Integration (v5)

For automated asset fetching, use `drp_scanner_pro_v5.html` with:
- API Key
- Company ID
- CORS Proxy (corsproxy.io recommended)

## 📤 Export Options

- **HTML** - Standalone scanner file (works offline)
- **TXT** - Dork list for manual searches

## ⚠️ Known Issues

- **CORS**: Direct SOCRadar API calls blocked by browsers (use CORS proxy)
- **Rate Limiting**: Google may block rapid searches (use slow mode)

## 📜 License

MIT License - Use responsibly for authorized security testing only.

---

Made with ❤️ for the security community
