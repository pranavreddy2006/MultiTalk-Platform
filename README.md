# MultiTalk - AI Video Generation Platform

🚀 **A comprehensive full-stack application that combines React frontend with Python AI backend for advanced video generation and user authentication.**

## 📋 Table of Contents

- [Overview](#overview)
- [Architecture](#architecture)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Prerequisites](#prerequisites)
- [Installation & Setup](#installation--setup)
- [Running the Application](#running-the-application)
- [API Endpoints](#api-endpoints)
- [Environment Variables](#environment-variables)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)

## 🎯 Overview

MultiTalk is an AI-powered video generation platform that allows users to create and manipulate videos using advanced machine learning models. The application features user authentication, a modern React frontend, and a powerful Python backend with AI capabilities.

## 🏗️ Architecture

### System Architecture Diagram

```
┌─────────────────────────────────────────────────────────────────┐
│                        MULTITALK PLATFORM                      │
│                     AI Video Generation System                 │
└─────────────────────────────────────────────────────────────────┘

┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│                 │    │                 │    │                 │
│   USER LAYER    │    │  FRONTEND LAYER │    │  BACKEND LAYER  │
│                 │    │                 │    │                 │
├─────────────────┤    ├─────────────────┤    ├─────────────────┤
│                 │    │                 │    │                 │
│  👤 Web Browser │────│  React App      │────│  Authentication │
│  📱 Mobile      │    │  Port: 5001     │    │  Server (Node)  │
│  💻 Desktop     │    │                 │    │  Port: 5002     │
│                 │    │  ┌─────────────┐│    │                 │
│                 │    │  │   ROUTES    ││    │  ┌─────────────┐│
│                 │    │  │             ││    │  │   ROUTES    ││
│                 │    │  │ /login      ││    │  │             ││
│                 │    │  │ /signup     ││◄───┤  │ POST /login ││
│                 │    │  │ /dashboard  ││    │  │ POST /signup││
│                 │    │  │ /create     ││    │  │             ││
│                 │    │  └─────────────┘│    │  └─────────────┘│
│                 │    │                 │    │                 │
└─────────────────┘    └─────────────────┘    └─────────────────┘
                                │                       │
                                │                       │
                                ▼                       ▼
                       ┌─────────────────┐    ┌─────────────────┐
                       │                 │    │                 │
                       │  UI COMPONENTS  │    │  AI PROCESSING  │
                       │                 │    │                 │
                       ├─────────────────┤    ├─────────────────┤
                       │                 │    │                 │
                       │ • Login/Signup  │    │  Python Backend │
                       │ • Dashboard     │    │                 │
                       │ • Video Studio  │    │  ┌─────────────┐│
                       │ • AI Assistant  │    │  │   WAN AI    ││
                       │ • Video Player  │    │  │   Models    ││
                       │                 │    │  │             ││
                       │                 │    │  │ • Video Gen ││
                       │                 │    │  │ • Processing││
                       │                 │    │  │ • Analysis  ││
                       │                 │    │  └─────────────┘│
                       │                 │    │                 │
                       └─────────────────┘    └─────────────────┘
                                                       │
                                                       │
                                                       ▼
                              ┌─────────────────────────────────────┐
                              │           DATABASE LAYER            │
                              │                                     │
                              ├─────────────────────────────────────┤
                              │                                     │
                              │         MongoDB Database            │
                              │         Port: 27017                 │
                              │                                     │
                              │  ┌─────────────┐  ┌─────────────┐  │
                              │  │    USERS    │  │   VIDEOS    │  │
                              │  │             │  │             │  │
                              │  │ • _id       │  │ • _id       │  │
                              │  │ • name      │  │ • title     │  │
                              │  │ • email     │  │ • url       │  │
                              │  │ • password  │  │ • metadata  │  │
                              │  │ • token     │  │ • user_id   │  │
                              │  └─────────────┘  └─────────────┘  │
                              │                                     │
                              └─────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│                        DATA FLOW                               │
└─────────────────────────────────────────────────────────────────┘

1. 👤 User → 🌐 React Frontend (Login/Signup)
2. 🌐 Frontend → 🔧 Node.js Auth Server (JWT Verification)
3. 🔧 Auth Server → 🗄️ MongoDB (User Validation)
4. 👤 User → 🌐 React Frontend (Video Generation Request)
5. 🌐 Frontend → 🤖 Python AI Backend (Processing)
6. 🤖 AI Backend → 🧠 WAN Models (Video Generation)
7. 🧠 Models → 🤖 AI Backend (Generated Video)
8. 🤖 AI Backend → 🌐 Frontend (Video Response)
9. 🌐 Frontend → 👤 User (Display Result)
```

### Component Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                     FRONTEND COMPONENTS                        │
└─────────────────────────────────────────────────────────────────┘

App.js
├── Navbar.js
├── LandingPage.js
├── Login.js (Auth System)
├── Dashboard.js
│   ├── AICreationStudio.js
│   ├── AIVideoStudio.js
│   ├── CreationMode.js
│   ├── VideoDetails.js
│   └── GeminiAssistant.js
└── [Protected Routes]

┌─────────────────────────────────────────────────────────────────┐
│                     BACKEND ARCHITECTURE                       │
└─────────────────────────────────────────────────────────────────┘

Authentication Server (Node.js)
├── server.js (Main Express Server)
├── User Schema (MongoDB)
├── JWT Middleware
├── bcrypt Password Hashing
└── CORS Configuration

AI Processing Backend (Python)
├── app.py (Main Flask Application)
├── server.py (Alternative Server)
├── wan/ (WAN AI Models)
│   ├── modules/ (Neural Network Components)
│   ├── configs/ (Model Configurations)
│   ├── utils/ (Utility Functions)
│   └── multitalk.py (Core AI Logic)
├── kokoro/ (Audio Processing)
└── src/ (Additional Processing Modules)
```

### Technology Stack Integration

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│    FRONTEND     │    │    BACKEND      │    │    DATABASE    │
│                 │    │                 │    │                 │
│ React 19.2.0    │────│ Node.js +       │────│ MongoDB 4.4+    │
│ React Router    │    │ Express 5.1.0   │    │                 │
│ Axios 1.13.1    │    │                 │    │ Collections:    │
│ CSS3 + Glass    │    │ Python 3.8+     │    │ • users         │
│ Morphism        │    │ Flask           │    │ • videos        │
│                 │    │                 │    │ • sessions      │
│                 │    │ AI Libraries:   │    │                 │
│                 │    │ • PyTorch 2.8   │    │ Features:       │
│                 │    │ • Transformers  │    │ • Authentication│
│                 │    │ • Diffusers     │    │ • User Profiles │
│                 │    │ • OpenCV        │    │ • Video Storage │
│                 │    │ • Gradio        │    │ • Metadata      │
│                 │    │                 │    │                 │
└─────────────────┘    └─────────────────┘    └─────────────────┘
```

## ✨ Features

### Frontend (React)
- 🔐 **User Authentication** - Secure signup/login system
- 🎨 **Modern UI/UX** - Responsive design with glass morphism effects
- 🔄 **Real-time Communication** - Seamless API integration
- 📱 **Mobile Responsive** - Works on all device sizes

### Backend (Python + Node.js)
- 🤖 **AI Video Generation** - Advanced video processing using WAN models
- 👤 **User Management** - JWT-based authentication
- 🗄️ **Database Integration** - MongoDB for user data storage
- 🔧 **API Services** - RESTful API endpoints

## 🛠️ Tech Stack

### Frontend
- **React** 19.2.0
- **React Router DOM** 7.9.4
- **Axios** 1.13.1
- **CSS3** with modern styling

### Backend
- **Node.js** with Express.js 5.1.0
- **Python** with Flask
- **MongoDB** with Mongoose 8.19.2
- **JWT** for authentication
- **bcryptjs** for password hashing

### AI/ML
- **PyTorch** 2.8.0
- **Transformers** 4.57.1
- **Diffusers** 0.35.2
- **OpenCV** 4.12.0
- **Gradio** 5.49.1

## 📁 Project Structure

```
MultitalkFinal1/
├── MultiTalk/                    # Frontend (React Application)
│   ├── src/
│   │   ├── components/
│   │   │   ├── Login.js         # Authentication component
│   │   │   └── Login.css        # Authentication styles
│   │   ├── App.js               # Main React component
│   │   └── index.js             # React entry point
│   ├── public/                  # Static assets
│   ├── package.json             # Frontend dependencies
│   ├── server.js                # Authentication server (Node.js)
│   └── .env                     # Environment variables
│
├── Multi-Talk/                   # Backend (Python AI Application)
│   ├── src/                     # Source code
│   ├── wan/                     # WAN model implementation
│   ├── kokoro/                  # Kokoro model files
│   ├── weights/                 # Model weights
│   ├── app.py                   # Main Python application
│   ├── server.py                # Flask server
│   ├── requirements.txt         # Python dependencies
│   └── generate_multitalk.py    # Video generation script
│
└── README.md                    # This file
```

## 📋 Prerequisites

Before setting up the project, ensure you have the following installed:

- **Node.js** (v16 or higher)
- **Python** (v3.8 or higher)
- **MongoDB** (v4.4 or higher)
- **Git**
- **npm** or **yarn**

## 🚀 Installation & Setup

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/MultitalkFinal1.git
cd MultitalkFinal1
```

### 2. Frontend Setup (React)

```bash
cd MultiTalk
npm install
```

### 3. Backend Setup (Python)

```bash
cd ../Multi-Talk
pip install -r requirements.txt
```

### 4. Database Setup

Create MongoDB data directory:
```bash
mkdir C:\data\db
```

### 5. Environment Configuration

Create `.env` file in the `MultiTalk` directory:

```env
MONGO_URI=mongodb://localhost:27017/multitalk
JWT_SECRET=your_jwt_secret_key_here_please_change_in_production
PORT=5002
```

## 🏃‍♂️ Running the Application

Follow these steps in order to start all services:

### 1. Start MongoDB
```bash
mongod --dbpath "C:\data\db"
```

### 2. Start Authentication Server (Terminal 1)
```bash
cd MultiTalk
node server.js
```
✅ **Authentication API**: http://localhost:5002

### 3. Start React Frontend (Terminal 2)
```bash
cd MultiTalk
npm start
```
✅ **Frontend**: http://localhost:5001

### 4. Start Python AI Backend (Terminal 3)
```bash
cd Multi-Talk
python app.py
```
✅ **AI Backend**: Available for video processing

## 🔌 API Endpoints

### Authentication API (Port 5002)

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/signup` | User registration |
| POST | `/login` | User authentication |

#### Signup Request
```json
{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "securepassword123"
}
```

#### Login Request
```json
{
  "email": "john@example.com",
  "password": "securepassword123"
}
```

## 🔧 Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `MONGO_URI` | MongoDB connection string | `mongodb://localhost:27017/multitalk` |
| `JWT_SECRET` | Secret key for JWT tokens | Required |
| `PORT` | Authentication server port | `5002` |

## 🚨 Troubleshooting

### Common Issues

1. **"Server connection error" during signup**
   - Ensure MongoDB is running
   - Check if authentication server is running on port 5002
   - Verify .env file configuration

2. **CUDA/GPU errors in Python backend**
   - The app automatically disables CUDA for CPU-only operation
   - Ensure all Python dependencies are installed

3. **Port conflicts**
   - Frontend: 5001
   - Authentication API: 5002
   - MongoDB: 27017

4. **Module import errors**
   - Run `npm install` in MultiTalk directory
   - Run `pip install -r requirements.txt` in Multi-Talk directory

### Reset Instructions

If you encounter issues, restart all services:

```bash
# Stop all running processes (Ctrl+C in each terminal)

# Restart MongoDB
mongod --dbpath "C:\data\db"

# Restart Authentication Server
cd MultiTalk && node server.js

# Restart Frontend
cd MultiTalk && npm start
```

## 🎯 Usage

1. **Access the application**: http://localhost:5001
2. **Create an account**: Click register and fill in your details
3. **Login**: Use your credentials to access the dashboard
4. **Generate videos**: Use the AI-powered video generation features

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- **Alibaba WAN Team** - For the core AI models
- **React Team** - For the amazing frontend framework
- **MongoDB** - For the reliable database solution

---

**⭐ If you find this project helpful, please give it a star!**

## 📞 Support

If you have any questions or need help, please:
- Create an issue in this repository
- Contact the maintainers

---

**Built with ❤️ using React, Python, and MongoDB**