
# 🛒 BÁO GIÁ CHI TIẾT TỪNG CHỨC NĂNG - HỆ THỐNG BÁN HÀNG ONLINE

---

## 📋 **TỔNG QUAN Dự ÁN**

**Hệ thống bán hàng online hoàn chỉnh** bao gồm:
- **Website bán hàng** cho khách mua
- **Panel quản trị** cho admin/seller quản lý  
- **Ứng dụng di động** cho khách hàng và shipper
- **Hệ thống thanh toán** VNPay tích hợp
- **6 loại tài khoản** với quyền khác nhau

**Tổng thời gian**: 2.5 tháng (61 ngày coding + 14 ngày testing & fix bug)

**📊 Quy Chuẩn Estimate:**
- **1 ngày làm việc** = 8 giờ coding hiệu quả
- **1 tuần** = 7 ngày làm việc (56 giờ) - không nghỉ
- **Tổng thời gian**: 75 ngày = 600 giờ làm việc = ~10.7 tuần

---

## 🏪 **PHẦN 1: WEBSITE BÁN HÀNG (KHÁCH HÀNG)**

### 🏠 **1.1 TRANG CHỦ** - *5 ngày*

| Chức năng | Mô tả chi tiết | Ví dụ thực tế | Estimate |
|-----------|---------------|---------------|----------|
| **Header Navigation** | Menu điều hướng chính, logo, tìm kiếm, giỏ hàng | Giống Shopee: Logo, tìm kiếm, giỏ hàng, đăng nhập | 0.8 ngày |
| **Banner Slider** | Slider ảnh quảng cáo có thể thay đổi | Ảnh khuyến mãi, sản phẩm mới tự động chuyển | 0.8 ngày |
| **Danh mục sản phẩm** | Hiển thị các danh mục chính với icon | Thực phẩm, gia dụng, điện tử... có ảnh minh họa | 0.8 ngày |
| **Sản phẩm nổi bật** | Hiển thị sản phẩm hot, mới, giảm giá | Sản phẩm có nhãn "Hot", "Sale", "New" | 0.8 ngày |
| **Flash Sale** | Khung giờ vàng với đếm ngược | Giống Tiki: Đồng hồ đếm ngược, % giảm giá lớn | 0.8 ngày |
| **Footer** | Thông tin liên hệ, chính sách, mạng xã hội | Địa chỉ, SĐT, link Facebook, Zalo | 0.5 ngày |
| **Responsive Design** | Tự động co giãn trên mobile, tablet | Xem đẹp trên mọi thiết bị | 0.5 ngày |

### 🔍 **1.2 TÌM KIẾM & DANH MỤC** - *4 ngày*

| Chức năng | Mô tả chi tiết | Ví dụ thực tế | Estimate |
|-----------|---------------|---------------|----------|
| **Tìm kiếm thông minh** | Gõ tên sản phẩm, hiện gợi ý tự động | Gõ "áo" → hiện "áo sơ mi", "áo thun"... | 0.8 ngày |
| **Bộ lọc sản phẩm** | Lọc theo giá, thương hiệu, đánh giá | Slider giá 100k-500k, tick chọn thương hiệu | 0.8 ngày |
| **Sắp xếp sản phẩm** | Sắp xếp theo giá, bán chạy, đánh giá | Dropdown: "Giá thấp → cao", "Bán chạy nhất" | 0.5 ngày |
| **Hiển thị dạng lưới** | Sản phẩm hiện dạng ô vuông có ảnh, giá | Giống Lazada: 4 sản phẩm/hàng trên desktop | 0.6 ngày |
| **Phân trang** | Chuyển trang khi có nhiều sản phẩm | "Trang 1, 2, 3..." hoặc "Load more" | 0.5 ngày |
| **Breadcrumb** | Đường dẫn: Trang chủ > Danh mục > Sản phẩm | Để biết đang ở đâu, click để quay lại | 0.3 ngày |
| **Số lượng kết quả** | Hiển thị "Tìm thấy 156 sản phẩm" | Để khách biết có bao nhiêu sản phẩm | 0.5 ngày |

### 📦 **1.3 CHI TIẾT SẢN PHẨM** - *4 ngày*

