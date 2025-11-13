🌐 WeApRous – Custom HTTP Server & Hybrid Chat System
CO3094 – Computer Networks – Ho Chi Minh City University of Technology
🚀 Overview

WeApRous is a lightweight networking framework built from scratch using Python sockets, developed for the course CO3094 – Computer Networks.

The project showcases a deep understanding of:

TCP/HTTP protocols

Socket-level communication

Client–Server & Peer–to–Peer interaction

Cookie/Session authentication

Real-time web application design

It consists of two main parts:

Task	Description
🟦 Task 1A – HTTP Server & Authentication	Implements a custom multi-threaded HTTP server, request parser, session-based login system.
🟩 Task 2.2 – Hybrid Chat Application	A real-time chat app supporting broadcast and direct peer messaging via HTTP endpoints and a modern web UI.
🧠 Key Features
🔐 Task 1A – HTTP Server

Python socket-based web server (no external frameworks)

Multi-threaded client handling

HTTP request parsing (method, path, headers, cookies, body)

Cookie-based authentication (auth=true, sessionid)

Minimalistic routing system using decorators

Static file serving (HTML, CSS, JS)

💬 Task 2.2 – Hybrid Chat

Peer registration and channel management

Tracker-based peer discovery

Two communication modes:

Broadcast (to all peers in a channel)

Direct (private peer-to-peer message)

Polling mechanism for real-time updates

Responsive, modern chat UI

Simple, scalable backend API

🧩 Architecture Overview
📡 Client (Web Browser)
│
├── Chat UI (HTML + CSS + JS)
│    ├── Peer Login
│    ├── Channel Selection
│    ├── Peer List
│    └── Message Window
│
└── Server (Python)
     ├── HTTP Parser (Request + Response)
     ├── Routing System (Task 1A)
     ├── Chat APIs (Task 2.2)
     ├── Tracker + Channel Manager
     └── Socket Layer (Multi-threaded)

🗂️ Directory Structure
CO3094-weaprous/
│
├── daemon/
│   ├── backend.py          # Core TCP server logic
│   ├── httpadapter.py      # HTTP parsing and client adapter
│   ├── request.py          # Request line, header, and cookie parsing
│   ├── response.py         # Response builder (HTML/JSON)
│   └── weaprous.py         # Lightweight routing framework
│
├── apps/
│   └── app.py              # API logic for Task 1A + Task 2.2
│
├── www/
│   ├── index.html          # Homepage
│   ├── login.html          # Authentication UI
│   └── chat.html           # Hybrid chat web interface
│
├── static/                 # Optional assets
│
├── start_app.py            # Entry point (clickable startup links)
└── README.md

⚙️ Setup & Execution
1. Run the Server
cd CO3094-weaprous/CO3094-weaprous
python start_app.py --server-ip 0.0.0.0 --server-port 9000

2. Access the Application

Visit in your browser:

http://127.0.0.1:9000/chat.html


Open multiple tabs to simulate multiple peers.

🔐 Task 1A – Authentication API

POST /login
Authenticate user and issue cookies.

Request

{
  "username": "admin",
  "password": "password"
}


Response

{
  "status": "authorized",
  "message": "Login successful"
}


Protected routes require:

Cookie auth=true

Valid sessionid

Unauthorized → 401 Unauthorized

💬 Task 2.2 – Hybrid Chat API
🧭 Peer Management
Endpoint	Method	Description
/submit-info	POST	Register peer (username, IP, port)
/add-list	POST	Join a channel
/get-list	GET	Retrieve all peers and channels
/connect-peer	POST	Retrieve IP/port for a specific peer
💭 Messaging
Endpoint	Method	Description
/broadcast-peer	POST	Send broadcast message to all peers
/send-peer	POST	Send private (direct) message
/channel/messages	POST	Retrieve channel message history
🖥️ User Interface

chat.html provides a responsive, Messenger-like experience:

Left: Peer & channel list

Right: Message panel

Bottom: Input composer

Auto refresh every 2 seconds

Click peer → switch to Direct Mode

Clear distinction between broadcast and direct messages

Modes

🌍 Broadcast Mode: message sent to everyone in the channel.

🔒 Direct Mode: message sent privately between two peers.

🔄 Workflow Summary

Initialization Phase

Peer logs in (/login)

Peer registers info (/submit-info)

Joins a channel (/add-list)

Retrieves peer list (/get-list)

Connection Setup

Peer requests target info via /connect-peer

Chatting Phase

Broadcast → /broadcast-peer

Direct → /send-peer

Fetch messages → /channel/messages

🛠️ Technology Stack
Component	Technology
Backend	Python (sockets, threading)
Protocol	HTTP 1.1 (custom implementation)
Authentication	Cookie + Session
Frontend	HTML5, CSS3, JavaScript
Communication	JSON over HTTP
Architecture	Client–Server + Hybrid Peer Logic
👨‍💻 Author

Trần Vũ Đình Huy
Computer Science and Engineering
Ho Chi Minh City University of Technology (HCMUT)
Course: CO3094 – Computer Networks

🧾 Project Status

✅ Task 1A – Completed (Authentication & HTTP Server)
✅ Task 2.2 – Completed (Hybrid Chat with Broadcast + Direct Messaging)
✅ UI – Responsive, functional, auto-refreshing
✅ Architecture – Verified and documented

🧭 Summary

This project demonstrates end-to-end implementation of an HTTP-based communication system — from socket-level protocol parsing to web-based peer interaction.
It bridges low-level network programming and application-layer design, showcasing how real communication systems are built from first principles.
