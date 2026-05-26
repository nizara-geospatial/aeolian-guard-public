# AEOLIAN-GUARD™ Core Engine
### by Nizara Geospatial — *Earth Intelligence, Automated.*

> **🔒 PRIVATE REPOSITORY** — Proprietary System  
> © 2026 Nizara Geospatial · Muhammad Nizam Abdurrachman  
> 📧 nizara.geospatial@gmail.com · 🔗 github.com/nizara-geospatial  
> 💼 linkedin.com/company/nizara-geospatial

---

## Repository Structure

```
aeolian-guard-core/
├── engine.py              ← Main pipeline (Phase 1 + Phase 2)
├── db_manager.py          ← PostgreSQL + PostGIS integration
├── locations_config.py    ← Multi-location configuration
├── schema.sql             ← Database schema (run once)
├── requirements.txt       ← Python dependencies
├── .gitignore             ← Exclude secrets & outputs
├── README.md              ← This file
└── .github/
    └── workflows/
        └── main.yml       ← GitHub Actions automation
```

---

## Required GitHub Secrets

**Settings → Secrets and variables → Actions → New repository secret**

| Secret | Description | Required |
|--------|-------------|----------|
| `GCP_SERVICE_ACCOUNT_KEY` | Google Cloud JSON key | ✅ Yes |
| `TELEGRAM_TOKEN` | Bot token from @BotFather | ✅ Yes |
| `TELEGRAM_ID` | Telegram chat ID | ✅ Yes |
| `DB_HOST` | PostgreSQL host (e.g. Supabase) | ⚠️ Optional |
| `DB_PORT` | PostgreSQL port (default: 5432) | ⚠️ Optional |
| `DB_NAME` | Database name: `nizara_geo` | ⚠️ Optional |
| `DB_USER` | Database user | ⚠️ Optional |
| `DB_PASSWORD` | Database password | ⚠️ Optional |
| `EMAIL_SENDER` | nizara.geospatial@gmail.com | ⚠️ Optional |
| `EMAIL_PASSWORD` | Zoho app password | ⚠️ Optional |

---

## Database Setup (One Time)

### Option A — Supabase (Recommended, Free)
```
1. Buka supabase.com → New Project
2. Name: nizara-geo
3. Copy connection string
4. SQL Editor → paste seluruh isi schema.sql → Run
5. Settings → Database → Connection string
   → masukkan ke GitHub Secrets sebagai DB_HOST dll
```

### Option B — Local PostgreSQL
```bash
createdb nizara_geo
psql nizara_geo < schema.sql
```

---

## Add New Client Location

Edit `locations_config.py`:
```python
'new_location_key': {
    'name':        'Facility Name',
    'country':     'UAE',
    'lat':          24.00,
    'lon':          54.00,
    'buffer_km':    30,
    'client':       'CLIENT_NAME',
    'active':        True,
    'alert_email':   'client@company.com',
    'telegram_id':   None,
    'description':  'Description',
    'timezone':     'Asia/Dubai'
},
```

---

## QGIS Connection

```
Layer → Add Layer → Add PostGIS Layer → New
Host    : [DB_HOST]
Database: nizara_geo
Schema  : public

Load these views/tables:
→ hotspots_qgis    (spatial polygons, last 7 days)
→ latest_status    (current status all locations)
→ monthly_trend    (trend chart data)
→ alert_summary_30d (alert counts)
```

---

## Pipeline Schedule

| Trigger | Time | Action |
|---------|------|--------|
| Auto | Daily 03:00 UTC | Full report all active locations |
| Manual | Anytime | Actions → Run workflow |

---

## Contacts

📧 nizara.geospatial@gmail.com  
🔗 github.com/nizara-geospatial  
💼 linkedin.com/company/nizara-geospatial

---
*© 2026 Nizara Geospatial · All rights reserved.*