| Chức năng | Mô tả chi tiết | Ví dụ thực tế | Estimate |
|-----------|---------------|---------------|----------|
| **Gallery ảnh sản phẩm** | Nhiều ảnh, zoom, xem fullscreen | Click để zoom, slide để xem ảnh khác | 0.8 ngày |
| **Thông tin cơ bản** | Tên, giá, mô tả, thương hiệu | Tên rõ ràng, giá gốc/giảm, % sale | 0.5 ngày |
| **Chọn phiên bản** | Size, màu sắc, số lượng | Size: S,M,L - Màu: Đỏ, Xanh - SL: +/- | 0.6 ngày |
| **Đánh giá khách hàng** | Sao, bình luận, ảnh từ người mua | "4.5⭐ (123 đánh giá)" + ảnh thật từ khách | 0.6 ngày |
| **Sản phẩm liên quan** | Gợi ý sản phẩm tương tự | "Khách hàng cũng xem", "Mua cùng" | 0.5 ngày |
| **Thêm vào giỏ hàng** | Nút to, rõ ràng, thông báo thành công | Nút cam to "THÊM VÀO GIỎ" + popup xác nhận | 0.5 ngày |
| **Mua ngay** | Bỏ qua giỏ hàng, chuyển luôn thanh toán | Nút đỏ "MUA NGAY" → trang checkout | 0.5 ngày |

### 🛒 **1.4 GIỎ HÀNG & THANH TOÁN** - *5 ngày*

| Chức năng | Mô tả chi tiết | Ví dụ thực tế | Estimate |
|-----------|---------------|---------------|----------|
| **Xem giỏ hàng** | Danh sách sản phẩm đã chọn | Ảnh, tên, giá, số lượng, xóa khỏi giỏ | 0.8 ngày |
| **Sửa giỏ hàng** | Thay đổi số lượng, xóa sản phẩm | Nút +/- số lượng, nút thùng rác để xóa | 0.5 ngày |
| **Nhập mã giảm giá** | Ô nhập coupon, tính toán lại giá | Nhập "SALE20" → giảm 20%, hiện tiết kiệm | 0.6 ngày |
| **Chọn địa chỉ giao hàng** | Danh sách địa chỉ đã lưu hoặc nhập mới | Chọn "Nhà riêng" hoặc "Thêm địa chỉ mới" | 0.6 ngày |
| **Chọn hình thức vận chuyển** | Giao nhanh, giao tiêu chuẩn với phí khác nhau | "Giao nhanh 2h (+20k)", "Giao tiêu chuẩn (Free)" | 0.5 ngày |
| **Chọn thanh toán** | VNPay, chuyển khoản, COD | QR VNPay, chuyển khoản, "Thanh toán khi nhận" | 0.8 ngày |
| **Xác nhận đơn hàng** | Tóm tắt đơn, nút đặt hàng cuối cùng | Review lại tất cả, nút "ĐẶT HÀNG" lớn | 0.6 ngày |
| **Trang cảm ơn** | Thông báo đặt hàng thành công + mã đơn | "Cảm ơn! Mã đơn #DH001" + link theo dõi | 0.6 ngày |

### 👤 **1.5 TÀI KHOẢN KHÁCH HÀNG** - *2 ngày*

| Chức năng | Mô tả chi tiết | Ví dụ thực tế | Estimate |
|-----------|---------------|---------------|----------|
| **Đăng ký/Đăng nhập** | Form đơn giản, login Facebook/Google | Email + mật khẩu hoặc nút "Login với Google" | 0.3 ngày |
| **Thông tin cá nhân** | Sửa tên, SĐT, email, avatar | Form edit profile + upload ảnh đại diện | 0.3 ngày |
| **Quản lý địa chỉ** | Thêm, sửa, xóa địa chỉ giao hàng | "Nhà riêng", "Công ty" với đầy đủ địa chỉ | 0.3 ngày |
| **Lịch sử đơn hàng** | Xem tất cả đơn đã mua | List đơn hàng: Mã, ngày, tổng tiền, trạng thái | 0.4 ngày |
| **Chi tiết đơn hàng** | Click vào đơn để xem chi tiết | Sản phẩm mua, địa chỉ giao, tracking | 0.3 ngày |
| **Theo dõi đơn hàng** | Trạng thái realtime của đơn | "Đang chuẩn bị" → "Đang giao" → "Đã giao" | 0.2 ngày |
| **Đánh giá sản phẩm** | Sau khi nhận hàng, rate sao + comment | "Chất lượng tốt 5⭐" + upload ảnh | 0.2 ngày |

