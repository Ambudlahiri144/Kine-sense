# Kine-sense
A full-stack Python application for video analytics, supporting both uploaded and YouTube videos. It provides real-time engagement tracking, analytics dashboards, and simulated revenue prediction, all through a modern Streamlit frontend and a Django backend with REST and WebSocket support.

---

## Features

- **Upload or analyze YouTube videos**
- **Track user engagement** (watch time, play count, heatmap of watched segments)
- **Real-time analytics dashboard** (live updates via WebSockets)
- **Simulated revenue prediction** based on engagement
- **Gallery and comparison of all analyzed videos**
- **REST API** for video management and analytics
- **Admin panel** for backend management [Admin Portal](http://localhost:8000/admin/).

---
## Architecture Diagram

![Diagram here](![Architecture_diagram_k](https://github.com/user-attachments/assets/dee5cece-a3d9-47d7-ad80-5304b694fb28)
)

---

## Tech Stack

| Layer      | Technology         | Purpose/Role                                      |
|------------|--------------------|---------------------------------------------------|
| Frontend   | Streamlit          | Dashboard UI, video gallery, analytics, charts    |
| Backend    | Django             | API, database, admin, business logic              |
| API        | Django REST Framework | RESTful endpoints for video data               |
| Realtime   | Django Channels    | WebSocket support for live analytics              |
| Server     | Daphne             | ASGI server for Django/Channels                   |
| Database   | SQLite (default)   | Stores video metadata and analytics               |
| ML         | Python (rule-based)| Simulated revenue prediction                      |

---

## How Does It Work?

1. User uploads a video or provides a YouTube link via the Streamlit frontend.
2. Backend stores video metadata and initializes analytics tracking.
3. When a video is played, the frontend opens a WebSocket connection to the backend.
4. User engagement (watch time, play/pause, etc.) is tracked in real-time and stored in the database.
5. Analytics and revenue predictions are updated live and displayed in the Streamlit dashboard.
6. Users can view a gallery of all videos, compare their performance, and see detailed analytics for each video.

---

## Output

- **Streamlit Dashboard:**  
  - Video gallery with thumbnails and stats
  - Detailed analytics for each video (watch time, retention, engagement, predicted revenue)
  - Real-time updates as users interact with videos

- **REST API:**  
  - Endpoints for uploading videos, analyzing YouTube videos, listing and retrieving video analytics

- **Admin Panel:**  
  - Manage all video records and analytics data

---

## Local Setup Instructions

### 1. **Go to Video-Analytics folder**

```sh
cd Video-Analytics
```

### 2. **Create and Activate a Virtual Environment**

```sh
python -m venv venv
# On Windows (PowerShell):
venv\Scripts\Activate.ps1
# On Windows (cmd):
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate
```

### 3. **Install Dependencies**

```sh
pip install -r requirements.txt
```

### 4. **Apply Database Migrations**

```sh
python manage.py migrate
```

### 5. **Run the Django Backend**

```sh
python manage.py runserver
```
- The backend will be available at `http://localhost:8000/`

### 6. **Run the Streamlit Frontend**

Open a new terminal, activate your virtual environment if needed, and run:
```sh
cd streamlit
streamlit run app.py
```
- The frontend will be available at `http://localhost:8501/`


## API Endpoints

| Endpoint                        | Method | Description                        |
|----------------------------------|--------|------------------------------------|
| `/api/videos/`                  | GET    | List all videos                    |
| `/api/upload/`                  | POST   | Upload a new video                 |
| `/api/analyze-youtube/`         | POST   | Analyze a YouTube video            |
| `/api/register-video/`          | POST   | Register a direct video link       |
| `/api/video/<video_id>/`        | GET    | Get analytics for a specific video |

---

## Requirements

```
django
djangorestframework
channels
streamlit
requests
ffmpeg-python
google-api-python-client
```

---

## Project Structure

```
Video-Analytics/
├── backend/
│   ├── analytics/
│   │   ├── models.py
│   │   ├── views.py
│   │   ├── consumers.py
│   │   ├── ml_model.py
│   │   ├── urls.py
│   │   ├── routing.py
│   │   └── ...
│   ├── settings.py
│   ├── urls.py
│   ├── asgi.py
│   └── ...
├── streamlit/
│   └── app.py
├── requirements.txt
└── manage.py
```

---

## Notes

- **YouTube API Key:**  
  The backend uses a hardcoded YouTube Data API key for demonstration. For production, set this via environment variable for security.
- **Media Storage:**  
  Uploaded videos and thumbnails are stored in the `media/` directory.
- **WebSocket Support:**  
  Real-time analytics require both backend and frontend to be running.

---
