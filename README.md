# 🚂 KPA Form Data — FastAPI + PostgreSQL Project

This project is developed as per the **KPA assignment specifications**.\
It provides RESTful APIs for submitting and retrieving KPA form data such as **Bogie Checksheet** and **Wheel Specifications**, using **FastAPI**, **PostgreSQL**, and **SQLAlchemy**.

---

## 📌 Project Specifications

- **Framework:** FastAPI
- **Database:** PostgreSQL
- **ORM:** SQLAlchemy
- **Environment Variables:** python-dotenv for DB connection config
- **API Documentation:** Swagger (at `/docs`)
- **API Testing:** Postman collection

This project follows the **OpenAPI spec** provided — strictly using **POST** for submitting form data and **GET** with query parameters for fetching it.

---

## ⚙️ Technologies Used

- Python 3.10+
- FastAPI
- SQLAlchemy
- psycopg2-binary (PostgreSQL driver)
- python-dotenv
- Uvicorn
- Postman

---

## ✅ Database Design & Algorithm

### 🗂️ Bogie Checksheet Flow

- Each Bogie Checksheet has:
  - `formNumber` *(unique)*
  - `inspectionBy`, `inspectionDate`
  - Details: `bogieChecksheet`, `bmbcChecksheet`, `bogieDetails`

**Algorithm:**

1. Receive JSON payload via **POST** `/api/forms/bogie-checksheet`
2. Validate with Pydantic schema
3. Insert into PostgreSQL using SQLAlchemy
4. Return success message with `formNumber`

### 🗂️ Wheel Specifications Flow

- Uses **GET** `/api/forms/wheel-specifications` with:
  - `formNumber`
  - `submittedBy`
  - `submittedDate`

**Algorithm:**

1. Receive query params
2. Filter rows with SQLAlchemy query
3. Return filtered data as JSON

---

## 🚀 Setup Instructions — Step by Step

### ✅ 1️⃣ Clone or download the project

```bash
cd C:\Users\YourName\Desktop\kpa_api_assignment_real
```

### ✅ 2️⃣ Create & activate virtual environment

```bash
python -m venv venv

# Windows:
venv\Scripts\activate
# macOS/Linux:
source venv/bin/activate
```

### ✅ 3️⃣ Install required packages

```bash
pip install -r requirements.txt
```

### ✅ 4️⃣ Create `.env` file

In the project root:

```env
DB_HOST=localhost
DB_PORT=5432
DB_NAME=kpa_db
DB_USER=postgres
DB_PASSWORD=your_pg_password
```

### ✅ 5️⃣ Create the PostgreSQL database

```sql
-- In psql shell:
CREATE DATABASE kpa_db;
```

### ✅ 6️⃣ Run the FastAPI server

```bash
uvicorn app.main:app --reload
```

Visit Swagger UI:

- [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)

---

## ✅ How to Use Postman

1. Import `yourname_postman_collection.json`
2. For **POST**:
   - URL: `http://127.0.0.1:8000/api/forms/bogie-checksheet`
   - Method: POST
   - Body: raw JSON with **unique** `formNumber`
3. For **GET**:
   - URL: `http://127.0.0.1:8000/api/forms/wheel-specifications?formNumber=WHEEL-2025-001&submittedBy=user_id_123&submittedDate=2025-07-03`
   - Method: GET

✅ Right-click your collection → Export → `yourname_postman_collection.json`

---

## ✅ Example Requests

### ➡️ POST `/api/forms/bogie-checksheet`

```json
{
  "formNumber": "BOGIE-2025-001",
  "inspectionBy": "user_id_456",
  "inspectionDate": "2025-07-03",
  "bogieChecksheet": {
    "axleGuide": "Worn"
  },
  "bmbcChecksheet": {
    "adjustingTube": "DAMAGED"
  },
  "bogieDetails": {
    "bogieNo": "BG1234",
    "dateOfIOH": "2025-07-01",
    "deficitComponents": "None"
  }
}
```

### ➡️ Example Response

```json
{
  "success": true,
  "message": "Bogie checksheet submitted successfully.",
  "data": {
    "formNumber": "BOGIE-2025-001",
    "status": "Saved"
  }
}
```

### ➡️ GET `/api/forms/wheel-specifications`

```json
{
  "success": true,
  "message": "Filtered wheel specification forms fetched successfully.",
  "data": [ ... ]
}
```

---

## 📝 Important Notes

- ✅ Always use a \*\*unique \*\*\`\` for each POST
- ✅ Use Swagger UI at `/docs` to test APIs
- ✅ Watch the terminal for DB errors (e.g., duplicate keys)
- ✅ Use Postman export as `aashu_collection.json` (I Have also uploaded the File on the Github repository as well) 

---

## ✅ Author

Assignment completed per PDF specifications — no external resources used.\
Built with **FastAPI + PostgreSQL + Swagger + Postman**.

**Good luck and happy coding! 🚀**

