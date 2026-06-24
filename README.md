# Project RED

Project RED is a multi-platform blood donation and hospital coordination system with:
- a Django + DRF backend API,
- two React web frontends (`frontend` with Vite, `project-red-frontend` with CRA),
- and a Flutter mobile app (`mobile`).

## Repository Structure

```text
Project-RED/
├── core/                  # Django app: models, serializers, views, websocket consumers
├── project_red/           # Django project settings, ASGI/WSGI, root URLs
├── frontend/              # React + Vite frontend
├── project-red-frontend/  # React (Create React App) frontend
├── mobile/                # Flutter mobile app
├── manage.py              # Django management entrypoint
└── requirements.txt       # Python backend dependencies
```

## Technical Architecture

### Backend (Django + DRF)
- **Framework:** Django 4.2
- **API Layer:** Django REST Framework
- **Auth:** JWT (`rest_framework_simplejwt`) + session auth
- **Database:** PostgreSQL
- **Realtime:** Django Channels (ASGI + WebSocket routing in `core/routing.py`)
- **API Docs:** drf-yasg (Swagger + ReDoc endpoints)
- **CORS:** `django-cors-headers`

Core domain models include:
- `User`, `Hospital`, `HospitalUser`
- `BloodRequest`, `Donation`, `BloodTest`
- `ChatRoom`, `Message`, `Notification`
- `DonorHospitalAssignment`

Primary API routing is under `core/urls.py` with `/api/...` endpoints.

### Web Frontend A (`frontend/`)
- **Runtime:** React 19 + Vite 6
- **Routing:** `react-router-dom`
- **UI:** MUI, Emotion, Tailwind CSS
- **Data/HTTP:** Axios
- **Charts:** Recharts
- **Realtime client:** Socket.IO client
- **Utilities:** jsPDF, html2canvas, jwt-decode, react-toastify, framer-motion

### Web Frontend B (`project-red-frontend/`)
- **Runtime:** React 19 + Create React App (`react-scripts`)
- **Routing/Data/UI:** `react-router-dom`, Axios, MUI/Emotion
- **Testing:** React Testing Library + Jest DOM

### Mobile App (`mobile/`)
- **Framework:** Flutter (Dart SDK ^3.8.1)
- **Networking:** `http`
- **Location:** `geolocator`
- **Local storage:** `shared_preferences`
- **Media/input:** `image_picker`
- **Formatting/i18n:** `intl`

## Backend Dependencies (`requirements.txt`)

- `Django`
- `djangorestframework`
- `django-cors-headers`
- `django-environ`
- `django-rest-auth`
- `django-allauth`
- `drf-yasg`
- `python-decouple`
- `psycopg2-binary`
- `requests`
- `Pillow`
- `channels`
- `channels-redis`

> Note: `project_red/settings.py` also references `rest_framework_simplejwt`, which should be installed in the backend environment.

## Environment Configuration (Backend)

`project_red/settings.py` reads these key environment variables:
- `SECRET_KEY`, `DEBUG`, `ALLOWED_HOSTS`
- `DB_NAME`, `DB_USER`, `DB_PASSWORD`, `DB_HOST`, `DB_PORT`
- `EMAIL_BACKEND`, `EMAIL_HOST`, `EMAIL_PORT`, `EMAIL_USE_TLS`, `EMAIL_HOST_USER`, `EMAIL_HOST_PASSWORD`
- `FRONTEND_URL`, `DEFAULT_FROM_EMAIL`
- `OPENAI_API_KEY`, `GOOGLE_MAPS_API_KEY`

Create a local `.env` file (do not commit it) with these values before running backend services.

## Local Development Setup

## 1) Backend

```bash
cd /home/runner/work/Project-RED/Project-RED
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
python manage.py migrate
python manage.py runserver
```

### 2) Frontend (Vite)

```bash
cd /home/runner/work/Project-RED/Project-RED/frontend
npm install
npm run dev
```

### 3) Frontend (CRA)

```bash
cd /home/runner/work/Project-RED/Project-RED/project-red-frontend
npm install
npm start
```

### 4) Mobile (Flutter)

```bash
cd /home/runner/work/Project-RED/Project-RED/mobile
flutter pub get
flutter run
```

## Build / Lint / Test Commands

### `frontend/` (Vite)
- `npm run lint`
- `npm run build`

### `project-red-frontend/` (CRA)
- `npm test`
- `npm run build`

### `mobile/` (Flutter)
- `flutter test`

### Backend (Django)
- `python manage.py check`
- `python manage.py test`

## API Documentation Endpoints

When backend is running:
- Swagger UI: `/swagger/`
- ReDoc: `/redoc/`
- OpenAPI schema: `/swagger.json` or `/swagger.yaml`
