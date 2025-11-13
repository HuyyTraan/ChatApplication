🌐 WeApRous – Custom HTTP Server & Hybrid Chat SystemCO3094 – Computer Networks – Ho Chi Minh City University of Technology (HCMUT)WeApRous là một framework mạng gọn nhẹ được xây dựng từ đầu bằng Python sockets, được phát triển cho môn học CO3094 – Mạng Máy Tính.Dự án này thể hiện sự hiểu biết sâu sắc về:Giao thức TCP/HTTPGiao tiếp ở tầng socketTương tác Client–Server & Peer–to–PeerXác thực bằng Cookie/SessionThiết kế ứng dụng web thời gian thực🚀 Tổng quan về dự ánDự án bao gồm hai phần chính:TaskDescription🟦 Task 1A – HTTP Server & AuthenticationCài đặt một HTTP server đa luồng tùy chỉnh, bộ phân tích request, và hệ thống đăng nhập dựa trên session.🟩 Task 2.2 – Hybrid Chat ApplicationMột ứng dụng chat thời gian thực hỗ trợ broadcast và nhắn tin trực tiếp (peer-to-peer) thông qua các endpoint HTTP và giao diện web hiện đại.🧠 Tính năng chính🔐 Task 1A – HTTP ServerWeb server dựa trên Python socket (không dùng framework bên ngoài).Xử lý client đa luồng (multi-threaded).Phân tích request HTTP (method, path, headers, cookies, body).Xác thực dựa trên cookie (auth=true, sessionid).Hệ thống routing tối giản sử dụng decorators.Phục vụ tệp tĩnh (HTML, CSS, JS).💬 Task 2.2 – Hybrid ChatĐăng ký peer và quản lý kênh chat.Khám phá peer dựa trên Tracker.Hai chế độ giao tiếp:Broadcast (đến tất cả peer trong kênh).Direct (nhắn tin riêng tư peer-to-peer).Cơ chế Polling để cập nhật theo thời gian thực.Giao diện chat hiện đại, responsive.API backend đơn giản, có khả năng mở rộng.🛠️ Công nghệ sử dụngComponentTechnologyBackendPython (sockets, threading)ProtocolHTTP 1.1 (custom implementation)AuthenticationCookie + SessionFrontendHTML5, CSS3, JavaScriptCommunicationJSON over HTTPArchitectureClient–Server + Hybrid Peer Logic🧩 Kiến trúc & Cấu trúc thư mụcSơ đồ kiến trúcPlaintext📡 Client (Web Browser)
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
Cấu trúc thư mụcCO3094-weaprous/
│
├── daemon/
│   ├── backend.py          # Lõi logic TCP server
│   ├── httpadapter.py      # Phân tích HTTP và client adapter
│   ├── request.py          # Phân tích request line, header, cookie
│   ├── response.py         # Xây dựng response (HTML/JSON)
│   └── weaprous.py         # Framework routing gọn nhẹ
│
├── apps/
│   └── app.py              # Logic API cho Task 1A + Task 2.2
│
├── www/
│   ├── index.html          # Trang chủ
│   ├── login.html          # Giao diện xác thực
│   └── chat.html           # Giao diện web chat
│
├── static/                 # (Tùy chọn) Tệp tĩnh, assets
│
├── start_app.py            # Entry point (khởi chạy server)
└── README.md
⚙️ Cài đặt & Khởi chạyChạy Server:Mở terminal và điều hướng đến thư mục dự án:Bashcd CO3094-weaprous/CO3094-weaprous
python start_app.py --server-ip 0.0.0.0 --server-port 9000
Truy cập ứng dụng:Mở trình duyệt và truy cập:http://127.0.0.1:9000/chat.htmlMẹo: Mở nhiều tab trình duyệt để giả lập nhiều peer cùng tham gia.📚 Tài liệu API🔐 Task 1A – Authentication APIPOST /loginXác thực người dùng và cấp cookie.Request Body:JSON{
  "username": "admin",
  "password": "password"
}
Response (Success):JSON{
  "status": "authorized",
  "message": "Login successful"
}
Lưu ý: Các route được bảo vệ yêu cầu:Cookie auth=trueMột sessionid hợp lệNếu không, server sẽ trả về 401 Unauthorized.💬 Task 2.2 – Hybrid Chat API🧭 Quản lý Peer & KênhEndpointMethodDescription/submit-infoPOSTĐăng ký thông tin peer (username, IP, port)./add-listPOSTTham gia vào một kênh chat./get-listGETLấy danh sách tất cả peer và kênh hiện có./connect-peerPOSTLấy IP/port của một peer cụ thể để kết nối trực tiếp.💭 Gửi & Nhận tin nhắnEndpointMethodDescription/broadcast-peerPOSTGửi tin nhắn broadcast đến tất cả peer trong kênh./send-peerPOSTGửi tin nhắn riêng tư (direct) đến một peer./channel/messagesPOSTLấy lịch sử tin nhắn của một kênh.🖥️ Giao diện người dùng (chat.html)Giao diện chat.html cung cấp trải nghiệm giống Messenger:Bên trái: Danh sách Peer & Kênh.Bên phải: Khung hội thoại.Bên dưới: Khung soạn thảo tin nhắn.Tự động làm mới (auto-refresh) mỗi 2 giây để lấy tin nhắn mới.Chế độ giao tiếp🌍 Broadcast Mode: Tin nhắn được gửi đến tất cả mọi người trong kênh.🔒 Direct Mode: Tin nhắn được gửi riêng tư giữa hai peer. (Chuyển sang chế độ này bằng cách nhấp vào tên một peer trong danh sách).🔄 Luồng hoạt động (Workflow)Phase Khởi tạo:Peer đăng nhập (/login).Peer đăng ký thông tin (/submit-info).Peer tham gia kênh (/add-list).Peer lấy danh sách các peer khác (/get-list).Phase Thiết lập kết nối (Direct):Peer A yêu cầu thông tin của Peer B qua /connect-peer.Phase Chat:Gửi Broadcast: POST /broadcast-peer.Gửi Direct: POST /send-peer.Lấy tin nhắn mới: POST /channel/messages (thực hiện polling).🧾 Trạng thái dự án✅ Task 1A – Completed (Authentication & HTTP Server)✅ Task 2.2 – Completed (Hybrid Chat with Broadcast + Direct Messaging)✅ UI – Completed (Responsive, functional, auto-refreshing)✅ Architecture – Verified and documented🧭 Tóm tắtDự án này trình bày việc triển khai end-to-end của một hệ thống giao tiếp dựa trên HTTP—từ việc phân tích giao thức ở tầng socket đến tương tác peer-to-peer trên nền tảng web.Nó là cầu nối giữa lập trình mạng cấp thấp và thiết kế tầng ứng dụng, cho thấy cách các hệ thống truyền thông thực tế được xây dựng từ những nguyên tắc cơ bản.👨‍💻 Tác giảTrần Vũ Đình HuyKhoa Khoa học và Kỹ thuật Máy tínhTrường Đại học Bách khoa (HCMUT)Môn học: CO3094 – Mạng Máy Tính
