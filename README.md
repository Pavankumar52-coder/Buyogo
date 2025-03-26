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

### Q&A Endpoint
**URL:** `/ask`  
**Method:** `POST`  
**Request:**

Sample Test Queries & Expected Answers:
The following queries covers different aspects of booking analytics and RAG-based question answering.

1. Revenue Trends:
Query: "Show me total revenue for July 2017."
Expected Answer: Sum of adr * (stays_in_week_nights + stays_in_weekend_nights) for bookings in July 2017.

Query: "What was the average daily rate (ADR) for August 2016?"
Expected Answer: Mean adr for bookings in August 2016.

2. Cancellation Analysis:
Query: "What percentage of bookings were canceled?"
Expected Answer: (sum(is_canceled) / total_bookings) * 100

Query: "Which month had the highest cancellation rate?"
Expected Answer: Month with the highest (canceled bookings / total bookings) * 100.

3. Geographical Insights:
Query: "Which country had the most bookings?"
Expected Answer: The country with the highest count in the country column.

Query: "Which locations had the highest booking cancellations?"
Expected Answer: The country with the highest sum of is_canceled == 1.

4. Booking Lead Time Analysis:
Query: "What is the average lead time for confirmed bookings?"
Expected Answer: Mean of lead_time where is_canceled == 0.

Query: "What is the distribution of lead times for bookings?"
Expected Answer: A histogram of lead_time.

5. Additional Analytics:
Query: "What is the average price of a hotel booking?"
Expected Answer: Mean adr.

Query: "What is the most common market segment for bookings?"
Expected Answer: The most frequent value in market_segment.

## Notes
- Ensure that you should have access to the Hugging Face model (`google/flan-t5-small`) before running.
- You should also have access token to use the abive model.
- Adjust FAISS indexing if working with large datasets.

## Author
Developed by,
Pavankumar Tirumalasetty
