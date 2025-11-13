🛰️ WeApRous – Hybrid Chat Application
CO3094 – Computer Networks – HCMUT
Big Lab Assignment (Task 1A + Task 2.2)
📌 Giới thiệu

Dự án này triển khai HTTP Server tự xây dựng từ socket và Hybrid Chat Application (Client–Server + Pseudo P2P) dựa trên yêu cầu của môn CO3094 – Computer Networks (232/233).

Hệ thống gồm:

Task 1A – Authentication Handling

Tự xây dựng HTTP server bằng Python socket

Xử lý HTTP request, response, cookie, session

API Login + trang chủ yêu cầu cookie auth và sessionid

Task 2.2 – Hybrid Chat Application

Mô phỏng quá trình:

Peer registration

Tracker update

Peer discovery

Connection setup

Broadcast chatting

Direct peer messaging

Kèm theo web UI giống messenger dùng HTML/CSS/JS

📁 Cấu trúc thư mục
CO3094-weaprous/
│
├── daemon/                 # HTTP server core (socket)
│   ├── backend.py          # Multi-threaded TCP server
│   ├── httpadapter.py      # Handle low-level HTTP parsing
│   ├── request.py          # Parse HTTP request (method, headers, cookies, body)
│   ├── response.py         # Build HTTP responses (JSON + static HTML)
│   └── weaprous.py         # Mini web framework (route decorator)
│
├── apps/
│   └── app.py              # Task 1A + Task 2.2 API handlers
│
├── www/
│   ├── index.html          # Homepage (Task 1A)
│   ├── login.html          # Login UI (Task 1A)
│   └── chat.html           # Web UI cho Task 2.2
│
├── static/                 # Icons / CSS (optional)
│
├── start_app.py            # Start server (clickable URL)
├── start_backend.py
├── start_proxy.py
└── README.md

🚀 Cách chạy dự án
1️⃣ Chạy server
cd CO3094-weaprous/CO3094-weaprous
python start_app.py --server-ip 0.0.0.0 --server-port 9000


Sau khi chạy, terminal sẽ hiện:

▶ Backend listening on: http://0.0.0.0:9000
▶ Open chat UI:
   👉 http://127.0.0.1:9000/chat.html


Click để mở ngay web UI.

🧪 Demo Task 1A – Authentication
API Login

POST /login

Body:

{
  "username": "admin",
  "password": "password"
}


Trả về:

{
  "status": "authorized",
  "message": "Login successful"
}

Trang chủ yêu cầu cookie

Khi vào /, server kiểm tra:

auth=true

sessionid=<random>

Nếu thiếu → trả 401 Unauthorized.

💬 Demo Task 2.2 – Hybrid Chat Application
Giao diện chat

Mở trên trình duyệt:

http://127.0.0.1:9000/chat.html


Web UI gồm:

Peer login + info

Channel list

Peers list

Chat window (messages)

Mode:

Broadcast (gửi cho mọi người trong channel)

Direct (click vào 1 peer để gửi riêng)

🔌 Danh sách API cho Task 2.2
API	Method	Mô tả
/submit-info	POST	Đăng ký peer lên tracker
/add-list	POST	Join channel
/get-list	GET	Lấy danh sách peers + channels
/connect-peer	POST	Lấy IP/port của peer đích
/broadcast-peer	POST	Gửi broadcast message
/send-peer	POST	Gửi direct message
/channel/messages	POST	Lấy lịch sử chat của channel
📌 Chi tiết hoạt động hệ thống
1. Initialization Phase (Client–Server)

Client gửi /submit-info để đăng ký

Server lưu thông tin peer vào CHAT_PEERS

Client gửi /add-list để join channel

Client gọi /get-list để xem danh sách peers/channels

2. Connection Setup

Gọi API:

POST /connect-peer
{
  "from": "alice",
  "to": "bob"
}


Server trả IP & port để client có thể mở kết nối riêng (nếu cần).

🔊 3. Peer Chatting Phase
✔ Broadcast messaging

Gửi cho tất cả người trong channel:

POST /broadcast-peer
{
  "from": "alice",
  "channel": "general",
  "message": "hello everyone"
}

✔ Direct messaging

Gửi riêng 1 người:

POST /send-peer
{
  "from": "alice",
  "to": "bob",
  "channel": "general",
  "message": "hi bob"
}


UI tự động lọc: chỉ 2 người liên quan mới thấy direct message.

🖥️ Web UI (chat.html)

Viết bằng HTML + CSS thuần (không framework)

Fancy UI style: shadow, blur, gradient, dark mode

Features:

Login peer

List channels

List peers

Broadcast chat

Direct chat (click peer → bật direct mode)

Auto-refresh 2s/lần (polling)

🛠️ Công nghệ sử dụng

Python socket (TCP server)

Tự implementar:

HTTP parsing

Multi-thread connection handler

Cookie/session

REST API routing

HTML/CSS/JS thuần (không framework)

🎓 Sinh viên thực hiện

Trần Vũ Đình Huy
Khoa Khoa Học & Kỹ Thuật Máy Tính – Đại Học Bách Khoa TP.HCM
MSSV: tự điền
Môn: CO3094 – Computer Networks (232/233)

📝 Ghi chú

Đây là phiên bản đầy đủ của cả Task 1A + Task 2.2 theo đúng cấu trúc bài tập lớn.

Server chạy độc lập, không dùng framework Flask/Django — hoàn toàn socket thuần theo yêu cầu đề tài.
