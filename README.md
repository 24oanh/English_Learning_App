# 📚 Minlish - Smart English Learning Application

<p align="center">
  <b>Minlish</b> là ứng dụng hỗ trợ học tiếng Anh thông minh trên hệ điều hành Android, tích hợp thuật toán lặp lại ngắt quãng <b>(Spaced Repetition System - SM-2)</b>, giúp người học ghi nhớ từ vựng lâu hơn, luyện tập ngữ pháp và theo dõi tiến độ học tập trực quan.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Node.js-18.x-green?style=for-the-badge&logo=nodedotjs" />
  <img src="https://img.shields.io/badge/Express.js-4.x-lightgrey?style=for-the-badge&logo=express" />
  <img src="https://img.shields.io/badge/MySQL-8.0-blue?style=for-the-badge&logo=mysql" />
  <img src="https://img.shields.io/badge/Android-Native-green?style=for-the-badge&logo=android" />
  <img src="https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge" />
</p>

---

## 🌟 Tính Năng Nổi Bật

### 🔐 1. Xác thực & Quản lý tài khoản (Authentication)
- **Đăng ký / Đăng nhập:** Bảo mật mật khẩu bằng `bcryptjs`, quản lý phiên đăng nhập bằng `JWT`.
- **Đăng nhập Google:** Tích hợp `Google OAuth2` tiện lợi.
- **Xác thực OTP qua Email:** Gửi mã xác nhận qua Email (`Nodemailer`) cho tính năng đăng ký và khôi phục mật khẩu.
- **Chỉnh sửa hồ sơ:** Cập nhật tên, mục tiêu học tập (IELTS/TOEIC, Giao tiếp,...), và trình độ hiện tại.

### 🧠 2. Học Từ Vựng với Thuật toán SM-2 (Spaced Repetition)
- **Flashcard & Ôn tập:** Áp dụng **Thuật toán SM-2** để tự động tính toán khoảng thời gian lặp lại bài học dựa trên đánh giá độ khó (0 - 5) của người dùng.
- **Bộ từ vựng (Word Sets):** 
  - Hệ thống từ vựng mặc định được phân loại theo chủ đề (Data từ file CSV).
  - Cho phép người dùng tự tạo, sửa, xóa bộ từ vựng cá nhân hóa.

### 📖 3. Học Ngữ Pháp & Làm Bài Tập Trắc Nghiệm (Grammar)
- **Danh sách bài học:** Cung cấp lý thuyết ngữ pháp chi tiết (Công thức, Giải thích, Ví dụ, Lỗi sai thường gặp).
- **Trắc nghiệm ngữ pháp:** Tạo bài tập ngắt đợt ngẫu nhiên (`ORDER BY RAND()`) từ cơ sở dữ liệu.
- **Lưu điểm số:** Theo dõi bài làm có điểm số cao nhất của người dùng.

### 📊 4. Theo Dõi Tiến Độ Học Tập (Progress Analytics)
- **Chuỗi học tập (Streak):** Tính toán số ngày học liên tiếp chuẩn xác theo múi giờ.
- **Thống kê chi tiết:**
  - Tổng số từ đã học / Số từ cần ôn tập trong ngày.
  - Tỷ lệ chính xác trong 7 ngày gần nhất (Retention Rate / Accuracy).
  - Biểu đồ thời gian học (phút) và lịch sử học tập theo từng ngày.

### ⚙️ 5. Cài Đặt & Đa Ngôn Ngữ (Settings & i18n)
- **Đa ngôn ngữ:** Hỗ trợ hoàn chỉnh **Tiếng Việt 🇻🇳** và **Tiếng Anh 🇺🇸**.
- **Cấu hình máy chủ (Server Settings):** Cho phép thay đổi URL API ngay trong ứng dụng (thuận tiện khi test trên Emulator hoặc thiết bị thật).
- **Thông báo nhắc nhở:** Tùy chỉnh hẹn giờ nhắc học bài hàng ngày, nhắc ôn tập từ vựng/ngữ pháp.

---

## 🛠️ Công Nghệ Sử Dụng (Tech Stack)

### Backend
- **Core:** Node.js, Express.js
- **Database:** MySQL (Sử dụng Connection Pool `mysql2/promise`)
- **Authentication:** JSON Web Token (JWT), bcryptjs, Google Auth Library
- **Email Service:** Nodemailer (Gửi OTP HTML Template)
- **Utilities:** `csv-parser` (Seeding dữ liệu từ CSV)

### Android App
- **Language/Platform:** Native Android (Java/Kotlin)
- **UI:** XML Layouts, Material Design Components, Custom Vector Drawables
- **Internationalization (i18n):** `values-en/strings.xml`, `values-vi/strings.xml`

---

## 📂 Cấu Trúc Dự Án (Project Structure)

```text
├── EL/
│   ├── backend/                      # Node.js Express API Server
│   │   ├── config/                   # Kết nối CSDL MySQL (db.js, schema.sql)
│   │   ├── controllers/              # Xử lý logic nghiệp vụ
│   │   │   ├── authController.js
│   │   │   ├── grammarController.js
│   │   │   ├── progressController.js
│   │   │   ├── userController.js
│   │   │   └── vocabularyController.js
│   │   ├── data/                     # Dữ liệu mẫu (grammar-content.json, CSVs)
│   │   ├── middleware/               # Middleware xác thực JWT (auth.js)
│   │   ├── routes/                   # API Endpoints Route definition
│   │   ├── scripts/                  # Script khởi tạo CSDL & seed dữ liệu
│   │   │   ├── db-create.js
│   │   │   ├── db-setup.js
│   │   │   ├── seed.js
│   │   │   └── seed-grammar.js
│   │   ├── utils/                    # Email service & OTP Helper
│   │   └── index.js / server.js
│   │
│   └── app/                          # Native Android Project
│       └── res/
│           ├── drawable/             # Vector icons (Google, Launchers,...)
│           ├── values/               # Color, themes
│           ├── values-en/            # Ngôn ngữ Tiếng Anh
│           └── values-vi/            # Ngôn ngữ Tiếng Việt
