npx @google/gemini-cli
BACKEND

npm install nodemon --save-dev

npm run dev

FRONTEND

npm install

npm run dev

GIT PUSH

git init git add . git commit -m "Initial commit"

git remote add origin https://github.com/your-username/mern-task-manager.git git branch -M main git push -u origin main

After updates: git add . git commit -m "update" git push

.gitignore .env node_modules/ dist/

.json { "name": "backend", "version": "1.0.0", "type": "module", "main": "server.js", "scripts": { "start": "node server.js", "dev": "nodemon server.js" },
MERN Task Manager - Commands, API Paths & Deployment Guide

========================
1. PROJECT SETUP
========================
mkdir mern-task-manager
cd mern-task-manager

========================
2. BACKEND SETUP
========================
mkdir backend
cd backend
npm init -y

Install dependencies:
npm install express mongoose cors dotenv
npm install nodemon --save-dev

------------------------
Backend Folder Structure
------------------------
backend/
  models/Task.js
  routes/tasks.js
  server.js
  .env

------------------------
IMPORTANT API BASE PATH
------------------------
All backend APIs start with:
/api/tasks

Examples:
GET    /api/tasks        -> Get all tasks
POST   /api/tasks        -> Create task
DELETE /api/tasks/:id    -> Delete task

------------------------
server.js (IMPORTANT)
------------------------
app.use('/api/tasks', require('./routes/tasks'));

------------------------
ENV FILE (.env)
------------------------
MONGO_URI=your_mongodb_connection
PORT=5000

------------------------
Run backend:
------------------------
npm run dev

Backend runs on:
http://localhost:5000

========================
3. FRONTEND SETUP
========================
cd ..
npm create vite@latest frontend
cd frontend
npm install
npm install axios

------------------------
Frontend Folder Structure
------------------------
frontend/
  src/
    api.js
    App.jsx
    components/

------------------------
ENV FILE (frontend/.env)
------------------------
VITE_API_URL=http://localhost:5000/api

IMPORTANT:
Frontend talks to backend using this base URL

========================
4. API CONNECTION (VERY IMPORTANT)
========================

Create file: src/api.js

--------------------------------
api.js
--------------------------------
import axios from "axios";

const API = axios.create({
  baseURL: import.meta.env.VITE_API_URL
});

export const getTasks = () => API.get("/tasks");
export const createTask = (data) => API.post("/tasks", data);
export const deleteTask = (id) => API.delete(`/tasks/${id}`);

--------------------------------
HOW IT WORKS
--------------------------------
Base URL:
http://localhost:5000/api

Final endpoints:
GET    http://localhost:5000/api/tasks
POST   http://localhost:5000/api/tasks
DELETE http://localhost:5000/api/tasks/:id

========================
5. RUN FRONTEND
========================
npm run dev

Frontend runs on:
http://localhost:5173

========================
6. GIT COMMANDS
========================
git init
git add .
git commit -m "Initial commit"

git remote add origin https://github.com/your-username/mern-task-manager.git
git branch -M main
git push -u origin main

After updates:
git add .
git commit -m "update"
git push

========================
7. BUILD FRONTEND
========================
npm run build

========================
8. DEPLOY BACKEND ON RENDER
========================
1. Go to render.com
2. Click "New Web Service"
3. Connect GitHub repo
4. IMPORTANT: Set Root Directory = backend
5. Set:
   Build Command: npm install
   Start Command: node server.js
6. Add Environment Variable:
   MONGO_URI=your_mongodb_connection
7. Click Deploy

After deploy:
Backend URL example:
https://your-backend.onrender.com

API becomes:
https://your-backend.onrender.com/api/tasks

========================
9. DEPLOY BACKEND ON RAILWAY
========================
1. Go to railway.app
2. Click "New Project"
3. Deploy from GitHub
4. Select repo
5. Set root folder = backend
6. Add env:
   MONGO_URI=your_mongodb_connection
7. Auto deploy

Backend URL example:
https://your-backend.up.railway.app

========================
10. CONNECT FRONTEND TO DEPLOYED BACKEND
========================

Update frontend/.env

OLD:
VITE_API_URL=http://localhost:5000/api

NEW:
VITE_API_URL=https://your-backend-url/api

Example:
VITE_API_URL=https://your-backend.onrender.com/api

IMPORTANT:
Always restart frontend after changing .env

========================
11. DEPLOY FRONTEND (RENDER / NETLIFY / VERCEL)
========================
Build command:
npm run build

Publish directory:
dist

Environment variable:
VITE_API_URL=https://your-backend-url/api

========================
12. FINAL FLOW (EXAM SUMMARY)
========================
1. Start backend
2. Start frontend
3. Connect API via api.js
4. Test CRUD
5. Push to GitHub
6. Deploy backend
7. Update frontend API URL
8. Deploy frontend

========================
END