---

## 🎛️ **PHẦN 2: HỆ THỐNG QUẢN TRỊ (ADMIN/SELLER)**

### 🏠 **2.1 DASHBOARD TỔNG QUAN** - *3 ngày*

| Chức năng | Mô tả chi tiết | Ví dụ thực tế | Estimate |
|-----------|---------------|---------------|----------|
| **Thống kê tổng quan** | Số liệu kinh doanh quan trọng | "Hôm nay: 50 đơn, 15tr doanh thu" | 0.8 ngày |
| **Biểu đồ doanh thu** | Biểu đồ theo ngày/tháng | Biểu đồ cột theo từng ngày trong tháng | 0.6 ngày |
| **Đơn hàng mới** | List đơn hàng cần xử lý | "5 đơn mới chờ xác nhận" + link nhanh | 0.5 ngày |
| **Sản phẩm sắp hết** | Cảnh báo sản phẩm ít hàng | "Áo thun trắng còn 3 cái" màu đỏ cảnh báo | 0.5 ngày |
| **Hoạt động gần đây** | Log các hành động mới | "9:30 - Đơn #123 đã giao thành công" | 0.3 ngày |
| **Shortcut nhanh** | Nút tắt đến chức năng hay dùng | "Thêm sản phẩm", "Xem đơn hàng", "Báo cáo" | 0.3 ngày |

### 📦 **2.2 QUẢN LÝ SẢN PHẨM** - *6 ngày*

| Chức năng | Mô tả chi tiết | Ví dụ thực tế | Estimate |
|-----------|---------------|---------------|----------|
| **Danh sách sản phẩm** | Bảng list tất cả sản phẩm | Bảng có ảnh, tên, giá, số lượng, trạng thái | 0.8 ngày |
| **Thêm sản phẩm mới** | Form nhập đầy đủ thông tin | Tên, mô tả, giá, ảnh, danh mục, thuộc tính | 1.5 ngày |
| **Sửa sản phẩm** | Edit thông tin sản phẩm có sẵn | Giống form thêm nhưng đã điền sẵn data | 0.5 ngày |
| **Upload ảnh sản phẩm** | Kéo thả nhiều ảnh, crop, resize | Kéo 5 ảnh vào, tự động resize phù hợp | 0.8 ngày |
| **Phiên bản sản phẩm** | Quản lý size, màu, giá khác nhau | Size S,M,L với giá và kho riêng biệt | 0.8 ngày |
| **Tồn kho** | Cập nhật số lượng hàng | Nhập số lượng nhập kho, xuất kho | 0.5 ngày |
| **Trạng thái sản phẩm** | Bật/tắt hiển thị, nổi bật | "Đang bán", "Hết hàng", "Nổi bật trang chủ" | 0.5 ngày |
| **Import/Export** | Nhập Excel hàng loạt | Upload file Excel với 1000 sản phẩm cùng lúc | 0.6 ngày |

### 🛒 **2.3 QUẢN LÝ ĐƠN HÀNG** - *5 ngày*

| Chức năng | Mô tả chi tiết | Ví dụ thực tế | Estimate |
|-----------|---------------|---------------|----------|
| **Danh sách đơn hàng** | Bảng tất cả đơn hàng | Mã đơn, khách hàng, tổng tiền, trạng thái, ngày | 0.5 ngày |
| **Chi tiết đơn hàng** | Xem đầy đủ thông tin đơn | Sản phẩm, địa chỉ, SĐT, ghi chú đặc biệt | 0.4 ngày |
| **Xử lý đơn hàng** | Chuyển trạng thái đơn | "Chờ xác nhận" → "Đang chuẩn bị" → "Đang giao" | 0.5 ngày |
| **In hóa đơn** | Xuất PDF hóa đơn | Click "In" → file PDF có thông tin đầy đủ | 0.3 ngày |
| **Phân công shipper** | Assign đơn cho shipper cụ thể | Chọn "Anh Nam" giao đơn này | 0.3 ngày |
| **Ghi chú nội bộ** | Note riêng cho team | "Khách yêu cầu giao trước 5h chiều" | 0.2 ngày |
| **Hoàn trả/Hủy đơn** | Xử lý đơn hủy, hoàn tiền | Chọn lý do hủy, hoàn tiền tự động | 0.4 ngày |
| **Lọc và tìm kiếm** | Tìm đơn theo nhiều tiêu chí | Tìm theo mã đơn, tên khách, ngày, trạng thái | 0.4 ngày |
| **Xuất báo cáo đơn** | Export Excel tất cả đơn | File Excel có tất cả đơn trong tháng | 0.5 ngày |

