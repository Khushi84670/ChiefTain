# Hotel Concierge AI Chatbot 🏨

![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)
![FastAPI](https://img.shields.io/badge/FastAPI-005571?style=for-the-badge&logo=fastapi)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Google Gemini](https://img.shields.io/badge/Google%20Gemini-8E75B2?style=for-the-badge&logo=google-gemini&logoColor=white)
![Supabase](https://img.shields.io/badge/Supabase-3ECF8E?style=for-the-badge&logo=supabase&logoColor=white)
![Twilio](https://img.shields.io/badge/Twilio-F22F46?style=for-the-badge&logo=Twilio&logoColor=white)

A next-gen AI-powered hotel chatbot and admin dashboard built for the **IIT Hackathon 2025 (Challenge: AIChieftain)**. This project handles room bookings, service requests, and FAQs, and performs sentiment analysis using cutting-edge LLM technology.

---

## 🌐 Live Demo

You can test the live application here:

-   **Chatbot Interface:** [https://chief-train-hr5t.vercel.app](https://chief-train-hr5t.vercel.app)
-   **Admin Panel:** [https://chief-train-hr5t.vercel.app/admin](https://chief-train-hr5t.vercel.app/admin)

---

## 🚀 Features

-   🤖 **AI Chatbot:** Voice and text-based interaction for a seamless user experience.
-   📅 **Booking System:** Check room availability and book rooms directly through the chat.
-   🛎️ **Room Service:** Guests can request room service, which triggers an instant SMS confirmation via Twilio.
-   🧠 **Smart Replies:** AI-generated, context-aware responses powered by Google Gemini 1.5 Flash.
-   📊 **Sentiment Analysis:** Real-time analysis of guest conversations to gauge satisfaction.
-   🖥️ **Admin Dashboard:** A comprehensive panel for staff to view sentiment summaries and manage all bookings and service requests.

---

## 👩‍💻 My Role in the Hackathon

- Contributed to backend development using FastAPI
- Integrated Google Gemini LLM for chatbot responses
- Configured Supabase database connectivity
- Assisted in API testing and debugging
- Supported frontend-backend integration

---

## 🏛️ System Architecture

The system is built on a modern, decoupled architecture ensuring scalability and maintainability.



[Image of a system architecture diagram]


### Components:
1.  **Frontend (React):** A responsive user interface for both the guest chatbot and the admin dashboard. It handles user input and communicates with the backend via REST APIs.
2.  **Backend (FastAPI):** A powerful Python backend that serves as the brain of the operation. It processes requests, integrates with the LLM, and connects to external services.
3.  **Database (Supabase):** A PostgreSQL database that stores all chat history, bookings, and room service requests.
4.  **LLM (Google Gemini):** Used for generating intelligent chat responses and performing sentiment analysis on guest messages.
5.  **External Services:**
    -   **Twilio:** For sending SMS notifications for room service requests.
    -   **SendGrid:** For sending email confirmations for room bookings.

### Data Flow:
1.  A guest interacts with the React chatbot UI.
2.  The frontend sends an API request to the FastAPI backend.
3.  The backend processes the input, querying the Gemini LLM for a response and interacting with the Supabase database.
4.  The response is sent back to the user and the interaction is logged in the database.
5.  Admins can view all data and AI-generated summaries on the React admin dashboard.

---

## 🛠️ Tech Stack

-   **Frontend:** React.js
-   **Backend:** FastAPI (Python)
-   **LLM Integration:** LangChain with Google Gemini 1.5 Flash
-   **Database:** Supabase (PostgreSQL)
-   **Email Service:** SendGrid
-   **SMS Service:** Twilio

---

## 🔧 Getting Started: Local Setup

Follow these instructions to get a copy of the project up and running on your local machine.

### Prerequisites

-   Git
-   Python 3.8+ and Pip
-   Node.js and npm

### Installation

1.  **Clone the repository:**
    ```sh
    git clone [https://github.com/your-username/your-repo-name.git](https://github.com/your-username/your-repo-name.git)
    cd your-repo-name
    ```

2.  **Set up Backend (FastAPI):**
    -   Navigate to the backend directory:
        ```sh
        cd backend
        ```
    -   Create and activate a virtual environment:
        ```sh
        python -m venv venv
        # On Windows
        venv\Scripts\activate
        # On macOS/Linux
        source venv/bin/activate
        ```
    -   Install the required Python packages:
        ```sh
        pip install -r requirements.txt
        ```
    -   Create a `.env` file in the `backend` directory and add your credentials:
        ```env
        SUPABASE_URL="your_supabase_url"
        SUPABASE_KEY="your_supabase_api_key"
        OPENAI_API_KEY="your_google_gemini_api_key" # Note: Name may vary based on LangChain setup
        SENDGRID_API_KEY="your_sendgrid_api_key"
        TWILIO_ACCOUNT_SID="your_twilio_account_sid"
        TWILIO_AUTH_TOKEN="your_twilio_auth_token"
        TWILIO_PHONE_NUMBER="your_twilio_phone_number"
        ```
    -   Start the backend server:
        ```sh
        uvicorn app.main:app --reload
        ```
    The backend will be running at `http://127.0.0.1:8000`.

3.  **Set up Frontend (React):**
    -   Open a new terminal and navigate to the frontend directory:
        ```sh
        cd frontend
        ```
    -   Install the required npm packages:
        ```sh
        npm install
        ```
    -   Start the frontend development server:
        ```sh
        npm run dev
        ```
    The frontend will be accessible at `http://localhost:5173`.

---

## 🔹 How to Use

-   **Guest User:** Interact with the chatbot at the main URL to ask questions, book a room, or request service.
-   **Admin User:** Navigate to `/admin` and log in with the password `hotel@123` to access the dashboard.

---

## 🔖 API Documentation

The backend API is served from the base URL: `https://chieftrain.onrender.com`

### 💬 Chat
-   `POST /chat/`
    -   Handles user messages and returns an AI response.
    -   **Body:** `{ "user_id": "string", "message": "string" }`
    -   **Response:** `{ "response": "AI-generated message" }`

-   `GET /chat/sentiment-summary-ai`
    -   Returns an AI-generated summary of chat sentiment.
    -   **Response:** `{ "top_positive": [], "top_negative": [], "top_neutral": [] }`

### 📅 Booking
-   `POST /booking/`
    -   Submits a new booking request.
    -   **Body:** `{ "user_id": "string", "name": "string", "room_type": "string", "check_in": "YYYY-MM-DD", "check_out": "YYYY-MM-DD" }`

-   `GET /booking/`
    -   Fetches all booking records.

-   `PATCH /booking/{id}/status?status=<status>`
    -   Updates a booking status. `status` can be `confirmed` or `rejected`.

-   `DELETE /booking/{id}`
    -   Deletes a booking record.

-   `GET /booking/availability/`
    -   Checks room availability for a given date range.
    -   **Query Params:** `check_in=YYYY-MM-DD`, `check_out=YYYY-MM-DD`

### 🛎️ Room Service Request
-   `POST /request/`
    -   Submits a new room service request and sends an SMS.
    -   **Body:** `{ "room_number": "string", "phone_number": "string", "request": "string" }`

-   `GET /request/`
    -   Fetches all service requests.

-   `PATCH /request/{id}/resolve`
    -   Marks a service request as resolved.

-   `DELETE /request/{id}`
    -   Deletes a service request.

### 📖 FAQ
-   `GET /faq/`
    -   Returns a list of hardcoded frequently asked questions.    
> Note: This project was developed collaboratively. I have modified, configured, and deployed my own working version for learning and demonstration purposes.
