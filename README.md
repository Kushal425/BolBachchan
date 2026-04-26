# 💬 BolBachchan — Real-Time Chat Application

A full-stack real-time messaging application where users can chat with each other instantly, see who's online, and share images — all with a clean, theme-customizable UI.

---

## 🚀 Features

- **Real-time messaging** powered by WebSockets (Socket.io) — messages are delivered instantly without page refresh
- **Online presence indicator** — see which users are currently active
- **JWT-based Authentication** — secure signup, login, and session management via HTTP-only cookies
- **Image sharing** — users can send images in chat, uploaded and hosted on Cloudinary
- **Profile management** — update your display name and profile picture
- **32 UI themes** — switch between light, dark, and many other themes via DaisyUI
- **Protected routes** — unauthenticated users are redirected to the login page automatically
- **Global state management** — lightweight client state handled with Zustand
- **Full error handling** — meaningful error messages on both client and server

---

## 🛠️ Tech Stack

| Layer      | Technology                                      |
|------------|-------------------------------------------------|
| Frontend   | React.js, Vite, TailwindCSS, DaisyUI, Zustand   |
| Backend    | Node.js, Express.js                             |
| Database   | MongoDB (Mongoose ODM)                          |
| Real-time  | Socket.io                                       |
| Auth       | JSON Web Tokens (JWT), bcryptjs                 |
| Media      | Cloudinary                                      |

---

## 📁 Project Structure

```
BolBachchan/
├── backend/
│   └── src/
│       ├── controllers/     # Route handler logic
│       ├── lib/             # DB, Cloudinary, Socket, JWT utilities
│       ├── middleware/      # Auth middleware (protectRoute)
│       ├── models/          # Mongoose schemas (User, Message)
│       ├── routes/          # API route definitions
│       ├── seeds/           # Database seeding scripts
│       └── index.js         # App entry point
└── frontend/
    └── src/
        ├── components/      # Reusable UI components
        ├── pages/           # Route-level page components
        ├── store/           # Zustand state stores
        ├── lib/             # Axios instance, helpers
        └── constants/       # App-wide constants
```

---

## ⚙️ Setup & Installation

### 1. Clone the repository

```bash
git clone https://github.com/your-username/bolbachchan.git
cd bolbachchan
```

### 2. Configure environment variables

> **Important:** The `.env` file must be created inside the `backend/` folder — **not** in the root of the project.

Create the file at `backend/.env` with the following content:

```env
MONGODB_URI=your_mongodb_connection_string
PORT=5001
JWT_SECRET=your_secret_key_here

CLOUDINARY_CLOUD_NAME=your_cloudinary_cloud_name
CLOUDINARY_API_KEY=your_cloudinary_api_key
CLOUDINARY_API_SECRET=your_cloudinary_api_secret

NODE_ENV=development
```

---

## 🖥️ Running Locally (Development)

Open **two separate terminals** — one for the backend and one for the frontend.

### Terminal 1 — Backend

```bash
cd backend
npm install
npm run dev
```

The backend server will start at **http://localhost:5001**

### Terminal 2 — Frontend

```bash
cd frontend
npm install
npm run dev
```

The frontend will start at **http://localhost:5173**

> Make sure the backend is running before opening the frontend.

---

## 🏗️ Production Build

To build and run everything from a single server:

```bash
# From the project root
npm run build   # installs deps and builds the frontend
npm start       # starts the backend which serves the built frontend
```

App will be available at **http://localhost:5001**

---

## 🔌 API Endpoints

### Auth Routes — `/api/auth`
| Method | Endpoint          | Description                |
|--------|-------------------|----------------------------|
| POST   | `/signup`         | Register a new user        |
| POST   | `/login`          | Login with credentials     |
| POST   | `/logout`         | Logout and clear session   |
| PUT    | `/update-profile` | Update profile picture     |
| GET    | `/check`          | Verify current auth status |

### Message Routes — `/api/messages`
| Method | Endpoint       | Description                          |
|--------|----------------|--------------------------------------|
| GET    | `/users`       | Get all users (for sidebar)          |
| GET    | `/:id`         | Get message history with a user      |
| POST   | `/send/:id`    | Send a message to a user             |

---

## 🗄️ Database Collections

### `users`
| Field        | Type     | Notes                        |
|--------------|----------|------------------------------|
| `email`      | String   | Unique, required             |
| `fullName`   | String   | Required                     |
| `password`   | String   | Hashed with bcryptjs         |
| `profilePic` | String   | Cloudinary URL               |
| `timestamps` | Auto     | `createdAt`, `updatedAt`     |

### `messages`
| Field        | Type     | Notes                        |
|--------------|----------|------------------------------|
| `senderId`   | ObjectId | Reference to User            |
| `receiverId` | ObjectId | Reference to User            |
| `text`       | String   | Message text content         |
| `image`      | String   | Cloudinary URL (optional)    |
| `timestamps` | Auto     | `createdAt`, `updatedAt`     |

---

## 🔒 Security Highlights

- Passwords are hashed using **bcryptjs** before storage
- JWTs are stored in **HTTP-only cookies** to prevent XSS attacks
- Cookie `sameSite: strict` to mitigate CSRF attacks
- Secure cookie flag enabled automatically in production

---

## 👤 Author

**Kushal Sarkar**