### 👥 **2.4 QUẢN LÝ KHÁCH HÀNG** - *4 ngày*

| Chức năng | Mô tả chi tiết | Ví dụ thực tế | Estimate |
|-----------|---------------|---------------|----------|
| **Danh sách khách hàng** | Bảng tất cả khách đã đăng ký | Tên, email, SĐT, ngày đăng ký, tổng mua | 0.6 ngày |
| **Thông tin chi tiết khách** | Profile đầy đủ của 1 khách | Lịch sử mua, địa chỉ, sở thích, tần suất mua | 0.8 ngày |
| **Lịch sử mua hàng** | Tất cả đơn của khách này | 20 đơn hàng từ 2023 đến nay của anh A | 0.5 ngày |
| **Phân nhóm khách hàng** | Gắn nhãn VIP, thường, mới | "VIP" (mua >5tr), "Thường", "Khách mới" | 0.6 ngày |
| **Gửi email marketing** | Gửi email khuyến mãi | Chọn nhóm "VIP" → gửi email sale 20% | 0.8 ngày |
| **Blacklist** | Chặn khách hàng xấu | Khách hay hủy đơn, chặn không cho đặt | 0.3 ngày |
| **Xuất danh sách** | Export Excel khách hàng | File Excel có email để gửi marketing | 0.4 ngày |

### 🚚 **2.5 QUẢN LÝ VẬN CHUYỂN** - *3 ngày*

| Chức năng | Mô tả chi tiết | Ví dụ thực tế | Estimate |
|-----------|---------------|---------------|----------|
| **Danh sách shipper** | Quản lý nhân viên giao hàng | Tên, SĐT, khu vực phụ trách, trạng thái | 0.5 ngày |
| **Phân ca làm việc** | Lịch làm việc của shipper | "Anh Nam: Ca sáng Quận 1", "Anh Tú: Ca chiều Q2" | 0.6 ngày |
| **Theo dõi giao hàng** | Xem shipper đang giao đâu | Map hiện vị trí shipper + đơn đang giao | 0.8 ngày |
| **Báo cáo hiệu suất** | Thống kê hiệu suất giao hàng | "Anh Nam: 95% giao thành công, trung bình 25 đơn/ngày" | 0.6 ngày |
| **Cài đặt phí ship** | Cấu hình giá cước theo khu vực | "Nội thành: 20k, Ngoại thành: 30k" | 0.3 ngày |
| **Xử lý khiếu nại** | Đơn giao thất bại | "Khách không có nhà" → đặt lịch giao lại | 0.2 ngày |

### 💰 **2.6 QUẢN LÝ TÀI CHÍNH** - *4 ngày*

| Chức năng | Mô tả chi tiết | Ví dụ thực tế | Estimate |
|-----------|---------------|---------------|----------|
| **Báo cáo doanh thu** | Biểu đồ thu chi theo thời gian | Biểu đồ cột doanh thu 12 tháng qua | 0.8 ngày |
| **Báo cáo bán hàng** | Sản phẩm bán chạy nhất | Top 10 sản phẩm, danh mục bán chạy | 0.6 ngày |
| **Quản lý giao dịch** | List tất cả giao dịch | Thu/chi, ngày, mô tả, số tiền, trạng thái | 0.6 ngày |
| **Thanh toán cho seller** | Trả tiền cho người bán | Tính % hoa hồng, trừ phí, chuyển khoản | 0.8 ngày |
| **Hóa đơn điện tử** | Xuất hóa đơn VAT | Tích hợp hóa đơn điện tử theo quy định | 0.6 ngày |
| **Báo cáo thuế** | Tổng hợp cho khai thuế | Doanh thu chịu thuế, VAT đầu vào/ra | 0.6 ngày |

### 🎯 **2.7 MARKETING & KHUYẾN MÃI** - *4 ngày*

