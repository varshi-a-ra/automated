# Automated Timetable Generator

This project contains two different approaches to build a timetable generator:

1. **Streamlit single-file app** (`advanced_app.py`) – a quick frontend/backend bundle you can run with Streamlit.
2. **Separated backend + frontend** – a FastAPI service that does the scheduling logic and a plain HTML/JavaScript frontend that talks to it.

---

## Backend (FastAPI)

### Requirements

```bash
python -m venv .venv        # create virtual env
. .venv/Scripts/Activate.ps1 # on Windows PowerShell
pip install -r backend/requirements.txt
```

### Run

```powershell
uvicorn backend.main:app --reload
```

The API will listen on `http://localhost:8000`.

### Endpoint

- `POST /generate` – accepts a JSON body matching `backend/main.py`'s `InputData` model:
  ```json
  {
    "days":5,
    "periods":6,
    "classes":["Class A","Class B"],
    "rooms":["R1","R2"],
    "subjects":{"Math":4,"Physics":3},
    "faculty":[{"name":"Alice","subjects":["Math"],"unavailable":["1-1"]}]
  }
  ```
  Returns schedules and statistics.

## Frontend

Open `frontend/index.html` in a browser (you can simply double‑click the file).
The page contains a form to enter configuration and will call the backend when you click **Generate timetable**. Results are rendered below as HTML tables.

> **Note:** The frontend assumes the backend is running at `http://localhost:8000`. If you change the host/port, update the `fetch` URL in the script.

## Streamlit alternative

If you prefer the single-file UI, run:

```powershell
pip install streamlit pandas
streamlit run advanced_app.py
```

That app embeds the generator logic and provides the same inputs and output views.

---

Feel free to extend the scheduler, add persistence, or integrate a richer frontend framework (React/Vue) using the API from `backend/main.py`.   
