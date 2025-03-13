# LinkedIn Insights Microservice

## 📌 Overview
The LinkedIn Insights Microservice is built to extract valuable insights from LinkedIn company pages. It scrapes company information, recent posts, and engagement metrics. This service uses **FastAPI** for building the RESTful API, **MongoDB** for data storage, and supports **asynchronous scraping** for optimal performance.

---

## 🚀 Key Features
- **Scrape LinkedIn company pages** for detailed insights
- **Extract essential information** like company profiles, posts, and engagement data
- **MongoDB storage** for persistent data management
- **FastAPI-powered RESTful API** with pagination and filtering
- **Optional Redis integration** for improved performance through caching
- **Environment variables support** via `.env` configuration

---

## 🏗 Project Structure
```
linkedin_insights_microservice/
│-- app/
│   ├── api/
│   │   ├── endpoints/
│   │   │   ├── scrape.py      # Scraping related endpoints
│   │   │   ├── page.py        # Endpoints for page data retrieval
│   │   │   ├── post.py        # Endpoints for post data retrieval
│   │   │   ├── user.py        # Endpoints for user interaction
│   ├── core/
│   │   ├── config.py          # Configuration settings for environment variables
│   │   ├── database.py        # MongoDB connection management
│   │   ├── cache.py           # Redis connection and cache handling (optional)
│   ├── models/
│   │   ├── page.py            # MongoDB models for page data
│   │   ├── post.py            # MongoDB models for post data
│   │   ├── user.py            # MongoDB models for user data
│   ├── services/
│   │   ├── scraper_service.py # Logic for scraping LinkedIn data
│   │   ├── page_service.py    # Logic for handling page data
│   ├── main.py                # FastAPI application entry point
│-- .env                        # Environment variables configuration file
│-- .gitignore                  # Git ignore file
│-- docker-compose.yml          # Docker Compose file for containerization
│-- Dockerfile                  # Dockerfile for app container
│-- requirements.txt            # Python dependencies
│-- README.md                   # Project documentation
│-- summary.txt                 # Project summary and notes

```

---

## ⚙️ Setup & Installation

### **1️⃣ Clone the Repository**
git clone https://github.com/your-repo/linkedin_insights
cd linkedin_insights

### **2️⃣ Set Up Virtual Environment**
python3 -m venv .venv
source .venv/bin/activate  # Mac/Linux
.venv\Scripts\activate     # Windows

### **3️⃣ Install Required Packages**
pip install -r requirements.txt

### **4️⃣ Set Up Environment Variables**
Create a `.env` file in the root directory and define the required variables:

MONGO_URI=mongodb://localhost:27017
DATABASE_NAME=linkedin_insights
LI_AT-{your_linkedin_cookie}

### **5️⃣ Run the FastAPI Server**
uvicorn app.main:app --reload

Access the API at: http://localhost:8000

---

## 📡 API Endpoints

### **1️⃣ Scrape LinkedIn Company Page**
POST /api/scraper/scrape

**Request Body:**
{
  "url": "https://www.linkedin.com/company/hp",
  "type": "company"
}

**Response:**
{
  "status": "success",
  "message": "Successfully scraped company page",
  "data": { Data_Context }
}

### **2️⃣ Retrieve All Scraped Pages**
GET /api/pages

### **3️⃣ Retrieve a Specific Page by ID**
GET /api/pages/{page_id}

---

## 🛠 Troubleshooting

### **1️⃣ Module Not Found Error**
Ensure you are importing modules correctly:

from app.core.database import pages_collection

### **2️⃣ MongoDB Connection Issues**
Verify that MongoDB is running:
mongod --dbpath /path/to/data/db

Ensure your `.env` file has the correct `MONGO_URI`.

Additionally, if you're using LinkedIn scraping, ensure that you have set up the necessary LinkedIn **cookies (LI_AT)**.

---

### Docker and Redis Setup (Optional)

If you want to use **Redis** for caching or running the service within containers, you can use the `docker-compose.yml` file to set up the app and Redis services easily.

docker-compose up --build

This will build the Docker image and start the app along with Redis.
