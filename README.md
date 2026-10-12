# STEM–Toán — Website bán học liệu trung học

Bộ mã HTML/CSS/JavaScript thuần, giao diện tiếng Việt, không cần cài thư viện hay bước build. Có thể đưa lên GitHub và dùng hosting tĩnh hỗ trợ HTTPS.

## 1. Sử dụng nhanh

1. Giải nén và đưa **các tệp bên trong thư mục stem-toan** vào thư mục gốc repository của bạn.
2. Mở `index.html` để xem trực tiếp. Hoặc chạy `python3 -m http.server 8000` trong thư mục rồi truy cập `http://localhost:8000`.
3. Bật GitHub Pages cho repository và chọn nguồn là nhánh chứa mã, thư mục gốc. Các đường dẫn tài nguyên là tương đối, phù hợp cả website đặt dưới tên repository.
4. Mở website từ địa chỉ hosting cung cấp.

## 2. Những gì đã có

- Giao diện học thuật màu xanh lá, nền sáng, thích ứng điện thoại và máy tính.
- Kho học liệu THCS/THPT; kế hoạch bài dạy và bản thiết kế STEM.
- Tìm kiếm không phân biệt dấu tiếng Việt; lọc cấp học, loại tài liệu; sắp xếp giá.
- Xem trước tối đa hai ảnh trang mẫu.
- Giỏ hàng lưu trên trình duyệt, mỗi tài liệu một bản, có xóa và tính tổng.
- Nhập tên, email; hiển thị QR của bạn; sinh mã tham chiếu và hướng dẫn chuyển khoản.
- Sao chép hoặc tải thông tin đơn; mở ứng dụng email với nội dung đơn soạn sẵn.
- Công cụ `editor.html` để sửa dữ liệu và xuất `content.js` mới.

**Đây là cửa hàng tĩnh với giao hàng thủ công.** Không có máy chủ lưu đơn, đăng nhập quản trị, kiểm tra ngân hàng, tự gửi email hoặc tự cấp quyền tải PDF. Khách phải thực sự gửi email; mở ứng dụng email không có nghĩa đơn đã được gửi. Người bán kiểm tra giao dịch thực tế trước khi gửi tài liệu. Không dùng nội dung đơn do khách gửi làm bằng chứng đã thanh toán.

## 3. Cập nhật QR sau

Hiện `qrImage`, `email` và thông tin ngân hàng để trống. Không có QR giả. Thanh toán chỉ mở khi có đường dẫn QR và email hợp lệ.

1. Đặt ảnh QR thật vào `assets/payment-qr.png`.
2. Trong `content.js`, cập nhật phần `shop`:

```javascript
email: "email-cua-ban@example.com",
qrImage: "assets/payment-qr.png",
bank: "Tên ngân hàng của bạn",
accountNumber: "Số tài khoản của bạn",
accountName: "TÊN CHỦ TÀI KHOẢN"
```

Thay toàn bộ giá trị ví dụ bằng thông tin thật. Kiểm tra QR trên điện thoại trước khi mở bán. Nên dùng QR nhận tiền không cố định số tiền/nội dung: khách nhập tổng tiền và mã tham chiếu hiển thị trên web. Ảnh QR tĩnh không tự thay đổi theo giỏ hàng.

## 4. Cập nhật nội dung và sản phẩm

Cách dễ: mở `editor.html` → sửa JSON → “Kiểm tra & tải content.js” → thay tệp cùng tên trên GitHub. Công cụ chỉ tạo tệp trên máy, không tự lưu thay đổi vào repository. Người khác mở công cụ cũng không thể sửa website của bạn; chỉ người có quyền ghi repository mới cập nhật được mã.

Hoặc chỉnh `content.js` trực tiếp. Sáu tài liệu, số trang và mức giá ban đầu là dữ liệu minh họa; thay bằng nội dung thực tế. Mặc định tất cả `available: false`, chưa thể thêm vào giỏ hoặc mua.

Mỗi sản phẩm gồm:

