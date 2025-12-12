🚀 Semantic Product Recommender System
Flask + FAISS + Sentence Transformers

This project is an intelligent semantic search–based product recommender.
It uses SentenceTransformer embeddings and FAISS vector search to recommend products based on meaning, not keywords.

✨ Features

🔍 Semantic product search (understands meaning, not keywords)

⚡ FAISS-based vector search for ultra-fast similarity matching

🧠 SentenceTransformer model (all-MiniLM-L6-v2) for embeddings

🔄 LRU caching for repeated queries

🧵 Thread-safe FAISS indexing

📈 Admin endpoints (stats, reload, health check)

🧹 Handles missing values and validates CSV structure

📂 Project Structure
.
│── app.py               # Flask backend with semantic recommender
│── templates/
│     └── index.html     # Frontend UI (search page)
│── products.csv         # Product dataset (user-provided)
│── README.md            # Documentation

🗂 Dataset Format (products.csv)

Your CSV must contain:

name	description

Optional: id, category, etc.

Example:

name,description
Air Purifier,HEPA air purifier for home and office
Electric Kettle,Fast-boil stainless steel kettle with auto shut-off
Portable Blender,USB rechargeable mini blender

📦 Installation

Install dependencies:

pip install flask pandas sentence-transformers faiss-cpu numpy


If faiss doesn't install, use:

pip install faiss-cpu

▶️ Running the App

Place your CSV file at:

C:\Users\Lenovo\Downloads\products.csv


Start the server:

python app.py


Open in browser:

http://localhost:5000

🌐 API Endpoints
1. GET /

Loads the search UI.

2. POST /recommend

Returns top semantic product matches.

Example Request:
{
  "query": "air purifier",
  "top_k": 5
}

Example Response:
{
  "error": false,
  "query": "air purifier",
  "total_results": 5,
  "results": [
    {
      "name": "Air Purifier",
      "description": "HEPA air purifier for home",
      "similarity_score": 92.14,
      "rank": 1
    }
  ]
}

3. GET /product/<id>

Get full details of a product by ID.

4. GET /stats

Returns model and index statistics:

total products

embedding dimension

model name

cache usage

5. POST /reload

Reload products from CSV without restarting server.

6. GET /health

Basic health check:

{
  "status": "healthy",
  "service": "Product Recommender",
  "products_loaded": true
}

🧠 How It Works (Simplified)

Load CSV → clean data

Convert each product into a combined text string

Generate embeddings using SentenceTransformer

Normalize embeddings and build FAISS index

On each search:

Embed the query

Compute similarity using FAISS

Return ranked products with similarity scores

🛠 Technologies Used

Flask — web API

SentenceTransformers — embedding model

FAISS — vector similarity search

NumPy / Pandas

LRU Cache for performance optimization

📜 License

Free to use for personal and commercial projects.
