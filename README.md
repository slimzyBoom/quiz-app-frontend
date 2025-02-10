# Quiz App Frontend

This is the frontend of the Quiz App, built using **Vue.js 3** and **Tailwind CSS**. It interacts with a Node.js backend to fetch quiz questions and track user progress.

## Features
- Fetches multiple-choice quiz questions from the backend
- Displays one question at a time
- Tracks user score and progress
- Shows final results after completing the quiz

## Tech Stack
- **Vue.js 3** (Composition API)
- **Tailwind CSS** (for styling)
- **Axios** (for API requests)

## Installation & Setup
### 1. Clone the repository
```sh
 git clone <repository-url>
 cd quiz-app-frontend
```

### 2. Install dependencies
```sh
npm install
```

### 3. Start the development server
```sh
npm run dev
```

## Project Structure
```
quiz-app-frontend/
│── src/
│   ├── App.vue       # Root component
│   ├── main.js       # Vue initialization
│── public/
│── package.json
│── README.md
```

## API Endpoints (Backend Required)
Ensure the backend is running on `http://localhost:5000`.
- **GET /questions** → Fetch quiz questions
- **POST /check-answer** → Check user answer



