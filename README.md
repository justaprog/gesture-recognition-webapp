# gesture-recognition-webapp
This project is a gesture recognition web application with a Vue.js frontend and a FastAPI backend. The goal is to capture video from the user's webcam, recognize gestures using a vision model, and store or process the results through backend services.

## Architecture
The recommended architecture is a layered system where Vue.js handles live interaction and gesture recognition, FastAPI manages application logic and persistence, and the ML training pipeline remains separated from the production application. This structure keeps the system modular, scalable, and easier to maintain.

For more details on the architecture, see the [Architecture Documentation](docs/architecture.md) and the [API Documentation](docs/api.md).
### System Overview
The system consists of three main parts:
- **Frontend (Vue.js)**: Handles user interaction, webcam access, live preview, and displaying gesture predictions.
- **Backend (FastAPI)**: Provides APIs for session handling, gesture event storage, model metadata, and optional inference (in case the model inference becomes too heavy).
- **ML Layer**: Contains the gesture recognition model and related preprocessing or postprocessing logic.

### High-Level Architecture
#### Client Application
- Runs in the browser
- Accesses webcam
- Run gesture inference using the fine-tuned MediaPipe gesture recognition model (low latency and better user experience)
- Displays live gesture recognition results
- Sends recognized gesture events to backend

#### Backend Services
API Server:
- Exposes REST endpoints
- Validates incoming requests
- Stores gesture/session data
- Optionally performs inference if the model is too heavy for client-side execution
Database:
- Stores sessions, gesture events, and possibly model version metadata

#### Model Training
- Separate scripts for training/fine-tuning and exporting the gesture recognition model

### Data Flow
1. User opens the web app
2. Frontend requests webcam permission
3. Video frames are captured in the browser
4. Gesture model predicts the current gesture
5. Frontend displays the result in real time
6. Frontend sends gesture event data to the backend
7. Backend validates and stores the event in the database

### Stack
- **Frontend**: Vue.js
- **Backend**: FastAPI, SQLAlchemy (for database interactions), PostgreSQL
- **Model Training**: Python, MediaPipe
- **Deployment**: Docker, Docker Compose

### Risks and Trade-Offs
#### Frontend Inference
Advantages: 
- Low latency
- Better responsiveness
- Lower backend cost

Disadvantages:
- Device/browser compatibility differences
- Performance depends on client hardware

### Initial MVP
- Vue frontend with webcam preview
- Integration of the existing fine-tuned MediaPipe gesture recognition model
- Frontend-side gesture recognition
- FastAPI backend for session creation and gesture event storage
- PostgreSQL database
- Basic architecture documentation and API documentation