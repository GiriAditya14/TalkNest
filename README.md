# Converse - Real-Time Chat Application

<div align="center">

![MERN Stack](https://img.shields.io/badge/Stack-MERN-green?style=for-the-badge)
![Socket.io](https://img.shields.io/badge/Socket.io-Real--time-blue?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge)

**A modern, full-stack real-time chat application built with the MERN stack, featuring instant messaging, online status tracking, and a beautiful responsive UI.**

[Features](#features) • [Tech Stack](#tech-stack) • [Architecture](#architecture) • [Installation](#installation) • [API Documentation](#api-documentation)

</div>

---

## 📋 Table of Contents

- [Overview](#overview)
- [Key Features](#key-features)
- [Technology Stack](#technology-stack)
- [System Architecture](#system-architecture)
- [Project Structure](#project-structure)
- [Installation & Setup](#installation--setup)
- [Environment Variables](#environment-variables)
- [API Documentation](#api-documentation)
- [Frontend Implementation](#frontend-implementation)
- [Backend Implementation](#backend-implementation)
- [Database Schema](#database-schema)
- [Security Features](#security-features)
- [Real-time Communication](#real-time-communication)
- [State Management](#state-management)
- [Deployment](#deployment)
- [Interview Questions & Answers](#interview-questions--answers)
- [Challenges & Solutions](#challenges--solutions)

---

## 🎯 Overview

**Converse** is a production-ready, full-stack real-time chat application that demonstrates modern web development practices. Built with the MERN stack (MongoDB, Express, React, Node.js) and Socket.io for real-time bidirectional communication, this application showcases end-to-end implementation of authentication, real-time messaging, file uploads, and responsive UI design.

### Problem Statement
Traditional communication requires users to constantly refresh pages to see new messages. Converse solves this by implementing WebSocket-based real-time communication, providing instant message delivery, online/offline status tracking, and a seamless user experience.

### Target Users
- Individuals seeking instant communication
- Teams requiring real-time collaboration
- Organizations needing secure internal messaging
- Developers learning full-stack development

### Why MERN Stack?

- **MongoDB**: Flexible NoSQL database perfect for storing chat messages and user data
- **Express.js**: Lightweight backend framework for building RESTful APIs
- **React**: Component-based UI library for building interactive interfaces
- **Node.js**: JavaScript runtime enabling full-stack JavaScript development
- **Socket.io**: Enables real-time, bidirectional event-based communication

---

## ✨ Key Features

### 🔐 Authentication & Authorization
- **JWT-based authentication** with HTTP-only cookies
- Secure password hashing using **bcrypt** (10 salt rounds)
- Protected routes with middleware verification
- Persistent login sessions (7-day token expiration)
- Auto-login on page refresh with token validation
- Secure logout with cookie clearing and socket disconnection

### 💬 Real-Time Messaging
- **Instant message delivery** using Socket.io WebSockets
- Send text messages and images
- Message history persistence in MongoDB
- Auto-scroll to latest messages
- Message timestamps with formatted display
- Real-time message status (sent/delivered)

### 👥 User Management
- User registration with validation
- Profile picture upload to **Cloudinary CDN**
- Update profile information
- View all registered users
- Filter online/offline users

### 🌐 Online Status Tracking
- Real-time online/offline status indicators
- User presence detection using Socket.io
- Online user count display
- Visual indicators (green dot for online users)
- Socket connection management on login/logout

### 🎨 Modern UI/UX
- **Responsive design** - Mobile, tablet, and desktop optimized
- **27 theme options** using DaisyUI
- Dark/light mode support
- Loading states and skeletons
- Toast notifications for user feedback
- Smooth animations and transitions
- Icon integration with Lucide React

### 📁 File Handling
- Image upload in messages
- Profile picture management
- Base64 encoding for image transfer
- Cloudinary integration for CDN storage
- Image preview before sending
- File type validation

---

## 🛠 Technology Stack

### Frontend
| Technology | Version | Purpose |
|-----------|---------|---------|
| **React** | 18.3.1 | UI library for building component-based interfaces |
| **Vite** | 5.4.10 | Fast build tool and dev server |
| **Zustand** | 5.0.1 | Lightweight state management |
| **React Router DOM** | 6.28.0 | Client-side routing |
| **Axios** | 1.7.7 | HTTP client with interceptors |
| **Socket.io Client** | 4.8.1 | WebSocket client for real-time communication |
| **Tailwind CSS** | 3.4.15 | Utility-first CSS framework |
| **DaisyUI** | 4.12.14 | Tailwind CSS component library |
| **Lucide React** | 0.459.0 | Modern icon library |
| **React Hot Toast** | 2.4.1 | Toast notifications |

### Backend
| Technology | Version | Purpose |
|-----------|---------|---------|
| **Node.js** | Latest | JavaScript runtime environment |
| **Express** | 4.21.1 | Web application framework |
| **MongoDB** | 8.8.1 | NoSQL database |
| **Mongoose** | 8.8.1 | MongoDB ODM for schema modeling |
| **Socket.io** | 4.8.1 | Real-time WebSocket server |
| **JWT** | 9.0.2 | Token-based authentication |
| **bcryptjs** | 2.4.3 | Password hashing |
| **Cloudinary** | 2.5.1 | Cloud-based image storage |
| **CORS** | 2.8.5 | Cross-Origin Resource Sharing |
| **dotenv** | 16.4.5 | Environment variable management |
| **Cookie Parser** | 1.4.7 | Parse HTTP cookies |

### Development Tools
- **Nodemon**: Auto-restart server on changes
- **ESLint**: Code linting and formatting
- **PostCSS**: CSS processing
- **Autoprefixer**: CSS vendor prefixing

---

## 🏗 System Architecture

### High-Level Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                    CLIENT TIER (React)                      │
│  ┌────────────┐  ┌────────────┐  ┌───────────────────────┐  │
│  │   Pages    │  │ Components │  │  State Management     │  │
│  │  - Login   │  │  - Navbar  │  │  - useAuthStore       │  │
│  │  - Signup  │  │  - Sidebar │  │  - useChatStore       │  │
│  │  - Home    │  │  - Chat    │  │  - useThemeStore      │  │
│  │  - Profile │  │  - Message │  │                       │  │
│  └────────────┘  └────────────┘  └───────────────────────┘  │
│                         ↕ HTTP/WebSocket                    │
└─────────────────────────────────────────────────────────────┘
                            ↕
┌─────────────────────────────────────────────────────────────┐
│                 SERVER TIER (Node.js/Express)               │
│  ┌─────────────┐  ┌──────────────┐  ┌──────────────────┐    │
│  │   Routes    │  │ Controllers  │  │   Middleware     │    │
│  │  - Auth     │→ │  - Auth      │  │  - protectRoute  │    │
│  │  - Messages │→ │  - Messages  │  │  - CORS          │    │
│  └─────────────┘  └──────────────┘  │  - Body Parser   │    │
│                                     └──────────────────┘    │
│  ┌────────────────────────────────────────────────────┐     │
│  │         Socket.io Server (WebSocket)               │     │
│  │  - Connection management                           │     │
│  │  - Online status tracking                          │     │
│  │  - Real-time message broadcasting                  │     │
│  └────────────────────────────────────────────────────┘     │
└─────────────────────────────────────────────────────────────┘
                            ↕
┌────────────────────────────────────────────────────────────┐
│                      DATA TIER                             │
│  ┌──────────────────┐          ┌─────────────────────────┐ │
│  │   MongoDB        │          │   Cloudinary CDN        │ │
│  │  - Users         │          │  - Profile pictures     │ │
│  │  - Messages      │          │  - Message images       │ │
│  └──────────────────┘          └─────────────────────────┘ │
└────────────────────────────────────────────────────────────┘
```

### Request Flow Diagram

**Authentication Flow:**
```
User → Login Form → POST /api/auth/login → Verify Credentials → 
Hash Compare → Generate JWT → Set HTTP-Only Cookie → 
Return User Data → Update Store → Connect Socket.io → Redirect Home
```

**Message Flow:**
```
User A → Type Message → POST /api/messages/send/:id → 
Save to MongoDB → Get Receiver Socket ID → 
Emit "newMessage" event → User B receives via Socket.io → 
Update UI in real-time
```

---

## 📁 Project Structure

```
Converse/
├── backend/
│   ├── src/
│   │   ├── controllers/
│   │   │   ├── auth.controller.js       # Authentication logic
│   │   │   └── message.controller.js    # Message operations
│   │   ├── lib/
│   │   │   ├── cloudinary.js            # Cloudinary config
│   │   │   ├── db.js                    # MongoDB connection
│   │   │   ├── socket.js                # Socket.io setup
│   │   │   └── utils.js                 # JWT generation
│   │   ├── middleware/
│   │   │   └── auth.middleware.js       # JWT verification
│   │   ├── models/
│   │   │   ├── user.model.js            # User schema
│   │   │   └── message.model.js         # Message schema
│   │   ├── routes/
│   │   │   ├── auth.route.js            # Auth endpoints
│   │   │   └── message.route.js         # Message endpoints
│   │   └── index.js                     # Server entry point
│   └── package.json
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   │   ├── Navbar.jsx               # Navigation bar
│   │   │   ├── Sidebar.jsx              # User list
│   │   │   ├── ChatContainer.jsx        # Message display
│   │   │   ├── ChatHeader.jsx           # Chat header
│   │   │   ├── MessageInput.jsx         # Message input
│   │   │   ├── NoChatSelected.jsx       # Empty state
│   │   │   ├── AuthImagePattern.jsx     # Auth page design
│   │   │   └── skeletons/               # Loading states
│   │   ├── pages/
│   │   │   ├── HomePage.jsx             # Main chat page
│   │   │   ├── LoginPage.jsx            # Login page
│   │   │   ├── SignUpPage.jsx           # Registration page
│   │   │   ├── ProfilePage.jsx          # User profile
│   │   │   └── SettingsPage.jsx         # Theme settings
│   │   ├── store/
│   │   │   ├── useAuthStore.js          # Auth state
│   │   │   ├── useChatStore.js          # Chat state
│   │   │   └── useThemeStore.js         # Theme state
│   │   ├── lib/
│   │   │   ├── axios.js                 # Axios config
│   │   │   └── utils.js                 # Utility functions
│   │   ├── constants/
│   │   │   └── index.js                 # App constants
│   │   ├── App.jsx                      # Root component
│   │   ├── main.jsx                     # Entry point
│   │   └── index.css                    # Global styles
│   └── package.json
└── README.md
```

---

## 🚀 Installation & Setup

### Prerequisites
- **Node.js** (v18 or higher)
- **MongoDB** (Local installation or MongoDB Atlas account)
- **Cloudinary** account (for image uploads)
- **Git**

### Step 1: Clone the Repository
```bash
git clone https://github.com/yourusername/Converse.git
cd Converse
```

### Step 2: Backend Setup
```bash
cd backend
npm install
```

Create `.env` file in backend directory:
```env
MONGODB_URI=mongodb://localhost:27017/Converse
# OR for MongoDB Atlas:
# MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/Converse

PORT=5001
JWT_SECRET=your_super_secret_jwt_key_minimum_32_characters
NODE_ENV=development

# Cloudinary Configuration
CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret
```

### Step 3: Frontend Setup
```bash
cd ../frontend
npm install
```

### Step 4: Run Development Servers

**Terminal 1 - Backend:**
```bash
cd backend
npm run dev
```
Server runs on: `http://localhost:5001`

**Terminal 2 - Frontend:**
```bash
cd frontend
npm run dev
```
Client runs on: `http://localhost:5173`

### Step 5: Build for Production
```bash
# Build frontend
cd frontend
npm run build

# Start production server (serves both frontend and backend)
cd ../backend
npm start
```

---

## 🔐 Environment Variables

### Backend (.env)

| Variable | Description | Example |
|----------|-------------|---------|
| `MONGODB_URI` | MongoDB connection string | `mongodb://localhost:27017/Converse` |
| `PORT` | Server port number | `5001` |
| `JWT_SECRET` | Secret key for JWT signing | `your_secret_key_here` |
| `NODE_ENV` | Environment mode | `development` or `production` |
| `CLOUDINARY_CLOUD_NAME` | Cloudinary cloud name | `your_cloud_name` |
| `CLOUDINARY_API_KEY` | Cloudinary API key | `123456789012345` |
| `CLOUDINARY_API_SECRET` | Cloudinary API secret | `your_api_secret` |

### Getting Cloudinary Credentials
1. Sign up at [Cloudinary](https://cloudinary.com/)
2. Go to Dashboard
3. Copy Cloud Name, API Key, and API Secret

### Getting MongoDB URI
**Local MongoDB:**
```
mongodb://localhost:27017/Converse
```

**MongoDB Atlas:**
1. Create account at [MongoDB Atlas](https://www.mongodb.com/cloud/atlas)
2. Create a cluster
3. Get connection string
4. Replace `<password>` and `<dbname>`

---

## 📡 API Documentation

### Base URL
```
http://localhost:5001/api
```

### Authentication Endpoints

#### 1. Sign Up
```http
POST /auth/signup
Content-Type: application/json

{
  "fullName": "John Doe",
  "email": "john@example.com",
  "password": "password123"
}

Response (201):
{
  "_id": "user_id",
  "fullName": "John Doe",
  "email": "john@example.com",
  "profilePic": ""
}
```

**Validation:**
- All fields required
- Password minimum 6 characters
- Email must be unique
- Valid email format

#### 2. Login
```http
POST /auth/login
Content-Type: application/json

{
  "email": "john@example.com",
  "password": "password123"
}

Response (200):
{
  "_id": "user_id",
  "fullName": "John Doe",
  "email": "john@example.com",
  "profilePic": "cloudinary_url"
}
```

**Process:**
1. Find user by email
2. Compare password with bcrypt
3. Generate JWT token
4. Set HTTP-only cookie
5. Return user data

#### 3. Logout
```http
POST /auth/logout

Response (200):
{
  "message": "Logged out successfully"
}
```

**Process:**
- Clears JWT cookie
- Client disconnects socket

#### 4. Check Authentication
```http
GET /auth/check
Authorization: Cookie (jwt token)

Response (200):
{
  "_id": "user_id",
  "fullName": "John Doe",
  "email": "john@example.com",
  "profilePic": "cloudinary_url"
}
```

**Protected Route** - Requires valid JWT

#### 5. Update Profile
```http
PUT /auth/update-profile
Authorization: Cookie (jwt token)
Content-Type: application/json

{
  "profilePic": "base64_encoded_image"
}

Response (200):
{
  "_id": "user_id",
  "fullName": "John Doe",
  "email": "john@example.com",
  "profilePic": "new_cloudinary_url"
}
```

**Protected Route** - Uploads to Cloudinary

### Message Endpoints

#### 1. Get All Users (for Sidebar)
```http
GET /messages/users
Authorization: Cookie (jwt token)

Response (200):
[
  {
    "_id": "user_id",
    "fullName": "Jane Doe",
    "email": "jane@example.com",
    "profilePic": "cloudinary_url"
  }
]
```

**Note:** Excludes current user from results

#### 2. Get Messages with User
```http
GET /messages/:userId
Authorization: Cookie (jwt token)

Response (200):
[
  {
    "_id": "message_id",
    "senderId": "user1_id",
    "receiverId": "user2_id",
    "text": "Hello!",
    "image": "cloudinary_url",
    "createdAt": "2026-01-29T10:30:00.000Z"
  }
]
```

**Returns:** All messages between current user and specified user

#### 3. Send Message
```http
POST /messages/send/:receiverId
Authorization: Cookie (jwt token)
Content-Type: application/json

{
  "text": "Hello, how are you?",
  "image": "base64_encoded_image"  // optional
}

Response (201):
{
  "_id": "message_id",
  "senderId": "current_user_id",
  "receiverId": "receiver_id",
  "text": "Hello, how are you?",
  "image": "cloudinary_url",
  "createdAt": "2026-01-29T10:30:00.000Z"
}
```

**Process:**
1. Upload image to Cloudinary (if provided)
2. Save message to MongoDB
3. Get receiver's socket ID
4. Emit real-time event if receiver online
5. Return saved message

---

## ⚛️ Frontend Implementation

### Component Architecture

#### 1. **App.jsx** - Root Component
```jsx
- Routes configuration (/, /login, /signup, /profile, /settings)
- Protected route logic
- Authentication check on mount
- Theme provider
- Toast notifications
```

**Key Features:**
- Auto-login on page load
- Route protection based on auth state
- Loading state during auth check
- Theme persistence

#### 2. **Pages**

**LoginPage.jsx**
- Email/password form with validation
- Show/hide password toggle
- Loading state during login
- Redirect to home after success
- Link to signup page

**SignUpPage.jsx**
- Full name, email, password fields
- Client-side validation
- Password requirements (min 6 chars)
- Email format validation
- Decorative auth pattern

**HomePage.jsx**
- Main chat interface
- Sidebar with user list
- Chat container (conditional render)
- Empty state when no chat selected

**ProfilePage.jsx**
- Display user information
- Profile picture upload
- Image preview
- Account creation date
- Non-editable email/name fields

**SettingsPage.jsx**
- 27 theme options
- Live theme preview
- Mock chat interface
- Theme persistence in localStorage

#### 3. **Components**

**Navbar.jsx**
```jsx
Features:
- App branding
- Settings link
- Profile link
- Logout button
- Theme switcher
- Responsive design
```

**Sidebar.jsx**
```jsx
Features:
- Display all users
- Online/offline indicators
- Filter online users (checkbox)
- User selection
- Active chat highlighting
- Profile picture display
- Loading skeleton
```

**ChatContainer.jsx**
```jsx
Features:
- Message history display
- Auto-scroll to bottom
- Message bubbles (sent/received)
- Timestamp formatting
- Image message support
- Loading skeleton
```

**MessageInput.jsx**
```jsx
Features:
- Text input field
- Image upload button
- Image preview with remove option
- Send button
- File type validation
- Form submission handling
```

**ChatHeader.jsx**
- Selected user info
- Online status display
- Profile picture

**NoChatSelected.jsx**
- Empty state message
- Decorative illustration
- Call-to-action text

### State Management (Zustand)

#### useAuthStore.js
```javascript
State:
- authUser: Current user object
- isSigningUp: Loading state
- isLoggingIn: Loading state
- isUpdatingProfile: Loading state
- isCheckingAuth: Auth check loading
- onlineUsers: Array of online user IDs
- socket: Socket.io connection

Actions:
- checkAuth(): Verify JWT on mount
- signup(data): Register new user
- login(data): Authenticate user
- logout(): Clear session
- updateProfile(data): Upload profile pic
- connectSocket(): Establish WebSocket
- disconnectSocket(): Close connection
```

#### useChatStore.js
```javascript
State:
- messages: Current conversation messages
- users: All users list
- selectedUser: Active chat user
- isUsersLoading: Loading state
- isMessagesLoading: Loading state

Actions:
- getUsers(): Fetch all users
- getMessages(userId): Load conversation
- sendMessage(data): Send new message
- setSelectedUser(user): Select chat
- subscribeToMessages(): Listen for new messages
- unsubscribeFromMessages(): Clean up listener
```

#### useThemeStore.js
```javascript
State:
- theme: Current theme name

Actions:
- setTheme(theme): Change and persist theme
```

### HTTP Client Configuration

**lib/axios.js**
```javascript
- Base URL configuration
- Credentials enabled (for cookies)
- Environment-aware URL
- Development: http://localhost:5001/api
- Production: /api
```

---

## 🔧 Backend Implementation

### Server Setup (index.js)

```javascript
1. Load environment variables (dotenv)
2. Configure middleware:
   - express.json() - Parse JSON bodies
   - cookie-parser - Parse cookies
   - CORS with credentials
3. Register routes:
   - /api/auth - Authentication
   - /api/messages - Messaging
4. Serve static files (production)
5. Start HTTP server with Socket.io
6. Connect to MongoDB
```

### Controllers

#### auth.controller.js

**signup(req, res)**
```javascript
Process:
1. Extract fullName, email, password
2. Validate all fields present
3. Check password length >= 6
4. Check email uniqueness
5. Hash password (bcrypt, salt: 10)
6. Create user in database
7. Generate JWT token
8. Set HTTP-only cookie
9. Return user data (exclude password)

Error Handling:
- 400: Missing fields
- 400: Password too short
- 400: Email exists
- 500: Server error
```

**login(req, res)**
```javascript
Process:
1. Extract email, password
2. Find user by email
3. Compare password with hash
4. Generate JWT token
5. Set HTTP-only cookie
6. Return user data

Error Handling:
- 400: Invalid credentials
- 500: Server error
```

**logout(req, res)**
```javascript
Process:
1. Clear JWT cookie (maxAge: 0)
2. Return success message
```

**updateProfile(req, res)**
```javascript
Process:
1. Get userId from req.user (middleware)
2. Extract profilePic (base64)
3. Upload to Cloudinary
4. Update user in database
5. Return updated user

Error Handling:
- 400: Missing profile pic
- 500: Upload/server error
```

**checkAuth(req, res)**
```javascript
Process:
1. Return req.user (set by middleware)

Note: Protected by auth middleware
```

#### message.controller.js

**getUsersForSidebar(req, res)**
```javascript
Process:
1. Get logged-in user ID
2. Find all users except current user
3. Exclude password field
4. Return users array

Query:
User.find({ _id: { $ne: loggedInUserId } }).select("-password")
```

**getMessages(req, res)**
```javascript
Process:
1. Get userToChatId from params
2. Get current user ID
3. Find messages where:
   - Sent by me to them, OR
   - Sent by them to me
4. Return messages

Query:
Message.find({
  $or: [
    { senderId: myId, receiverId: userToChatId },
    { senderId: userToChatId, receiverId: myId }
  ]
})
```

**sendMessage(req, res)**
```javascript
Process:
1. Extract text, image from body
2. Get receiverId from params
3. Get senderId from req.user
4. Upload image to Cloudinary (if present)
5. Create message document
6. Save to database
7. Get receiver's socket ID
8. Emit "newMessage" if receiver online
9. Return saved message

Real-time Broadcasting:
const receiverSocketId = getReceiverSocketId(receiverId);
if (receiverSocketId) {
  io.to(receiverSocketId).emit("newMessage", newMessage);
}
```

### Middleware

#### auth.middleware.js - protectRoute

```javascript
Process:
1. Extract JWT from cookies
2. Verify token exists
3. Decode token with secret
4. Extract userId from payload
5. Find user in database
6. Attach user to req.user
7. Call next()

Error Handling:
- 401: No token provided
- 401: Invalid token
- 404: User not found
- 500: Server error

Usage:
router.get("/protected", protectRoute, controller);
```

### Library Files

#### lib/db.js - MongoDB Connection
```javascript
- Connect to MongoDB using Mongoose
- Use MONGODB_URI from env
- Log connection success/error
- Export connectDB function
```

#### lib/socket.js - Socket.io Setup
```javascript
Components:
- Express app instance
- HTTP server wrapping app
- Socket.io server with CORS

User Socket Map:
{ userId: socketId }

Events:
- "connection": User connects
  - Store userId:socketId mapping
  - Emit "getOnlineUsers" to all clients
  
- "disconnect": User disconnects
  - Remove from userSocketMap
  - Emit updated "getOnlineUsers"

Exports:
- io: Socket server instance
- app: Express app
- server: HTTP server
- getReceiverSocketId(userId): Get socket ID
```

#### lib/utils.js - JWT Generation
```javascript
generateToken(userId, res):
1. Create JWT with userId payload
2. Set expiration: 7 days
3. Sign with JWT_SECRET
4. Set as HTTP-only cookie:
   - maxAge: 7 days in ms
   - httpOnly: true (XSS protection)
   - sameSite: "strict" (CSRF protection)
   - secure: true (production only)
5. Return token
```

#### lib/cloudinary.js - Cloudinary Config
```javascript
- Import cloudinary v2
- Configure with env variables:
  - cloud_name
  - api_key
  - api_secret
- Export configured instance
```

---

## 🗄 Database Schema

### User Model (user.model.js)

```javascript
{
  email: {
    type: String,
    required: true,
    unique: true
  },
  fullName: {
    type: String,
    required: true
  },
  password: {
    type: String,
    required: true,
    minlength: 6
  },
  profilePic: {
    type: String,
    default: ""
  },
  createdAt: Date,    // Auto-generated (timestamps)
  updatedAt: Date     // Auto-generated (timestamps)
}

Indexes:
- email (unique index)

Collection: users
```

### Message Model (message.model.js)

```javascript
{
  senderId: {
    type: ObjectId,
    ref: "User",
    required: true
  },
  receiverId: {
    type: ObjectId,
    ref: "User",
    required: true
  },
  text: {
    type: String,
    default: ""
  },
  image: {
    type: String,
    default: ""
  },
  createdAt: Date,    // Auto-generated (timestamps)
  updatedAt: Date     // Auto-generated (timestamps)
}

References:
- senderId → User._id
- receiverId → User._id

Collection: messages
```

### Database Relationships

```
User (1) ----→ (Many) Messages (as sender)
User (1) ----→ (Many) Messages (as receiver)
```

### Sample Documents

**User:**
```json
{
  "_id": "507f1f77bcf86cd799439011",
  "email": "john@example.com",
  "fullName": "John Doe",
  "password": "$2a$10$hashedpassword...",
  "profilePic": "https://res.cloudinary.com/...",
  "createdAt": "2026-01-29T10:00:00.000Z",
  "updatedAt": "2026-01-29T10:00:00.000Z"
}
```

**Message:**
```json
{
  "_id": "507f1f77bcf86cd799439012",
  "senderId": "507f1f77bcf86cd799439011",
  "receiverId": "507f1f77bcf86cd799439013",
  "text": "Hello, how are you?",
  "image": "https://res.cloudinary.com/...",
  "createdAt": "2026-01-29T10:30:00.000Z",
  "updatedAt": "2026-01-29T10:30:00.000Z"
}
```

---

## 🔒 Security Features

### 1. Authentication Security

**JWT (JSON Web Tokens)**
- Signed with secret key
- 7-day expiration
- Stored in HTTP-only cookies (not accessible via JavaScript)
- Prevents XSS attacks

**Password Security**
- Hashed using bcrypt
- Salt rounds: 10
- Never stored in plain text
- Never returned in API responses

### 2. Cookie Security

```javascript
Cookie Configuration:
- httpOnly: true        // Prevents XSS
- sameSite: "strict"    // Prevents CSRF
- secure: true          // HTTPS only (production)
- maxAge: 7 days        // Auto-expiration
```

### 3. CORS Configuration

```javascript
cors({
  origin: "http://localhost:5173",  // Specific origin
  credentials: true                  // Allow cookies
})
```

### 4. Input Validation

**Client-side:**
- Required field checks
- Email format validation
- Password length validation
- File type validation (images only)

**Server-side:**
- Field presence validation
- Password minimum length (6 chars)
- Email uniqueness check
- Mongoose schema validation

### 5. Route Protection

```javascript
Protected Routes:
- GET /api/auth/check
- PUT /api/auth/update-profile
- GET /api/messages/users
- GET /api/messages/:id
- POST /api/messages/send/:id

Mechanism:
All protected routes use protectRoute middleware
which verifies JWT before allowing access
```

### 6. Error Handling

**Never expose sensitive information in errors:**
- Generic "Invalid credentials" (not "Email not found")
- Internal errors logged server-side only
- User-friendly error messages client-side

### 7. Environment Variables

- Sensitive data in .env file
- .env excluded from version control (.gitignore)
- Different configs for dev/production

---

## 🌐 Real-time Communication

### Socket.io Implementation

#### Server-Side (lib/socket.js)

**Connection Handling:**
```javascript
io.on("connection", (socket) => {
  // Extract userId from handshake query
  const userId = socket.handshake.query.userId;
  
  // Store mapping
  userSocketMap[userId] = socket.id;
  
  // Broadcast online users to all clients
  io.emit("getOnlineUsers", Object.keys(userSocketMap));
  
  // Handle disconnect
  socket.on("disconnect", () => {
    delete userSocketMap[userId];
    io.emit("getOnlineUsers", Object.keys(userSocketMap));
  });
});
```

**Broadcasting Messages:**
```javascript
// In sendMessage controller
const receiverSocketId = getReceiverSocketId(receiverId);
if (receiverSocketId) {
  io.to(receiverSocketId).emit("newMessage", newMessage);
}
```

#### Client-Side (useAuthStore.js)

**Connection:**
```javascript
connectSocket: () => {
  const { authUser } = get();
  if (!authUser || get().socket?.connected) return;
  
  const socket = io(BASE_URL, {
    query: { userId: authUser._id }
  });
  
  socket.connect();
  set({ socket });
  
  // Listen for online users
  socket.on("getOnlineUsers", (userIds) => {
    set({ onlineUsers: userIds });
  });
}
```

**Message Subscription (useChatStore.js):**
```javascript
subscribeToMessages: () => {
  const socket = useAuthStore.getState().socket;
  
  socket.on("newMessage", (newMessage) => {
    // Check if message is from selected user
    if (newMessage.senderId === selectedUser._id) {
      set({ messages: [...get().messages, newMessage] });
    }
  });
}
```

### Real-time Features

1. **Online Status**
   - Updates when users connect/disconnect
   - Broadcasted to all connected clients
   - Visual indicators in sidebar

2. **Instant Messaging**
   - Messages delivered immediately
   - No page refresh needed
   - Updates recipient's UI in real-time

3. **Connection Management**
   - Auto-connect on login
   - Auto-disconnect on logout
   - Reconnection handling

---

## 📦 State Management

### Zustand Store Pattern

**Why Zustand?**
- Minimal boilerplate
- No Provider wrapper needed
- Excellent TypeScript support
- Built-in devtools
- Small bundle size (~1KB)

### Store Structure

```javascript
const useStore = create((set, get) => ({
  // State variables
  stateVar: initialValue,
  
  // Actions (functions)
  action: async (params) => {
    set({ loading: true });
    try {
      const result = await apiCall(params);
      set({ stateVar: result, loading: false });
    } catch (error) {
      set({ loading: false });
      handleError(error);
    }
  }
}));
```

### Usage in Components

```javascript
const Component = () => {
  const { stateVar, action } = useStore();
  
  useEffect(() => {
    action();
  }, [action]);
  
  return <div>{stateVar}</div>;
};
```

### State Persistence

**Theme Store:**
```javascript
- Reads from localStorage on init
- Saves to localStorage on change
- Persists across page refreshes
```

---

## 🚢 Deployment

### Production Build

**Frontend:**
```bash
cd frontend
npm run build
# Creates: frontend/dist/
```

**Backend serves frontend:**
```javascript
if (process.env.NODE_ENV === "production") {
  app.use(express.static(path.join(__dirname, "../frontend/dist")));
  
  app.get("*", (req, res) => {
    res.sendFile(path.join(__dirname, "../frontend/dist/index.html"));
  });
}
```

### Deployment Platforms

**Recommended:**
- **Render** (Full-stack deployment)
- **Railway** (Easy setup)
- **Heroku** (Classic option)
- **DigitalOcean** (App Platform)

**Steps:**
1. Push code to GitHub
2. Connect repository to platform
3. Set environment variables
4. Configure build command: `npm run build`
5. Configure start command: `npm start`
6. Deploy

### Environment Configuration

**Production .env:**
```env
MONGODB_URI=mongodb+srv://...
PORT=5001
JWT_SECRET=your_production_secret
NODE_ENV=production
CLOUDINARY_CLOUD_NAME=...
CLOUDINARY_API_KEY=...
CLOUDINARY_API_SECRET=...
```

---

## 💼 Frequently Asked Questions

### General Architecture

**Q: Explain your project's architecture.**

**A:** Converse follows a 3-tier architecture:
1. **Client Tier**: React SPA with Zustand for state management, communicates via Axios (HTTP) and Socket.io (WebSocket)
2. **Server Tier**: Node.js/Express REST API with JWT authentication, Socket.io server for real-time features, and middleware for request processing
3. **Data Tier**: MongoDB for user/message storage and Cloudinary for image CDN

**Q: How does authentication work?**

**A:** We use JWT-based authentication:
1. User submits credentials to `/api/auth/login`
2. Server validates email/password using bcrypt
3. If valid, generates JWT with 7-day expiration
4. Token stored in HTTP-only cookie (XSS protection)
5. Cookie sent with every request
6. `protectRoute` middleware verifies token
7. User data attached to `req.user` for controllers

### Real-time Features

**Q: How did you implement real-time messaging?**

**A:** Using Socket.io WebSockets:
1. **Connection**: Client connects with `userId` in query params
2. **Storage**: Server maintains `userSocketMap` mapping `userId` to `socketId`
3. **Sending**: When user sends message via HTTP POST, controller checks if receiver is online
4. **Broadcasting**: If online, emits "newMessage" event to receiver's socket
5. **Receiving**: Client listens for "newMessage" event and updates UI
6. **Online Status**: Server broadcasts "getOnlineUsers" array on connect/disconnect

**Q: Why Socket.io over native WebSockets?**

**A:** Socket.io provides:
- Automatic reconnection
- Fallback to HTTP long-polling
- Room/namespace support
- Better browser compatibility
- Built-in event system
- Easier implementation

### Database & Performance

**Q: How is your database structured?**

**A:** Two main collections:
1. **Users**: Stores authentication and profile data with unique email index
2. **Messages**: References sender/receiver User IDs, stores text/image URLs

Messages query uses `$or` operator to fetch bidirectional conversations efficiently.

**Q: How do you handle image uploads?**

**A:**
1. Client converts image to base64
2. Sends to server in request body
3. Server uploads to Cloudinary CDN
4. Cloudinary returns permanent URL
5. URL saved in MongoDB (not the image itself)
6. This keeps database lean and leverages CDN for fast delivery

### Security

**Q: What security measures did you implement?**

**A:**
1. **Passwords**: Hashed with bcrypt (10 salt rounds), never stored plain
2. **JWT**: Signed tokens with expiration
3. **Cookies**: HTTP-only (XSS prevention), SameSite strict (CSRF prevention)
4. **CORS**: Configured with specific origin and credentials
5. **Validation**: Both client and server-side
6. **Protected Routes**: Middleware verification before access

**Q: What is the difference between authentication and authorization?**

**A:**
- **Authentication**: Verifying identity (login with credentials)
- **Authorization**: Verifying permissions (access to protected routes)

In Converse: Login authenticates, middleware authorizes access to protected endpoints.

### State Management

**Q: Why did you choose Zustand over Redux?**

**A:** Zustand offers:
- Simpler API (less boilerplate)
- No Provider wrapper needed
- Smaller bundle size (~1KB vs ~30KB)
- Built-in async support
- Easier learning curve

Perfect for small-to-medium apps like chat applications.

**Q: How do you manage global state?**

**A:** Three Zustand stores:
1. **useAuthStore**: Authentication state, socket connection, online users
2. **useChatStore**: Messages, user list, selected user
3. **useThemeStore**: UI theme preference

Each store is self-contained with state and actions.

### React & Frontend

**Q: How do you handle route protection?**

**A:** In `App.jsx`, routes conditionally render based on `authUser`:
```jsx
<Route 
  path="/" 
  element={authUser ? <HomePage /> : <Navigate to="/login" />} 
/>
```

On mount, `checkAuth()` verifies JWT, setting `authUser` if valid.

**Q: How do you prevent unnecessary re-renders?**

**A:**
- Zustand selectors extract only needed state
- React Router prevents full page reloads
- `useEffect` dependencies carefully managed
- Conditional rendering for chat components

### Backend & Node.js

**Q: Explain the middleware pattern.**

**A:** Middleware functions have access to request/response objects:
```javascript
const middleware = (req, res, next) => {
  // Perform operations
  // Modify req/res
  next(); // Pass to next middleware/controller
};
```

Our `protectRoute` middleware verifies JWT, attaches user to `req.user`, then calls `next()`.

**Q: How does Express handle async errors?**

**A:** We use try-catch blocks in async controllers:
```javascript
try {
  await operation();
  res.json(data);
} catch (error) {
  console.log(error);
  res.status(500).json({ message: "Internal Server Error" });
}
```

### Testing & Debugging

**Q: How would you test this application?**

**A:**
- **Unit Tests**: Jest for utility functions, controllers
- **Integration Tests**: Supertest for API endpoints
- **E2E Tests**: Playwright/Cypress for user flows
- **Real-time Tests**: Socket.io test utilities

**Q: How do you debug Socket.io issues?**

**A:**
- Console logs on connect/disconnect events
- Socket.io DevTools extension
- Network tab to monitor WebSocket frames
- Check `userSocketMap` state on server

---

## 🎯 Challenges Faced

### Challenge 1: Real-time Message Synchronization

**Problem:** Ensuring messages appear in correct order when sent rapidly.

**Solution:**
- MongoDB's `createdAt` timestamp for ordering
- Frontend sorts messages by timestamp
- Socket.io guarantees event order within connection

### Challenge 2: Socket Connection Management

**Problem:** Preventing duplicate socket connections on re-renders.

**Solution:**
```javascript
if (!authUser || get().socket?.connected) return;
```
Check if socket already connected before creating new connection.

### Challenge 3: Image Upload Performance

**Problem:** Large base64 images slow down requests.

**Solution:**
- Cloudinary handles optimization
- Async upload doesn't block UI
- CDN delivery for fast loading
- Could add image compression client-side

### Challenge 4: JWT Token Refresh

**Problem:** 7-day expiration requires re-login.

**Solution:**
- Current: User logs in again
- Future: Implement refresh token pattern
- Use access token (short-lived) + refresh token (long-lived)

### Challenge 5: Typing Indicators

**Problem:** Not yet implemented.

**Solution:**
- Emit "typing" event when user types
- Broadcast to receiver
- Clear indicator after timeout
- Store typing state in chat store

### Challenge 6: Message Read Receipts

**Problem:** No read status tracking.

**Solution:**
- Add `isRead` boolean to Message schema
- Emit "messageRead" event when message viewed
- Update database and broadcast to sender

### Challenge 7: Scalability

**Problem:** Single server can't handle millions of users.

**Solution:**
- Horizontal scaling with Redis adapter for Socket.io
- Load balancer distribution
- Database sharding by user ID
- CDN for static assets

---

## 📚 What I Learnt?

This project demonstrates proficiency in:

✅ Full-stack JavaScript development (MERN)  
✅ RESTful API design and implementation  
✅ Real-time bidirectional communication (WebSockets)  
✅ JWT-based authentication & authorization  
✅ State management patterns (Zustand)  
✅ Component-based UI architecture (React)  
✅ NoSQL database design (MongoDB)  
✅ Cloud services integration (Cloudinary)  
✅ Security best practices (XSS, CSRF prevention)  
✅ Responsive UI design (Tailwind CSS)  
✅ Git version control  
✅ Environment-based configuration  

---

## 🤝 Contributing

Contributions welcome! Please follow these steps:

1. Fork the repository
2. Create feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit changes (`git commit -m 'Add AmazingFeature'`)
4. Push to branch (`git push origin feature/AmazingFeature`)
5. Open Pull Request

---

## 👨‍💻 Author

**Aditya Giri**

---

## 🙏 Acknowledgments

- Socket.io documentation
- React documentation
- MongoDB documentation
- Tailwind CSS & DaisyUI
- Cloudinary
- The open-source community

---

<div align="center">

**⭐ Star this repository if you found it helpful!**

Made with ❤️ using the MERN Stack

</div>
