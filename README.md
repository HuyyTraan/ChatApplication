🛰️ WeApRous – Hybrid Chat Application
CO3094 – Computer Networks – HCMUT
📌 Overview

This project implements:

Task 1A – Authentication (HTTP Server)

Custom HTTP server using Python sockets

Request parsing (method, path, headers, cookies, body)

Response builder (status line, headers, JSON, static HTML)

Cookie & session management (auth=true + sessionid)

Simple login page + API /login

Task 2.2 – Hybrid Chat Application

Peer registration, tracker update

Peer discovery

Connection setup

Broadcast chatting

Direct peer messaging

Channel management

Modern web UI (HTML + CSS + JavaScript)

📂 Project Structure
CO3094-weaprous/
│
├── daemon/
│   ├── backend.py          # Low-level TCP server (multi-threaded)
│   ├── httpadapter.py      # HTTP parsing, connection handling
│   ├── request.py          # Parse HTTP request & cookies
│   ├── response.py         # JSON + static HTML responses
│   └── weaprous.py         # Mini web framework (route decorator)
│
├── apps/
│   └── app.py              # Task 1A + Task 2.2 API handlers
│
├── www/
│   ├── index.html          # Task 1A homepage
│   ├── login.html          # Login UI (Task 1A)
│   └── chat.html           # Web UI for hybrid chat
│
├── static/                 # (Optional) assets, icons
│
├── start_app.py            # Start server with clickable link
├── start_backend.py
├── start_proxy.py
└── README.md

🚀 Running the Server
cd CO3094-weaprous/CO3094-weaprous
python start_app.py --server-ip 0.0.0.0 --server-port 9000


After starting, you will see:

Backend listening on: http://0.0.0.0:9000
Open chat UI:
   http://127.0.0.1:9000/chat.html


Open a browser and visit the chat UI.

🧪 Task 1A – Authentication API
POST /login
Request body:
{
  "username": "admin",
  "password": "password"
}

Successful response:
{
  "status": "authorized",
  "message": "Login successful"
}

Access Control

Accessing / requires:

auth=true

sessionid=<token>

Otherwise → 401 Unauthorized.

💬 Task 2.2 – Hybrid Chat Application

The chat system supports:

Broadcast (send to everyone in the channel)

Direct chat (send privately to one peer)

Channel management

Peer discovery

Automatic refresh (polling every 2 seconds)

Open UI:

http://127.0.0.1:9000/chat.html


Each browser tab acts as a peer.

🔌 Chat APIs
Endpoint	Method	Description
/submit-info	POST	Register peer (username, IP, port)
/add-list	POST	Join a channel
/get-list	GET	Get peers + channels
/connect-peer	POST	Retrieve peer IP/port for connection setup
/broadcast-peer	POST	Send broadcast message
/send-peer	POST	Send direct message
/channel/messages	POST	Fetch channel message history
📡 Protocol Flow Overview
1. Initialization Phase

Peer → /submit-info

Server updates tracker

Peer joins channel via /add-list

Peer gets list via /get-list

2. Connection Setup
POST /connect-peer
{
   "from": "alice",
   "to": "bob"
}


Returns IP + port of target peer.

3. Chatting Phase
Broadcast
POST /broadcast-peer
{
  "from": "alice",
  "channel": "general",
  "message": "hello everyone"
}

Direct
POST /send-peer
{
  "from": "alice",
  "to": "bob",
  "channel": "general",
  "message": "hi bob"
}

🖥️ Web UI (chat.html)

Features:

Peer login

Realtime peer list

Channel list

Broadcast & direct messaging

Beautiful modern UI

Auto-refreshing messages

Direct mode: Click a peer → UI switches to direct message mode.

🛠️ Technologies Used

Python (socket programming)

Custom HTTP server (no Flask/Django)

HTML / CSS / JavaScript

Multi-thread TCP architecture

Client polling for message updates

👨‍🎓 Author

Trần Vũ Đình Huy
Computer Science & Engineering – HCMUT
Course: CO3094 – Computer Networks

✔ Status

All requirements for Task 1A and Task 2.2 have been fully implemented and verified.
