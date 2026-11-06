# EcommerceLaptop

Nền tảng thương mại điện tử chuyên bán laptop. Dự án tách frontend Next.js khỏi backend ASP.NET Core và có các thành phần hạ tầng cho tìm kiếm, cache, giám sát và thanh toán.

## Thành phần

- `ecommerce-laptop-frontend/`: giao diện Next.js 16, React 19, TypeScript và Tailwind CSS.
- `src/EcommerceLaptop.API/`: API ASP.NET Core .NET 9; có Swagger khi chạy Development, SignalR, JWT/Identity, Hangfire, rate limiting, CSRF và logging.
- `src/EcommerceLaptop.Core/`: domain entities và các hợp đồng dịch vụ.
- `src/EcommerceLaptop.Infrastructure/`: truy cập dữ liệu, tích hợp dịch vụ và middleware.
- `tests/`: unit test và integration test.
- `monitoring/`: cấu hình Prometheus.

## Chức năng chính

- Danh mục, tìm kiếm và quản lý sản phẩm laptop.
- Tài khoản, phân quyền quản trị, giỏ hàng, đơn hàng, đánh giá và khuyến mãi.
- Tích hợp các luồng thanh toán; cấu hình khóa phải đặt trong biến môi trường hoặc cấu hình cục bộ.
- Chat thời gian thực qua SignalR, dashboard tác vụ nền qua Hangfire và endpoint metrics Prometheus tại `/metrics`.
- Hỗ trợ Redis, Qdrant, Typesense, Prometheus, Grafana và Loki bằng Docker Compose.

## Yêu cầu

- .NET SDK 9.
- Node.js LTS và npm/pnpm.
- Docker Desktop (tùy chọn, cho các dịch vụ hạ tầng).
- SQL Server/LocalDB cho cơ sở dữ liệu mặc định.

## Chạy cục bộ

1. Tạo cấu hình riêng từ `src/EcommerceLaptop.API/appsettings.example.json`; không commit khóa API, mật khẩu hoặc cấu hình production.
2. Khởi động dịch vụ phụ trợ nếu cần:

   ```powershell
   docker compose up -d
   ```

3. Chạy API:

   ```powershell
   dotnet run --project src/EcommerceLaptop.API
   ```

4. Trong cửa sổ terminal khác, chạy frontend:

   ```powershell
   cd ecommerce-laptop-frontend
   npm install
   npm run dev
   ```

5. Chạy kiểm thử backend bằng `dotnet test EcommerceLaptop.sln`. Frontend có các lệnh `npm run lint`, `npm test` và `npm run test:e2e`.