| Chức năng | Mô tả chi tiết | Ví dụ thực tế | Estimate |
|-----------|---------------|---------------|----------|
| **Tạo mã giảm giá** | Coupon với điều kiện khác nhau | "SALE20": Giảm 20% đơn >500k, hạn đến 31/12 | 0.5 ngày |
| **Flash Sale** | Khuyến mãi có thời hạn | "Sale 50% trong 24h cho 100 sản phẩm đầu" | 0.6 ngày |
| **Banner quảng cáo** | Quản lý banner trang chủ | Upload ảnh banner, link đến sản phẩm | 0.3 ngày |

### ⚙️ **2.8 CÀI ĐẶT HỆ THỐNG** - *2 ngày*

| Chức năng | Mô tả chi tiết | Ví dụ thực tế | Estimate |
|-----------|---------------|---------------|----------|
| **Thông tin website** | Tên shop, logo, thông tin liên hệ | "Shop ABC", upload logo, địa chỉ, SĐT | 0.3 ngày |
| **Cài đặt thanh toán** | Cấu hình VNPay, chuyển khoản | Nhập merchant ID VNPay, STK ngân hàng | 0.4 ngày |
| **Cài đặt vận chuyển** | Phí ship, thời gian giao | "Miễn phí đơn >300k", "Giao trong 2-3 ngày" | 0.3 ngày |
| **Template email** | Mẫu email tự động | Email xác nhận đơn, email marketing | 0.3 ngày |
| **Phân quyền user** | Cấp quyền cho nhân viên | "Nhân viên A: Chỉ xem đơn hàng", "B: Full quyền" | 0.4 ngày |

---

## 🔧 **PHẦN 4: TÍCH HỢP & HỆ THỐNG**

### 💳 **4.1 TÍCH HỢP THANH TOÁN** - *3 ngày*

| Chức năng | Mô tả chi tiết | Ví dụ thực tế | Estimate |
|-----------|---------------|---------------|----------|
| **VNPay Gateway** | Thanh toán qua VNPay | QR code, thẻ ATM, Internet Banking | 2 ngày |
| **COD** | Thanh toán khi nhận hàng | Shipper thu tiền, báo cáo về hệ thống | 0.3 ngày |
| **Chuyển khoản** | Upload ảnh chuyển khoản | Khách chụp ảnh bill → admin xác nhận | 0.4 ngày |
| **Báo cáo giao dịch** | Reconciliation | Đối soát với VNPay, báo cáo chi tiết | 0.3 ngày |

### 📧 **4.2 HỆ THỐNG EMAIL & THÔNG BÁO** - *2 ngày*

| Chức năng | Mô tả chi tiết | Ví dụ thực tế | Estimate |
|-----------|---------------|---------------|----------|
| **Email tự động** | Auto send theo trigger | Đặt hàng → gửi email xác nhận tự động | 0.5 ngày |
| **Template email** | Mẫu email đẹp | Template responsive, logo, màu sắc brand | 0.4 ngày |

### 🔐 **4.3 BẢO MẬT & PHÂN QUYỀN** - *2.5 ngày*

| Chức năng | Mô tả chi tiết | Ví dụ thực tế | Estimate |
|-----------|---------------|---------------|----------|
| **Phân quyền chi tiết** | 6 loại user, quyền cụ thể | Admin: full quyền, Seller: chỉ sản phẩm mình | 2 ngày |

### 📊 **4.4 ANALYTICS & BÁO CÁO** - *3 ngày*

| Chức năng | Mô tả chi tiết | Ví dụ thực tế | Estimate |
|-----------|---------------|---------------|----------|
| **Báo cáo chi tiết** | Export Excel, PDF | Báo cáo doanh thu, sản phẩm, khách hàng | 1 ngày |
| **Customer journey** | Hành trình khách hàng | Từ visit → add cart → purchase | 2 ngày |

---

## 🧪 **PHẦN 5: TESTING & BẢO ĐẢM CHẤT LƯỢNG**

### 🔍 **5.1 TESTING TOÀN DIỆN** - *7 ngày*

