# 🚀 Hướng dẫn Deploy lên GitHub + Render (Miễn phí)

---

## ⚡ BƯỚC 1: Cài đặt Git (nếu chưa có)

1. Tải Git tại: https://git-scm.com/download/win
2. Cài đặt (nhấn Next liên tục, giữ mặc định)
3. Mở **Command Prompt** hoặc **PowerShell**, gõ kiểm tra:
```
git --version
```
Nếu hiển thị version (ví dụ `git version 2.45.0`) là OK.

---

## ⚡ BƯỚC 2: Tạo tài khoản GitHub

1. Truy cập: https://github.com
2. Click **"Sign up"** → Điền email, password, username
3. Verify email
4. Đăng nhập GitHub

---

## ⚡ BƯỚC 3: Tạo Repository trên GitHub

1. Đăng nhập GitHub → Click dấu **"+"** góc trên phải → **"New repository"**
2. Điền:
   - **Repository name:** `asean-scholarship-prep`
   - **Description:** `ASEAN Scholarship Interview Preparation App`
   - **Chọn:** Public
   - **KHÔNG tick** "Add a README file" (vì mình đã có rồi)
3. Click **"Create repository"**
4. GitHub sẽ hiện trang hướng dẫn → GIỮ TRANG NÀY MỞ

---

## ⚡ BƯỚC 4: Đẩy code lên GitHub

Mở **PowerShell** hoặc **Terminal** trong thư mục project:

```powershell
# Di chuyển đến thư mục project
cd D:\Kiro\Schoolar

# Cho phép chạy script (nếu bị lỗi)
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass

# Khởi tạo Git repo
git init

# Thêm tất cả files
git add .

# Tạo commit đầu tiên
git commit -m "Initial commit: ASEAN Scholarship Interview Prep App"

# Đổi branch thành main
git branch -M main

# Kết nối với GitHub (THAY your-username bằng username GitHub của bạn)
git remote add origin https://github.com/your-username/asean-scholarship-prep.git

# Đẩy code lên
git push -u origin main
```

**Lưu ý:** Lần đầu push, Git sẽ hỏi đăng nhập GitHub:
- Nếu hiện cửa sổ đăng nhập → đăng nhập bình thường
- Nếu hỏi password trong terminal → dùng **Personal Access Token** (không dùng password):
  1. GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)
  2. Generate new token → tick "repo" → Copy token
  3. Dùng token này thay cho password

**Sau khi push xong:** Vào GitHub repo → thấy code hiện lên là OK! ✅

---

## ⚡ BƯỚC 5: Tạo tài khoản Render

1. Truy cập: https://render.com
2. Click **"Get Started for Free"**
3. Chọn **"GitHub"** để đăng ký (dễ nhất - liên kết luôn)
4. Authorize Render truy cập GitHub

---

## ⚡ BƯỚC 6: Deploy lên Render

### Cách A: Web Service (Khuyên dùng)

1. Đăng nhập https://dashboard.render.com
2. Click **"New +"** (nút xanh, góc trên) → Chọn **"Web Service"**
3. Chọn **"Build and deploy from a Git repository"** → Click **"Next"**
4. Tìm repo **asean-scholarship-prep** → Click **"Connect"**
5. Điền cấu hình:

| Mục | Giá trị |
|-----|---------|
| **Name** | `asean-scholarship-prep` |
| **Region** | `Singapore (Southeast Asia)` |
| **Branch** | `main` |
| **Runtime** | `Node` |
| **Build Command** | `npm install` |
| **Start Command** | `npm start` |
| **Instance Type** | `Free` ← QUAN TRỌNG: chọn cái miễn phí! |

6. Click **"Create Web Service"**
7. Đợi 2-3 phút, Render sẽ:
   - Clone code từ GitHub
   - Chạy `npm install`
   - Khởi động `npm start`
8. Khi thấy **"Live"** (xanh lá) → DONE! 🎉

### Cách B: Static Site (Đơn giản hơn, không cần server)

