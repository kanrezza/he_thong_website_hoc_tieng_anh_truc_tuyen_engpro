# EngPro – Hệ thống Website Học Tiếng Anh Trực tuyến

Đồ án cơ sở: Phát triển website học tiếng Anh trực tuyến. EngPro là nền tảng luyện thi chứng chỉ tiếng Anh quốc tế, hỗ trợ ba vai trò Học viên, Giáo viên và Quản trị viên với đầy đủ quy trình học tập: ghi danh khóa học, học bài giảng, theo dõi tiến độ, làm bài kiểm tra và quản lý doanh thu.

## Công nghệ sử dụng

- Backend: Node.js, Express 4
- Cơ sở dữ liệu: MySQL 8 (driver mysql2)
- Xác thực: express-session, mã hóa mật khẩu bằng bcrypt
- Upload và xử lý file: multer, xlsx (nhập câu hỏi từ Excel)
- Frontend: HTML, CSS, JavaScript thuần (không framework)

## Tính năng chính

Học viên
- Đăng ký, đăng nhập, quản lý hồ sơ và đổi mật khẩu
- Xem danh sách khóa học, ghi danh và học bài giảng
- Theo dõi tiến độ hoàn thành từng khóa học
- Làm bài kiểm tra đầu vào, bài luyện tập và bài thi thử
- Gửi phản hồi cho khóa học

Giáo viên
- Quản lý bài giảng và tài liệu của khóa học
- Tạo và quản lý ngân hàng câu hỏi cho từng bài kiểm tra
- Theo dõi tiến độ và kết quả học tập của học viên
- Xem thống kê giảng dạy

Quản trị viên
- Quản lý người dùng, khóa học và ghi danh
- Tạo bài kiểm tra chung và nhập câu hỏi từ file Excel
- Thống kê tổng quan hệ thống và báo cáo doanh thu

## Cấu trúc thư mục

```
project_EngPro/
├── server.js            # Toàn bộ API backend (Express + MySQL)
├── index.html           # Trang chủ
├── pages/               # Các trang giao diện (login, dashboard, học, thi...)
├── js/                  # Script phía client dùng chung
├── db/
│   ├── engpro.sql       # Script tạo cơ sở dữ liệu
│   └── eer.png          # Sơ đồ quan hệ thực thể (ERD)
├── uploads/             # Nơi lưu file tải lên (không đưa lên Git)
├── package.json
└── README.md
```

## Yêu cầu môi trường

- Node.js phiên bản 20.12 trở lên
- MySQL phiên bản 8 trở lên

## Cài đặt và chạy

1. Cài đặt các gói phụ thuộc

```bash
npm install
```

2. Tạo cơ sở dữ liệu từ script có sẵn

```bash
mysql -u root -p < db/engpro.sql
```

3. Tạo file cấu hình `.env` ở thư mục gốc

```env
PORT=8080
MYSQLHOST=127.0.0.1
MYSQLPORT=3306
MYSQLUSER=root
MYSQLPASSWORD=mat_khau_cua_ban
MYSQLDATABASE=engpro
```

4. Khởi chạy ứng dụng

```bash
npm start      # chế độ thường
npm run dev    # chế độ tự reload khi sửa code
```

5. Mở trình duyệt tại địa chỉ

```
http://localhost:8080
```

## Tổng quan API

API được tổ chức theo nhóm vai trò, trả về dữ liệu dạng JSON theo định dạng thống nhất `{ success, data }` hoặc `{ success, message }`.

- `/api/auth/*`    Đăng ký, đăng nhập, đăng xuất, lấy thông tin phiên
- `/api/user/*`    Chức năng dành cho học viên: khóa học, tiến độ, bài thi, hồ sơ
- `/api/gv/*`      Chức năng dành cho giáo viên: bài giảng, câu hỏi, thống kê
- `/api/admin/*`   Chức năng dành cho quản trị viên: người dùng, ghi danh, doanh thu

## Cơ sở dữ liệu

Script `db/engpro.sql` tạo các bảng chính gồm: users, categories, courses, lectures, materials, enrollments, lecture_progress, tests, questions, test_results, admin_tests, admin_questions, admin_test_results, feedback, teacher_feedback. Sơ đồ quan hệ thực thể được mô tả trong `db/eer.png`.

## Tác giả

kanrezza – Đồ án cơ sở
