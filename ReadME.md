# Contec — Roku Data Dashboard

A Streamlit-based internal analytics dashboard for tracking, visualizing, and managing Roku service data. Built with SQLite for local data storage and bcrypt-secured user authentication.

---

## Features

- **Secure Login** — bcrypt-hashed password authentication with role-based access (User / Admin / Super Admin)
- **User Management** — Admins can create, delete, and update user accounts
- **Monthly Revenue Graph** — Histogram of monthly revenue broken down by week
- **Weekly Revenue Data** — Week-over-week quantity and amount comparisons
- **Weekly Services Data** — Service-code-level breakdown for any date range
- **Statistical Data** — Aggregated stats with Pie, Line, Bar, and Scatter chart options across weekly / monthly / quarterly / half-yearly periods
- **Analysis Data** — Deep-dive summaries including top/least models by quantity and revenue, service-code insights, and revenue share charts

---
<img width="1921" height="1005" alt="image" src="https://github.com/user-attachments/assets/a022a930-83df-4a56-98e8-b432910bf45a" />

<img width="1916" height="1011" alt="image" src="https://github.com/user-attachments/assets/9b334ded-5d93-4d5d-aece-18f3f3892255" />

<img width="1921" height="1011" alt="image" src="https://github.com/user-attachments/assets/7ec20e32-cd3f-4002-b7e6-ddd82ee7ed43" />

<img width="1921" height="974" alt="image" src="https://github.com/user-attachments/assets/9ba5b261-5e92-4d90-8c24-931b080f7937" />

<img width="1919" height="994" alt="image" src="https://github.com/user-attachments/assets/1c44a3b3-c18c-4d43-8db8-f4d178023cb2" />


## Tech Stack

| Library | Purpose |
|---|---|
| `streamlit` | Web UI framework |
| `pandas` / `numpy` | Data processing |
| `plotly` / `matplotlib` | Charts and visualizations |
| `streamlit-aggrid` | Interactive data grids |
| `sqlite3` | Local database |
| `bcrypt` | Password hashing |
| `cachetools` | TTL-based query caching (30 min) |
| `python-dotenv` | Environment variable management |

---

## Project Structure

```
roku_data-main/
├── roku.py            # Main application (all pages, DB, auth logic)
├── mycontec.db        # SQLite database
├── mycontec           # Binary — compiled app artifact
├── contec.png         # Sidebar logo
├── requirements.txt   # Python dependencies
├── config.toml        # Streamlit configuration
├── secrets.toml       # Streamlit secrets (keep private)
├── .env               # User credentials (keep private)
└── .gitignore
```

---

## Getting Started

### 1. Install dependencies

```bash
pip install -r requirements.txt
```

### 2. Run the app

```bash
streamlit run roku.py
```

### 3. Log in

Default admin credentials:

| Field | Value |
|---|---|
| Username | `lakshmanan` |
| Password | `clak$123` |

> **Change the default admin password immediately after first login.**

---

## Database Schema

### `roku_data` table

Stores all service/invoice records.

| Column | Type | Description |
|---|---|---|
| `contec_id` | INTEGER PK | Auto-increment ID |
| `reportdate` | DATE | Report date |
| `designator` | VARCHAR | Designator code |
| `TrackingID` | VARCHAR | Tracking identifier |
| `invoice_code` | VARCHAR | Invoice code |
| `qty` | INTEGER | Quantity |
| `rate` | FLOAT | Unit rate |
| `amount` | FLOAT | Total amount |
| `invoice_number` | VARCHAR | Invoice number |
| `servicecode` | VARCHAR | Service code |
| `Palletsize` | INTEGER | Pallet size |
| `PalletCount` | INTEGER | Pallet count |
| `Model` | VARCHAR | Device model |
| `TestDate` | DATE | Test date |
| `FailureDescription` | VARCHAR | Failure details |
| `failurecode` | VARCHAR | Failure code |
| `PartDescription` | VARCHAR | Part description |
| `invoicetype` | VARCHAR | Invoice type |
| `Invoice_Reference` | VARCHAR | Reference number |

### `users` table

Stores user accounts and roles.

| Column | Type | Description |
|---|---|---|
| `username` | TEXT PK | Unique username |
| `password_hash` | TEXT | bcrypt hash |
| `is_admin` | BOOLEAN | Admin flag |
| `is_superadmin` | BOOLEAN | Super admin flag |
| `created_at` | TIMESTAMP | Account creation time |
| `last_login` | TIMESTAMP | Last login time |

---

## Security Notes

- Passwords are hashed with `bcrypt` and never stored in plain text.
- `.env` and `secrets.toml` contain sensitive credentials — **do not commit these to version control**.
- Both files are listed in `.gitignore`.

---

## License

See [LICENSE](LICENSE) for details.
