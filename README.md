# Supabase Keep Alive

A lightweight Python serverless project to keep your Supabase database alive.  
It periodically sends a small query to prevent the database from going idle.  
This project is optimized for deployment on Vercel and is intended to be triggered by an external cron service.

## Features

- 🛠 Configurable target table via environment variables
- 🚀 Fully serverless, ideal for Vercel hosting
- 📦 Simple environment setup
- 🆓 Open-source, non-commercial use only
- Vercel Cron

## Project Structure

```
supabase-keepalive/
├── api/
│   └── keepalive.py
├── .env.example
├── requirements.txt
├── vercel.json
└── LICENSE
```

## Getting Started

### 1. Set Up Environment Variables

Create a `.env` file based on the provided `.env.example`:

```env
SUPABASE_CONFIG='[
  {
    "name": "Supabase1",
    "supabase_url": "https://your-project.supabase.co",
    "supabase_key": "your-api-key",
    "table_name": "your_table"
  },
  {
    "name": "Supabase2",
    "supabase_url": "https://another-project.supabase.co",
    "supabase_key": "another-api-key",
    "table_name": "another_table"
  }
]'
```

**Important:**  
Never commit your real `.env` file.  
On Vercel, configure these environment variables in **Project Settings > Environment Variables**.

---

### 2. Deploy to Vercel

- Push the project to a GitHub repository.
- Import the repository into [Vercel](https://vercel.com/).
- Set up environment variables on the Vercel dashboard.
- Deploy your project.

---

### 3. Use Vercel Cron Job
- Edit  `vercel.json` file

---

### 4. Set Up External Cron Job(Optional)

Use any external cron service (such as EasyCron, UptimeRobot, GitHub Actions)  
to periodically trigger your endpoint once per day:

```
GET https://your-vercel-project.vercel.app/api/keepalive
```

---

## API Endpoint

**GET `/api/keepalive`**
**GET `/api/keepalive/all`**
**GET `/api/keepalive/index`** (default index 0)
**GET `/api/keepalive/index/1`** (index 1)
**GET `/api/keepalive/name/Supabase1`** (name Supabase1)

### Response

- Success:  
  ```json
  { "status": "success", "message": "ok" }
  ```
- Failure:  
  ```json
  { "status": "error", "message": "failure" }
  ```

---

## License

This project is licensed under the **MIT** license.

---

## Notes

- This project uses [Supabase Python Client](https://github.com/supabase-community/supabase-py) and [FastAPI](https://fastapi.tiangolo.com/).
- Keep the queried table lightweight to ensure minimal resource usage.
- Supabase databases usually remain active, but periodic pings add an extra layer of stability for serverless applications.