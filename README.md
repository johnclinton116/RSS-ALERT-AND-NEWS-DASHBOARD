# JCF Alert & News Dashboard — V1

> **Builder Not Coder** — Real-time news intelligence for India, built with RSS, AI, and zero-fuss deployment.

---

## What Is It?

JCF Alert & News Dashboard is a self-hosted Flask web application that aggregates 100+ live RSS feeds from Indian news sources, runs AI-based verification on articles, plots city-level alerts on an interactive map, and gives your team a shared workspace with role-based access, internal chat, and rich export options.

It works out of the box on SQLite (no database server needed) and upgrades transparently to Microsoft SQL Server when available.

---

## Quick Start

### 1. Clone / Download

```
git clone <your-repo-url>
cd jcf-dashboard
```

### 2. Install Dependencies

```
pip install -r requirements.txt
```

> **Python 3.9 or later** is required. Python 3.10 / 3.11 recommended.

### 3. Run

```
python app_jcf_V1.py
```

Open your browser at **http://localhost:5012**

### 4. Log In

| Field    | Value       |
|----------|-------------|
| Username | `admin`     |
| Password | `admin@123` |

> Change your password immediately after first login via the 🔑 icon in the header.

---

## Database Options

### SQLite (default — zero setup)

If `pyodbc` is not installed, or if MSSQL is unreachable, the app automatically runs entirely on SQLite. All features work identically. Your data is stored in `news_fallback.db` next to the script.

```
# No configuration needed — just run the app.
python app_jcf_V1.py
```

### Microsoft SQL Server (optional upgrade)

1. Install the ODBC Driver:  
   - Windows: [Download ODBC Driver 17](https://learn.microsoft.com/en-us/sql/connect/odbc/download-odbc-driver-for-sql-server)
   - Linux: `sudo apt install unixodbc-dev && pip install pyodbc`

2. Edit `DB_CONFIG` near the top of `app_jcf_V1.py`:

```python
DB_CONFIG = {
    "server":   "YOUR_SERVER_IP",
    "database": "jcf_news",
    "username": "sa",
    "password": "YourPassword",
    "driver":   "ODBC Driver 17 for SQL Server",
    "port":     1433,
}
```

3. Set `USE_MSSQL = True` (already the default).

The app will connect to MSSQL and fall back to SQLite automatically if the server is down — no manual intervention needed.

---

## Features

| Feature | Details |
|---|---|
| 📡 RSS Feed Aggregation | 191+ India news sources, auto-fetched every 5–60 min |
| 🤖 AI Verification | Groq API — labels articles ✅ Real / ❌ Fake / ⚠️ Unverified |
| 🗺️ City Heat Map | Leaflet.js map with pins coloured by category and risk level |
| 🚨 Alerts | High / Medium / Low priority cards with urgent pulse animation |
| 📂 Categories | Traffic · Weather · Power Outage · Festivals · Crime · Health · Politics · Business |
| ⭐ Favourites | Bookmark any article or alert |
| 🔔 Notifications | Bell icon with unread badge; auto-notifies on high-priority articles |
| 🔍 Search & Filter | Keyword · city/state · event type · date range · priority · category |
| 📤 Export | CSV · PDF · Excel (multi-sheet workbook) |
| 💬 Internal Chat | Per-user private messaging with article sharing |
| 📰 Article Assignment | Admins can assign articles to team members |
| 🌐 Language Translate | Google Translate widget for any article |
| 📱 Mobile Friendly | Responsive layout; tested on iOS and Android |
| 👥 Multi-User | Up to 20 named users; roles: Admin · Editor · Viewer |
| 📊 Pivot / Analytics | Word-frequency pivot, source breakdown, sentiment trends |
| 🔗 LAN QR Access | Shows QR code for same-network phones and tablets |

---

## Folder Structure

```
jcf-dashboard/
├── app_jcf_V1.py          # Main application (single file)
├── requirements.txt       # Python dependencies
├── README.md              # This file
├── logo/                  # Drop your logo here (auto-detected)
│   └── my_logo_pic.png    # Rename to any .png or .jpg
├── news_fallback.db       # SQLite database (auto-created)
└── log/
    └── jcfalert_YYYYMMDD.log   # Daily log files (7-day retention)
```

---

## Logo Setup

Place your logo file in a subfolder called `logo/` next to the script:

```
logo/my_logo_pic.png
```

The app auto-detects any `.png` or `.jpg` in the `logo/` folder on startup. You can also upload a logo through **Settings → Logo Upload** while the app is running.

---

## Configuration Reference

All settings are near the top of `app_jcf_V1.py`:

| Variable | Default | Purpose |
|---|---|---|
| `USE_MSSQL` | `True` | Try MSSQL first; fall back to SQLite |
| `DB_CONFIG` | see file | MSSQL connection details |
| `DB_PATH` | `news_fallback.db` | SQLite file location |
| `DATA_RETENTION_DAYS` | `30` | Auto-delete articles older than N days |
| `LOG_RETENTION_DAYS` | `7` | Auto-delete log files older than N days |
| `LOG_DIR` | `Documents/JCF RSS Dashboard/Log` | Log output folder |

---

## Groq AI Verification (optional)

1. Get a free API key at [console.groq.com](https://console.groq.com)
2. In the dashboard, go to **⚙️ Settings → Groq API Key** and paste your key.
3. Click **🤖 Verify** in the header toolbar to verify unverified articles.

---

## Network Access (LAN)

The app binds to `0.0.0.0:5012` so any device on the same network can access it. Go to **Settings → Network / LAN Access** to see your LAN URL and a QR code for quick mobile access.

---

## Logs

Logs are written daily to the `log/` folder (next to the script). Files older than 7 days are deleted automatically. Format: `jcfalert_YYYYMMDD.log`.

---

## Support

📧 **johnclinton116@gmail.com**

---

## Default Login Reminder

```
URL:      http://localhost:5012
Username: admin
Password: admin@123
```