| Loại Test | Mô tả chi tiết | Ví dụ thực tế | Estimate |
|-----------|---------------|---------------|----------|
| **Functional Testing** | Test từng chức năng hoạt động | Test đăng ký, đặt hàng, thanh toán... | 2 ngày |
| **Payment Testing** | Test tất cả hình thức thanh toán | VNPay sandbox, COD, chuyển khoản | 1 ngày |
| **Performance Testing** | Test tốc độ, tải cao | 1000 user cùng lúc, trang load <2s | 1 ngày |
| **Security Testing** | Test bảo mật | SQL injection, XSS, data validation | 1 ngày |
| **User Experience Testing** | Test với người dùng thật | 10 người thật sử dụng và feedback | 1 ngày |
| **Browser Testing** | Test trên nhiều trình duyệt | Chrome, Safari, Firefox, Edge | 0.5 ngày |

### 🐛 **5.2 BUG FIXING & OPTIMIZATION** - *6 ngày*

| Loại Công Việc | Mô tả chi tiết | Ví dụ thực tế | Estimate |
|----------------|---------------|---------------|----------|
| **Critical Bug Fix** | Sửa lỗi nghiêm trọng | Không thanh toán được, đơn hàng mất | 2 ngày |
| **UI/UX Polish** | Chỉnh sửa giao diện | Căn chỉnh button, màu sắc, font chữ | 1.5 ngày |
| **Performance Tuning** | Tối ưu tốc độ | Optimize database query, compress image | 1.5 ngày |
| **Code Cleanup** | Dọn dẹp code | Remove unused code, optimize structure | 0.5 ngày |
| **Documentation** | Viết tài liệu hướng dẫn | User manual, admin guide | 0.5 ngày |

---

## 📋 **TỔNG KẾT CHI TIẾT**

### 📊 **Bảng Tổng Hợp Theo Phần**

| Phần | Số Chức Năng | Thời Gian | % Tổng | Độ Phức Tạp |
|------|-------------|-----------|--------|-------------|
| **🏪 Website Khách Hàng** | 35 chức năng | 20 ngày | 27% | Trung bình |
| **🎛️ Hệ Thống Quản Trị** | 67 chức năng | 32 ngày | 43% | Cao |
| **🔧 Tích Hợp & Hệ Thống** | 17 chức năng | 9 ngày | 12% | Trung bình |
| **🧪 Testing & Fix Bug** | 15 hoạt động | 14 ngày | 18% | Cao |
| **📋 TỔNG CỘNG** | **134 items** | **75 ngày** | **100%** | **Mixed** |

### ⏰ **Timeline Chi Tiết (7 ngày/tuần)**

| Tuần | Ngày | Focus Area | Key Deliverables |
|------|------|------------|------------------|
| **W1** | 1-7 | Authentication & Foundation | User Auth, Database Setup |
| **W2** | 8-14 | Basic Framework & Admin Base | Admin Layout, Basic CRUD |
| **W3** | 15-21 | Admin Panel Core | Dashboard, Product Management |
| **W4** | 22-28 | Admin Orders & Users | Order Management, User Management |
| **W5** | 29-35 | Admin Advanced | Reports, Financial Management |
| **W6** | 36-42 | Admin Marketing | Marketing Tools, Settings |
| **W7** | 43-49 | Client Frontend Base | Homepage, Product Listing |
| **W8** | 50-56 | Client Shopping Flow | Product Details, Cart, Checkout |
| **W9** | 57-63 | Client User Features | User Account, Order History |
| **W10** | 64-70 | Integration & Testing | System Integration, Testing |
| **W11** | 71-75 | Bug Fix & Launch | Final Bug Fixes, Launch Prep |

---

## 🎯 **KẾT LUẬN**

**Hệ thống e-commerce hoàn chỉnh này sẽ cung cấp:**

✅ **134 chức năng chi tiết** từ cơ bản đến nâng cao
✅ **6 loại người dùng** với quyền hạn rõ ràng  
✅ **Tích hợp đầy đủ** thanh toán VNPay, email notifications
✅ **Testing & Bug fixing toàn diện** đảm bảo chất lượng cao

**Thời gian thực hiện**: 2.5 tháng (75 ngày liên tục = 11 tuần làm 7 ngày/tuần)
**Phạm vi**: Hệ thống web hoàn chỉnh
**Bảo hành**: 1 tháng miễn phí, hỗ trợ kỹ thuật

*Lưu ý: Timeline 11 tuần làm việc 7 ngày/tuần không nghỉ. Ưu tiên Auth & Admin trước (6 tuần), Client sau (3 tuần), Integration & Launch (2 tuần).*
