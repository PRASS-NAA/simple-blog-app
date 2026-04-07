# Simple Blog App

A full-stack web application built for educational purposes, demonstrating CRUD operations with modern web technologies.

## 🚀 Tech Stack

- **Frontend**: React.js, CSS3
- **Backend**: Node.js, Express.js
- **Database**: MySQL
- **Architecture**: RESTful API

## ✨ Features

- ✅ Create, read, update, and delete blog posts
- 📱 Responsive design for all devices
- 🎨 Clean, intuitive user interface
- 👤 Author attribution and timestamps
- 📝 Simple text editor for content creation
- 🔍 Post excerpts on home page

## 🛠️ Installation

### Prerequisites
- Node.js (v14 or higher)
- MySQL Server
- npm or yarn

### Setup

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd simple-blog-app
   ```

2. **Database Setup**
   ```sql
   CREATE DATABASE blog_db;
   USE blog_db;
   
   CREATE TABLE posts (
     id INT AUTO_INCREMENT PRIMARY KEY,
     title VARCHAR(255) NOT NULL,
     content TEXT NOT NULL,
     author VARCHAR(100) NOT NULL,
     created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
   );
   ```

3. **Install Dependencies**
   ```bash
   # Install backend dependencies
   cd backend
   npm install
   
   # Install frontend dependencies
   cd ../frontend
   npm install
   ```

4. **Start Development Servers**
   
   **Terminal 1 - Backend Server:**
   ```bash
   cd backend
   node server.js
   ```
   Backend runs on: http://localhost:5003
   
   **Terminal 2 - Frontend Server:**
   ```bash
   cd frontend
   npm start
   ```
   Frontend runs on: http://localhost:3000

## 📁 Project Structure

```
simple-blog-app/
├── backend/
│   ├── server.js          # Express server
│   ├── database.sql       # Database schema
│   └── package.json
├── frontend/
│   ├── src/
│   │   ├── App.js         # Main React component
│   │   ├── App.css        # Styling
│   │   └── index.js       # Entry point
│   └── package.json
└── README.md
```

## 🔌 API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/posts` | Get all posts |
| GET | `/api/posts/:id` | Get single post |
| POST | `/api/posts` | Create new post |
| PUT | `/api/posts/:id` | Update post |
| DELETE | `/api/posts/:id` | Delete post |

## 🎯 Learning Objectives

This project helps students understand:
- Full-stack development workflow
- RESTful API design principles
- Database integration with MySQL
- React component architecture
- CRUD operations implementation
- Frontend-backend communication

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request


## 👨‍💻 Author

Created by www.virustechsolutions.com for educational purposes to demonstrate modern web development practices.
