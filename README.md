# PC Master – Hệ thống Thương mại Điện tử Linh kiện PC

Ứng dụng web Full-Stack thương mại điện tử chuyên doanh linh kiện máy tính (CPU, VGA, RAM, Mainboard, SSD) với đầy đủ phân hệ Khách hàng, Giỏ hàng, Theo dõi vận đơn, Hỗ trợ trực tuyến (Live Chat) và Trang quản trị (Admin Dashboard).

---

## Tính năng chính

1. **Phân hệ Khách hàng & Mua sắm (`UserStore`, `ProductsPage`, `ProductDetail`):**
   - Tìm kiếm sản phẩm theo từ khóa, lọc đa tiêu chí (danh mục, khoảng giá), sắp xếp và phân trang động.
   - Quản lý giỏ hàng (`CartDrawer`) đồng bộ với cơ sở dữ liệu MySQL, tự động kiểm tra tồn kho thực tế.
   - Đặt hàng với cơ chế khóa dòng (`SELECT ... FOR UPDATE`) trong MySQL Transaction giúp chống xung đột tồn kho khi nhiều người mua cùng lúc.
   - Theo dõi tiến trình đơn hàng trực quan (`OrderHistory` & Timeline vận đơn tự động sinh mã tracking).
2. **Xác thực, Phân quyền & Hồ sơ (`AuthModal`, `ProfilePage`):**
   - Đăng ký, đăng nhập và phân quyền RBAC (`user` / `admin`) sử dụng **JWT** và mã hóa mật khẩu **Bcrypt**.
   - Tải lên và tự động nén ảnh đại diện (`800x800`, JPEG 80%) cũng như ảnh sản phẩm (`1200x1200`, JPEG 85%) phía server bằng **Multer** và **Sharp**.
3. **Trang Quản trị & Phân tích Doanh thu (`AdminDashboard`):**
   - Biểu đồ thống kê doanh thu theo thời gian, phễu trạng thái đơn hàng (Order Funnel), Top sản phẩm/danh mục bán chạy và cảnh báo hàng sắp hết kho (`Recharts`).
   - Nhận thông báo đơn hàng mới theo thời gian thực qua **Server-Sent Events (SSE)** (`/api/admin/orders/stream`).
   - Quản lý toàn diện (CRUD) sản phẩm, danh mục, đơn hàng và người dùng.
4. **Hỗ trợ Trực tuyến (`ChatWidget`):**
   - Hệ thống nhắn tin hỗ trợ trực tiếp giữa Khách hàng và Admin kèm bộ đếm tin nhắn chưa đọc.

---

## Công nghệ sử dụng

- **Frontend:** React 19, TypeScript, Tailwind CSS 4, Motion (Framer Motion), Recharts, Lucide Icons, Vite 6
- **Backend:** Node.js, Express.js (32 RESTful API & SSE endpoints), Multer, Sharp, JWT, Bcryptjs
- **Cơ sở dữ liệu:** MySQL 8.0+ (9 bảng quan hệ, 13 B-Tree indexes tối ưu hóa truy vấn)

---

## Hướng dẫn cài đặt & Chạy dự án

### 1. Yêu cầu hệ thống
- **Node.js** >= 18
- **MySQL** >= 8.0

### 2. Clone dự án & Cài đặt thư viện
```bash
git clone https://github.com/thinhdang1104/PCshop.git
cd PCshop
npm install
```

### 3. Cấu hình biến môi trường
Copy file `.env.example` thành `.env.local` và cập nhật thông tin kết nối MySQL:
```bash
cp .env.example .env.local
```
Nội dung file `.env.local`:
```env
DB_HOST=localhost
DB_USER=root
DB_PASSWORD=mat_khau_mysql_cua_ban
DB_NAME=pcmaster
JWT_SECRET=mot_chuoi_bi_mat_rat_dai
ADMIN_EMAIL=admin@pcmaster.local
ADMIN_PASSWORD=mat_khau_admin_it_nhat_8_ky_tu
```

### 4. Khởi chạy ứng dụng
```bash
npm run dev
```
Server và giao diện web sẽ chạy tại: **http://localhost:3000** (Database, các bảng, index và dữ liệu mẫu sẽ tự động được khởi tạo trong lần chạy đầu tiên).
