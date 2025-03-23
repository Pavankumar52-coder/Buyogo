# Buyogo
# Hotel Bookings Analytics & RAG-based Q&A API

## Overview
This project analyzes hotel booking data, extracts insights, and provides a Retrieval-Augmented Generation (RAG)-based Q&A system using sentence embeddings and a transformer model.

## Features
- **Data Preprocessing**: Handled missing values using replacement method and processes key columns.
- **Visualization**: Generated revenue trends(lineplot), cancellation rates(value), and geographical distribution insights(barplot).
- **RAG-based Q&A**: Used FAISS vector database for similarity search and a transformer model for text generation.
- **FastAPI Server**: Provides API endpoints for analytics and Q&A.
- **Ngrok Integration**: Exposes API publicly for testing.

## Requirements
Ensure you have Python 3.10+ and the following dependencies installed:

```sh
pip install pandas matplotlib seaborn faiss-cpu sentence-transformers transformers fastapi uvicorn pyngrok
```

## Setup & Running the API
### 1. Upload Dataset
Use Google Colab to upload `hotel_bookings.csv`.

```python
from google.colab import files
files.upload()
```

### 2. Run the Code
Copy and execute the Python script in a Colab notebook.

### 3. Start FastAPI Server
Run the following command to start the server:

```python
import uvicorn
uvicorn.run(app, host="0.0.0.0", port=8000)
```

### 4. Access API via Ngrok
Run:

```python
from pyngrok import ngrok
public_url = ngrok.connect(8000).public_url
print(f"FastAPI running at: {public_url}")
```

## API Endpoints
### Analytics Endpoint
**URL:** `/analytics`  
**Method:** `POST`  
**Response:**
```json
{
  "cancellation_rate": "20.35%",
  "top_countries": {
    "USA": 5000,
    "UK": 4200
  }
}
```

### Q&A Endpoint
**URL:** `/ask`  
**Method:** `POST`  
**Request:**
```json
{
  "query": "What is the total revenue for July 2017?"
}
```
**Response:**
```json
{
  "response": "The total revenue for July 2017 was approximately $1.2M."
}
```

## Notes
- Ensure that you should have access to the Hugging Face model (`mistralai/Mistral-Small-24B-Instruct-2501`) before running.
- You should also have access token to use the abive model.
- Adjust FAISS indexing if working with large datasets.

## Author
Developed by,
Pavankumar Tirumalasetty
