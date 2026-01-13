<div align="center">

# 🌐 WeApRous – Custom HTTP Server & Hybrid Chat
### CO3094 – Computer Networks | Ho Chi Minh City University of Technology    
 
![Python](https://img.shields.io/badge/Language-Python_-blue?style=for-the-badge&logo=python)
![Protocol](https://img.shields.io/badge/Protocol-HTTP%2F1.1-green?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completed-success?style=for-the-badge) 
![Course](https://img.shields.io/badge/Course-CO3094-orange?style=for-the-badge)

<p> 
  <b>A lightweight networking framework built from scratch using Python sockets.</b><br>
  <i>Demonstrating TCP/HTTP protocols, Client–Server architecture, and Real-time Web Application design.</i>
</p>

</div>

---

## 🚀 Overview

**WeApRous** is a custom networking project developed for the course **CO3094**. It bridges low-level network programming and application-layer design by implementing a web server without external frameworks.

The project consists of two main components:
1.  **🟦 Task 1A:** A Multi-threaded HTTP Server with custom request parsing and cookie-based authentication.
2.  **🟩 Task 2.2:** A Hybrid Chat Application supporting both **Broadcast** (channel-wide) and **Direct** (P2P) messaging.

---

## 🧠 Key Features

### 🔐 Task 1A – HTTP Server Core
* **Pure Python Sockets:** No external web frameworks (Flask/Django) used.
* **Multi-threading:** Handles multiple client connections simultaneously.
* **HTTP Parser:** Custom parsing for Methods (GET/POST), Headers, Cookies, and Body.
* **Authentication:** Session-based login system (`auth=true`, `sessionid`).
* **Routing:** Minimalistic routing system using decorators.
* **Static Files:** Serves HTML, CSS, and JS assets efficiently.

### 💬 Task 2.2 – Hybrid Chat System
* **Dual Communication Modes:**
    * 🌍 **Broadcast:** Messages sent to all peers in a channel.
    * 🔒 **Direct:** Private peer-to-peer messaging.
* **Tracker Mechanism:** Manages peer discovery and channel lists.
* **Real-time Updates:** Polling mechanism for instant message delivery.
* **Modern UI:** Responsive web interface with auto-refresh logic.

---

## 🧩 Architecture

The system follows a **Client-Server** model combined with **Hybrid Peer Logic**.

```mermaid
graph TD
    A[Client / Web Browser] -->|HTTP Request| B(Server / Python Daemon)
    B -->|Parse| C{Router}
    C -->|Task 1A| D[Auth & Static Files]
    C -->|Task 2.2| E[Chat API & Tracker]
    E --> F[Socket Layer]
🗂️ Directory StructureBashCO3094-weaprous/
│
├── daemon/                 # Core Server Logic
│   ├── backend.py          # TCP server implementation
│   ├── httpadapter.py      # HTTP parsing adapter
│   ├── request.py          # Request parsing (headers, cookies)
│   ├── response.py         # Response builder (HTML/JSON)
│   └── weaprous.py         # Routing framework
│
├── apps/
│   └── app.py              # Business Logic (Auth + Chat APIs)
│
├── www/                    # Frontend Interface
│   ├── index.html          # Homepage
│   ├── login.html          # Login UI
│   └── chat.html           # Main Chat UI
│
├── static/                 # Assets (CSS/JS/Images)
├── start_app.py            # Entry Point
└── README.md
⚙️ Setup & Execution1. PrerequisitesPython 3.x installed.2. Run the ServerNavigate to the project directory and start the application:Bashcd CO3094-weaprous/CO3094-weaprous
python start_app.py --server-ip 0.0.0.0 --server-port 9000
3. Access the ApplicationOpen your web browser and visit:http://127.0.0.1:9000/chat.htmlTip: Open the URL in multiple tabs (Incognito mode recommended) to simulate multiple peers.🔌 API Documentation🔐 Authentication (Task 1A)EndpointMethodDescription/loginPOSTAuthenticates user. Requires username & password. Returns sessionid.Protected Routes*Checks for Cookie: auth=true and valid session. Returns 401 if invalid.💬 Hybrid Chat (Task 2.2)Peer ManagementEndpointMethodDescription/submit-infoPOSTRegisters peer (Username, IP, Port)./add-listPOSTJoins a specific channel./get-listGETRetrieves list of active peers and channels./connect-peerPOSTRetrieves IP/Port for a target peer (for Direct Mode).MessagingEndpointMethodDescription/broadcast-peerPOSTSends a message to all peers in the channel./send-peerPOSTSends a private message to a specific peer./channel/messagesPOSTRetrieves message history for the UI.🖥️ User InterfaceThe interface (chat.html) provides a responsive, Messenger-like experience:Left Panel: Peer list & Channel selection.Right Panel: Message history & Input composer.Interaction:Clicking a peer switches to Direct Mode.Default view is Broadcast Mode.Auto-refreshes every 2 seconds to fetch new data.🛠️ Technology StackBackend: Python (Sockets, Threading)Protocol: HTTP 1.1 (Custom Implementation)Frontend: HTML5, CSS3, JavaScript (Fetch API)Data Exchange: JSON over HTTP👨‍💻 AuthorTrần Vũ Đình HuyInstitution: Ho Chi Minh City University of Technology (HCMUT)Course: Computer Networks (CO3094)<div align="center"><i>This project is for educational purposes, demonstrating how real communication systems are built from first principles.</i></div>