1. Dashboard → **"New +"** → **"Static Site"**
2. Connect repo **asean-scholarship-prep**
3. Settings:
   - **Name:** `asean-scholarship-prep`
   - **Branch:** `main`
   - **Build Command:** (để trống - KHÔNG điền gì)
   - **Publish Directory:** `public`
4. Click **"Create Static Site"**
5. Đợi 1-2 phút → DONE! 🎉

---

## ⚡ BƯỚC 7: Truy cập App

Sau khi deploy thành công:
- **URL của bạn:** `https://asean-scholarship-prep.onrender.com`
- Mở link trên điện thoại hoặc máy tính đều được!
- Chia sẻ link cho bạn bè cùng ôn tập!

---

## 🔄 Cập nhật App (khi sửa code)

Mỗi khi bạn sửa `app.html` hoặc bất kỳ file nào:

```powershell
# Copy app.html mới sang public
Copy-Item "app.html" "public/index.html" -Force

# Add và commit thay đổi
git add .
git commit -m "Update: mô tả ngắn thay đổi"

# Push lên GitHub
git push
```

Render sẽ **tự động re-deploy** trong 2-3 phút! Không cần làm gì thêm.

---

## 📋 Cấu trúc Project

```
D:\Kiro\Schoolar\
├── public/
│   └── index.html          ← App chạy trên web (copy từ app.html)
├── node_modules/           ← Packages (tự tạo khi npm install)
├── .gitignore              ← Bỏ qua node_modules khi push
├── app.html                ← Source code gốc
├── server.js               ← Express web server
├── package.json            ← Cấu hình project + dependencies
├── render.yaml             ← Cấu hình Render (tự động)
├── README.md               ← Giới thiệu project
└── DEPLOY-RENDER.md        ← Hướng dẫn này
```

---

## ⚠️ Lưu ý về Free Tier Render

| Đặc điểm | Chi tiết |
|-----------|----------|
| 💰 Chi phí | **MIỄN PHÍ** hoàn toàn |
| 🔒 HTTPS | Tự động (an toàn) |
| 🌐 Custom domain | Hỗ trợ (nếu có domain riêng) |
| 😴 Sleep mode | App "ngủ" sau 15 phút không dùng |
| ⏰ Wake up | Mất ~30 giây để "thức" lại khi có người truy cập |
| 📊 Giới hạn | 750 giờ/tháng (đủ chạy 24/7) |

### Giữ app luôn "thức" (tùy chọn):
1. Vào https://uptimerobot.com (miễn phí)
2. Tạo tài khoản
3. Add New Monitor → HTTP(s) → Dán URL app của bạn
4. Set interval: 5 minutes
5. App sẽ không bao giờ ngủ!

---

## 🔧 Troubleshooting (Xử lý lỗi)

| Lỗi | Nguyên nhân | Cách sửa |
|------|-------------|----------|
| `git push` bị rejected | Repo trên GitHub không trống | Dùng `git push -u origin main --force` lần đầu |
| `npm install` lỗi script | PowerShell chặn script | Chạy `Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass` |
| Deploy fail trên Render | Build lỗi | Vào Render Dashboard → Logs → Đọc error message |
| App trắng trên Render | Thiếu public/index.html | Chạy `Copy-Item "app.html" "public/index.html" -Force` rồi push lại |
| Hình không hiện | Mất internet hoặc Unsplash down | Hình load từ internet, cần có mạng |
| Push lên GitHub lỗi auth | Token hết hạn | Tạo Personal Access Token mới |

---

## 📱 Mở app trên điện thoại

Sau khi deploy xong, chỉ cần:
1. Mở trình duyệt trên điện thoại (Chrome, Safari)
2. Gõ URL: `https://asean-scholarship-prep.onrender.com`
3. Thêm vào Home Screen để dùng như app:
   - **iPhone:** Share → Add to Home Screen
   - **Android:** Menu (3 chấm) → Add to Home Screen

---

Chúc bạn deploy thành công và PASS phỏng vấn ASEAN Scholarship! 🇻🇳✈️🇸🇬
