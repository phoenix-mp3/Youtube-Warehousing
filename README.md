# YouTube Data Harvesting and Warehousing by Hemanth Karthick

Welcome to the **YouTube Data Harvesting and Warehousing** project! This application enables users to access, analyze, and store data from various YouTube channels, leveraging powerful technologies like PostgreSQL, MongoDB, and Streamlit.

## 🚀 Project Overview

The application provides a seamless interface for retrieving, saving, and querying YouTube channel and video data. Built with Python and a suite of robust tools, it supports the following features:

- **Data Retrieval:** Fetch channel and video information using the YouTube Data API v3.
- **Data Storage:** Store raw data in MongoDB, acting as a data lake.
- **Data Migration:** Migrate data from MongoDB to PostgreSQL for structured querying and analysis.
- **Data Querying:** Search and retrieve data from the SQL database with various options.

## 🔧 Tools and Libraries

- **Streamlit:** Build interactive and user-friendly UIs for data interaction.
- **Python:** Core programming language for data retrieval, processing, and visualization.
- **Google API Client:** Interface with YouTube's Data API v3 to fetch data.
- **MongoDB:** Document database for storing unstructured or semi-structured data.
- **PostgreSQL:** Relational database for managing structured data with advanced SQL features.

## 📦 Required Libraries

Ensure you have the following Python libraries installed:

```bash
pip install google-api-python-client
pip install streamlit
pip install psycopg2
pip install pymongo
pip install pandas
```

## 🔍 Features

### Data Retrieval

Fetch channel and video data from YouTube using the API:

```python
from googleapiclient.discovery import build

# Set up YouTube API client
youtube = build('youtube', 'v3', developerKey='YOUR_API_KEY')

# Example function to get channel details
def get_channel_details(channel_id):
    request = youtube.channels().list(
        part='snippet,contentDetails,statistics',
        id=channel_id
    )
    response = request.execute()
    return response
```

### Data Storage

Store data in MongoDB:

```python
from pymongo import MongoClient

# Connect to MongoDB
client = MongoClient('mongodb://localhost:27017/')
db = client['youtube_data']

# Example function to insert data
def store_channel_data(channel_data):
    db.channels.insert_one(channel_data)
```

### Data Migration

Move data from MongoDB to PostgreSQL:

```python
import psycopg2

# Connect to PostgreSQL
conn = psycopg2.connect(dbname='youtube_db', user='user', password='password', host='localhost')
cur = conn.cursor()

# Example function to insert data into PostgreSQL
def migrate_channel_data():
    data = db.channels.find()
    for item in data:
        cur.execute("INSERT INTO channels (id, name, description) VALUES (%s, %s, %s)",
                    (item['id'], item['name'], item['description']))
    conn.commit()
```

### Data Querying

Query and analyze data with SQL:

```python
# Example function to query channel data
def query_channel_data(name):
    cur.execute("SELECT * FROM channels WHERE name = %s", (name,))
    results = cur.fetchall()
    return results
```

## ⚠️ Ethical Considerations

Respect YouTube’s terms of service and data protection regulations. Ensure responsible data handling and prevent misuse. Prioritize privacy and integrity in your data scraping processes.

## 🌐 Getting Started

1. **Clone the Repository:**

    ```bash
    git clone https://github.com/yourusername/youtube-data-warehousing.git
    ```

2. **Install Dependencies:**

    ```bash
    pip install -r requirements.txt
    ```

3. **Run the Application:**

    ```bash
    streamlit run app.py
    ```

4. **Configure Your API Keys:**

    Update `config.py` with your YouTube API key and database connection details.

## 🛠️ Contributing

Contributions are welcome! Please open an issue or submit a pull request on GitHub.

## 📄 License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
