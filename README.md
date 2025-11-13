⭐ WeApRous – Custom HTTP Server & Hybrid Chat System
🏫 CO3094 – Computer Networks – Ho Chi Minh City University of Technology
📘 1. Introduction

This project implements:

🟦 Task 1A – Custom HTTP Server & Authentication
Built entirely on raw Python sockets, with full HTTP parsing, cookie/session handling, and a minimal routing framework.

🟩 Task 2.2 – Hybrid Chat Application
Implements peer registration, discovery, broadcast messaging, direct messaging, and a modern chat UI.

This assignment demonstrates practical understanding of:

TCP socket programming

HTTP protocol

State management with cookies

Peer communication

Real-time message handling

UI/UX considerations for networking applications

🎯 2. Features
🔐 Task 1A – HTTP Authentication

Custom built HTTP server (no Flask/Django)

Multi-threaded TCP handler

Request parsing: method, path, headers, cookies, body

Response builder (status line, headers, JSON/HTML)

Session + cookie authentication (auth, sessionid)

Login API + UI

💬 Task 2.2 – Hybrid Chat Application

Peer registration (/submit-info)

Channel join/listing

Peer discovery (/get-list)

Broadcast messaging

Direct peer-to-peer messaging

Modern chat UI (inspired by Messenger/Discord)

Auto-refresh every 2 seconds (polling)

Clickable peer for direct chat mode

Per-channel message history

🏗️ 3. System Architecture
📱 Chat UI          – HTML, CSS, JavaScript
│
├── 🌐 Chat API     – Broadcast + Direct Messaging
│
└── 🔌 HTTP Server  – Python Sockets (custom design)
       ├── Request Parser
       ├── Cookie / Session Manager
       ├── Routing Framework
       └── Static File Server

📁 4. Directory Structure
CO3094-weaprous/
│
├── daemon/
│   ├── backend.py          # Low-level TCP server
│   ├── httpadapter.py      # HTTP decode/encode + connection handling
│   ├── request.py          # Parse HTTP request line/headers/cookies
│   ├── response.py         # Build response (HTML/JSON)
│   └── weaprous.py         # Mini web framework (router)
│
├── apps/
│   └── app.py              # Task 1A + Task 2.2 API implementation
│
├── www/
│   ├── index.html          # Homepage
│   ├── login.html          # Authentication UI
│   └── chat.html           # Hybrid chat interface
│
├── static/                 # Static assets (optional)
│
├── start_app.py            # Start server (includes clickable URLs)
└── README.md

🚀 5. Running the Application
▶️ Start the Server
cd CO3094-weaprous/CO3094-weaprous
python start_app.py --server-ip 0.0.0.0 --server-port 9000

🌍 Open the Chat UI
http://127.0.0.1:9000/chat.html


Open multiple tabs to simulate multiple peers.

🔐 6. Task 1A – Authentication
POST /login
{
  "username": "admin",
  "password": "password"
}

✔ Successful Response
{
  "status": "authorized",
  "message": "Login successful"
}

🔒 Protected Route

Accessing / requires:

auth=true

sessionid=<valid token>

Else → 401 Unauthorized

💬 7. Task 2.2 – Hybrid Chat API
🔧 Peer Management
Endpoint	Method	Purpose
/submit-info	POST	Register peer (username, IP, port)
/add-list	POST	Join channel
/get-list	GET	Retrieve peer list + channel list
/connect-peer	POST	Retrieve IP/port of a target peer
💭 Messaging
Endpoint	Method	Purpose
/broadcast-peer	POST	Broadcast chat message
/send-peer	POST	Direct peer-to-peer message
/channel/messages	POST	Load message history
🖥️ 8. Chat UI Overview

The chat interface (chat.html) includes:

👤 Peer login module

📡 Channel selection

🧑‍🤝‍🧑 Peer list

💬 Message window

⌨️ Input composer

🔄 Automatic polling every 2 seconds

🎯 Direct chat mode (click peer name)

Modes

Broadcast Mode
Send to all peers in a channel

Direct Mode
Visible only to sender + target peer

🔄 9. Communication Workflow
Initialization Phase

Login (Task 1A)

Register peer → /submit-info

Join channel → /add-list

Fetch peers/channels → /get-list

Connection Setup
POST /connect-peer
{
  "from": "alice",
  "to": "bob"
}

Messaging Phase

Broadcast → /broadcast-peer

Direct → /send-peer

Retrieve history → /channel/messages

🛠️ 10. Technologies Used

Python 3

TCP sockets

Multi-threading

Custom HTTP parsing

Vanilla JavaScript

HTML + CSS (custom UI, no frameworks)

👨‍💻 11. Author

Trần Vũ Đình Huy
Computer Science & Engineering
Ho Chi Minh City University of Technology
Course: CO3094 – Computer Networks

📌 12. Project Status

All functionalities required for:

Task 1A (Authentication)

Task 2.2 (Hybrid Chat System)

have been fully implemented, tested, and successfully demonstrated.
