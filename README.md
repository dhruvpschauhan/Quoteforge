QuoteForge is a web-based quotation tool built for a large sanitaryware and piping-materials supplier. It replaces the repeated manual work of preparing separate dealership quotes with one workflow: enter a client's requested products and quantities, then generate comparable quotations for multiple brands at once.


What used to take around **2 hours** can now be completed in about **10 minutes**. QuoteForge also creates downloadable files so the client can compare prices and choose the option that works best for them.


## Features


- Build a quote by searching products and entering quantities.
- Calculate prices using product MRPs, configured discounts, and GST rates.
- Compare totals across **Apollo, Supreme, Astral, and Ashirvad**, with the lowest total highlighted.
- Export a comparison workbook in **Excel (.xlsx)** format, with a comparison sheet and brand-specific detail sheets.
- Export a multi-page **PDF** with comparison and brand-specific quote details.
- Browse, search, filter, and revisit saved quote history.
- Maintain the dealer's business profile and logo for quotation documents.
- Manage dealership contacts.
- Administer product and discount data, including Excel upload and sync workflows.


## Tech stack


- **Frontend:** React, Vite, Tailwind CSS
- **Backend:** Python, FastAPI, SQLAlchemy (async)
- **Database:** SQLite by default
- **Exports:** openpyxl for Excel and WeasyPrint for PDF


## Run locally


### Requirements


- Python 3.10+
- Node.js and npm


### Windows quick start


From the repository folder, run `Setup-New-PC.bat` once to install dependencies. Then run `Start-QuoteForge.bat` to start the backend and frontend and open the app in your browser.


The app uses the Vite development server at `http://localhost:5174` and the API at `http://localhost:8000`. FastAPI's interactive API documentation is available at `http://localhost:8000/docs`.


### Manual setup


Install backend and frontend dependencies:


```powershell
cd backend
python -m pip install -r requirements.txt
cd ..\frontend
npm install
```


In one terminal, start the backend:


```powershell
cd backend
python -m uvicorn app.main:app --reload --port 8000
```


In another terminal, start the frontend:


```powershell
cd frontend
npm run dev -- --open
```


### PDF support on Windows


WeasyPrint may require additional native libraries on Windows. If PDF export fails, follow the [WeasyPrint installation guide](https://doc.courtbouillon.org/weasyprint/stable/first_steps.html). Excel export does not depend on WeasyPrint.


## Configuration


The backend reads settings from environment variables or a `.env` file in the backend working directory. The default database is `backend/quoteforge.db` when the backend is started from the `backend` folder.


| Variable | Default | Description |
| --- | --- | --- |
| `DATABASE_URL` | `sqlite+aiosqlite:///./quoteforge.db` | SQLAlchemy async database URL |
| `ADMIN_PASSWORD` | `quoteforge2024` | Password used by protected product and discount administration endpoints |
| `CORS_ORIGINS` | `http://localhost:5173` | Comma-separated allowed browser origins |
| `UPLOAD_DIR` | `uploads` | Backend upload directory |


For example, create `backend/.env` and set a private admin password before use:


```dotenv
ADMIN_PASSWORD=replace-with-a-private-password
```


Do not commit `.env` files or production credentials. The app creates its database tables and upload directories on backend startup.


## Using QuoteForge


1. Add or sync the product catalog and configure discounts in the admin area.
2. Set up the dealer's profile and GST rates in Settings.
3. Create a quote by selecting products and quantities and entering the client's name.
4. Compare the calculated brand totals, then download the Excel workbook or PDF.
5. Reopen saved quotes from Quote History when needed.


## Repository layout


```text
backend/
  app/
    api/          Quote, product, discount, dealer profile, and dealership APIs
    core/         Settings, database, and dependencies
    models/       Database models
    pdf/          PDF rendering helpers
    routers/      PDF export routes
    services/     Quote calculation, Excel/PDF export, and Excel parsing
    templates/    PDF templates
frontend/
  src/
    components/   Quote, admin, settings, and layout components
    pages/        Quote, history, admin, and settings pages
```