| Trường | Ý nghĩa |
| --- | --- |
| `id` | Mã duy nhất, chữ thường không dấu, số và dấu gạch ngang |
| `title`, `subtitle` | Tên và mô tả ngắn |
| `level` | `THCS` hoặc `THPT` |
| `grade` | Ví dụ `Lớp 8–9` |
| `kind` | `Kế hoạch bài dạy` hoặc `Bản thiết kế` |
| `price` | Số nguyên VNĐ, không viết dấu phân cách |
| `pages` | Số trang PDF đầy đủ |
| `symbol` | Ký hiệu trên bìa minh họa |
| `color` | `mint`, `sand`, `blue`, `pink` |
| `topic` | Chủ đề Toán |
| `previewImages` | Mảng tối đa 2 đường dẫn ảnh mẫu |
| `available` | `true` để mở bán, `false` để hiện Sắp phát hành |

Ví dụ sau khi có tài liệu thật:

```javascript
previewImages: ["assets/previews/cau-giay-1.jpg", "assets/previews/cau-giay-2.jpg"],
available: true
```

Nếu mở tệp trực tiếp và trình duyệt hạn chế lưu giỏ/sao chép, dùng máy chủ local hoặc website HTTPS. Công cụ biên tập yêu cầu ảnh mẫu trong assets; không dùng đường dẫn PDF làm ảnh mẫu.

## 5. Bảo vệ PDF và giao tài liệu

- Xuất riêng 1–2 trang đầu thành ảnh JPG/PNG/WebP; chỉ đăng những ảnh đó lên website.
- **Không đăng PDF đầy đủ lên repository, kể cả định dùng CSS hoặc JavaScript để che trang.** Ai truy cập đường dẫn công khai cũng có thể tải. `.gitignore` bỏ qua PDF để giảm đưa nhầm bằng Git, nhưng không ngăn upload thủ công qua giao diện GitHub.
- Ảnh xem trước là công khai và người xem vẫn có thể lưu ảnh. Có thể tự thêm watermark vào ảnh mẫu.
- Giữ PDF đầy đủ trên máy hoặc kho riêng có kiểm soát quyền truy cập. Sau khi kiểm tra tiền vào tài khoản, gửi tệp trực tiếp cho email khách hàng.
- Khách dùng mã đơn và số tiền khi chuyển khoản; mã này chỉ là tham chiếu được sinh ở trình duyệt, không phải bản ghi đơn hàng trên máy chủ. Khách nên tải thông tin đơn trước khi đóng hộp thoại. Giỏ được giữ lại sau khi mở email để tránh mất dữ liệu khi email chưa gửi.
- Muốn tự động cấp tải PDF sau thanh toán cần thêm backend, lưu đơn và giá phía server, lưu trữ riêng tư, xác thực giao dịch qua nhà cung cấp và liên kết tải có thời hạn. GitHub Pages một mình không thực hiện các bước đó.

## 6. Quy trình kiểm tra trước khi bán

1. Cập nhật tên, giá, mô tả, số trang thật; tải 1–2 ảnh mẫu cho từng sản phẩm.
2. Thêm email nhận đơn, QR và tài khoản ngân hàng thật.
3. Bật `available: true` cho sản phẩm đã hoàn thiện.
4. Kiểm tra tìm kiếm, bộ lọc, thêm/xóa giỏ, tổng tiền và hiển thị trên điện thoại.
5. Tạo một đơn thử; kiểm tra người nhận QR và email soạn sẵn; đối chiếu giao dịch bằng ngân hàng rồi thử gửi tài liệu.
6. Bổ sung điều khoản sử dụng tài liệu, chính sách xử lý đơn/hoàn tiền và thông tin người bán theo hoạt động thực tế của bạn.

## Cấu trúc

- `index.html`: bố cục cửa hàng.
- `styles.css`: giao diện và responsive.
- `content.js`: dữ liệu cửa hàng/sản phẩm để bạn sửa.
- `app.js`: tìm kiếm, giỏ hàng, xem trước, chuyển khoản và email đơn hàng.
- `editor.html`, `editor.js`: công cụ xuất cấu hình nội dung.
- `assets/previews/`: ảnh 1–2 trang mẫu.
- `assets/payment-qr.png`: tự thêm ảnh QR thật sau.

Không sử dụng dịch vụ phân tích hoặc gửi dữ liệu khách hàng tới máy chủ trong mã nguồn này. Giỏ hàng chỉ lưu ID sản phẩm trong localStorage; tên/email được dùng trong nội dung email và tệp đơn do khách chủ động tạo.
