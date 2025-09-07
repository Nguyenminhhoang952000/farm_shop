# Hệ Thống Phân Quyền và Luồng Người Dùng cho Sàn Thương Mại Điện Tử

## Tổng Quan Dự Án
**Mục Tiêu Chính**: Xây dựng website bán hàng và ứng dụng di động toàn diện với giao diện hiện đại, bắt mắt và thân thiện với người dùng.

**Vấn Đề Cần Giải Quyết**: Cung cấp trải nghiệm mua sắm tiện lợi cho khách hàng không muốn ra ngoài do thời tiết, bận công việc hoặc các lý do khác.

**Đối Tượng Người Dùng**: Giới trẻ độ tuổi 18-40 và những người có nhu cầu sử dụng dịch vụ.

## Phạm Vi Hệ Thống
- **Giới Hạn Địa Lý**: Cấp tỉnh với chia nhỏ theo Phường/Xã
- **Khu Vực Bán Hàng**: Phạm vi bán hàng có giới hạn cho từng sản phẩm
- **Giao Diện Tham Khảo**: Đăng ký kiểu Shopee, hiển thị kiểu Homfam
- **Danh Mục Sản Phẩm**: Hàng thiết yếu gia dụng + món ăn đã nấu sẵn
- **Chiến Lược Đăng Ký**: Đăng ký ban đầu đơn giản với ít thông tin, yêu cầu bổ sung khi người dùng cần tính năng nâng cao

## Các Vai Trò
- **Super Admin (Admin Tổng)**: Quyền truy cập toàn hệ thống, quản lý tất cả người dùng, vai trò và phân quyền.
- **Admin (Người nhập hàng)**: Quản lý kho hàng, khách hàng, shipper và đơn hàng.
- **Người Bán/Chủ Cửa Hàng**: Quản lý cửa hàng riêng, sản phẩm và đơn hàng của mình, chuyên biệt cho các hoạt động quản lý đơn hàng.
- **Admin Shipper**: Quản lý các shipper, quản lý các đơn giao hàng được phân công, cập nhật trạng thái giao hàng, tải lên bằng chứng và báo cáo giao hàng.
- **Khách Hàng (Người mua)**: Truy cập các tính năng phía khách hàng, đặt hàng, theo dõi giao hàng.

---

## Sơ Đồ Hệ Thống Chi Tiết (Mermaid Diagrams)

### 1. Cấu Trúc Phân Cấp User

```mermaid
flowchart LR
    subgraph L1 ["🔴 CẤP 1 - QUYỀN CAO NHẤT"]
        SA["👑 Super Admin<br/>━━━━━━━━━━━━━<br/>🔧 Toàn quyền 20 modules<br/>👥 Quản lý tất cả user<br/>⚙️ Cài đặt hệ thống<br/>📊 Báo cáo tổng quan<br/>💾 Backup/Restore"]
    end
    
    subgraph L2 ["🔵 CẤP 2 - QUẢN LÝ CHUYÊN MÔN"]
        direction TB
        A["👨‍💼 Admin<br/>━━━━━━━━━━━━━<br/>📦 Quản lý sản phẩm<br/>🛒 Quản lý đơn hàng<br/>👥 Quản lý khách hàng<br/>📋 Xem báo cáo<br/>🏪 Quản lý kho"]
        
        OM["📦 Order Manager<br/>━━━━━━━━━━━━━<br/>📦 Xử lý đơn hàng<br/>🚚 Phân công shipper<br/>📊 Báo cáo vận chuyển<br/>⏰ Theo dõi ETA<br/>🔄 Xử lý đổi trả"]
        
        S["🏪 Seller<br/>━━━━━━━━━━━━━<br/>🏪 Quản lý cửa hàng<br/>📦 CRUD sản phẩm riêng<br/>📈 Analytics bán hàng<br/>💰 Rút tiền doanh thu<br/>🎁 Tạo khuyến mãi"]
    end
    
    subgraph L3 ["🟢 CẤP 3 - THỰC THI & KHÁCH HÀNG"]
        direction TB
        SH["🚚 Shipper<br/>━━━━━━━━━━━━━<br/>📦 Nhận đơn được giao<br/>🚚 Cập nhật trạng thái<br/>📸 Upload bằng chứng<br/>📞 Liên hệ khách hàng<br/>📊 Báo cáo giao hàng"]
        
        C["🛒 Customer<br/>━━━━━━━━━━━━━<br/>🔍 Xem sản phẩm<br/>🛒 Đặt hàng<br/>📋 Theo dõi đơn hàng<br/>⭐ Đánh giá sản phẩm<br/>💳 Thanh toán"]
    end
    
    %% Kết nối phân cấp từ trái qua phải
    SA ====> A
    SA ====> OM  
    SA ====> S
    A ====> SH
    A ====> C
    
    %% Quyền hạn Super Admin
    SA -.-> SA_PERM[🔧 Toàn quyền 20 modules<br/>👥 Quản lý tất cả user<br/>⚙️ Cài đặt hệ thống<br/>📊 Báo cáo tổng quan<br/>💾 Backup/Restore]
    
    %% Quyền hạn Admin
    A -.-> A_PERM[📦 Quản lý sản phẩm<br/>🛒 Quản lý đơn hàng<br/>👥 Quản lý khách hàng<br/>📋 Xem báo cáo<br/>🏪 Quản lý kho]
    
    %% Quyền hạn Order Manager
    OM -.-> OM_PERM[� Quản lý đơn hàng<br/>📦 Theo dõi vận chuyển<br/>💰 Xử lý thanh toán<br/>📊 Báo cáo bán hàng]
    
    %% Quyền hạn Seller
    S -.-> S_PERM[🏪 Quản lý shop riêng<br/>� Quản lý sản phẩm shop<br/>🛒 Xử lý đơn hàng shop<br/>📊 Báo cáo doanh thu]
    
    %% Quyền hạn Shipper
    SH -.-> SH_PERM[� Nhận đơn giao hàng<br/>📍 Cập nhật trạng thái<br/>📷 Upload bằng chứng<br/>📞 Liên hệ khách hàng]
    
    %% Quyền hạn Customer
    C -.-> C_PERM[🛒 Đặt hàng<br/>👤 Quản lý tài khoản<br/>📦 Theo dõi đơn hàng<br/>⭐ Đánh giá sản phẩm]
    
    classDef superAdmin fill:#ff6b6b,stroke:#fff,color:#fff
    classDef admin fill:#4ecdc4,stroke:#fff,color:#fff
    classDef manager fill:#45b7d1,stroke:#fff,color:#fff
    classDef seller fill:#96ceb4,stroke:#fff,color:#333
    classDef shipper fill:#feca57,stroke:#fff,color:#333
    classDef customer fill:#ff9ff3,stroke:#fff,color:#333
    classDef permission fill:#f8f9fa,stroke:#dee2e6,color:#495057
    
    class SA superAdmin
    class A admin
    class OM manager
    class S seller
    class SH shipper
    class C customer
    class SA_PERM,A_PERM,OM_PERM,S_PERM,SH_PERM,C_PERM permission

    OM --> OM1[📦 Xử lý đơn hàng]
    OM --> OM2[🚚 Phân công shipper]
    OM --> OM3[📊 Báo cáo vận chuyển]
    OM --> OM4[⏰ Theo dõi ETA]
    OM --> OM5[🔄 Xử lý đổi trả]

    S --> S1[🏪 Quản lý cửa hàng]
    S --> S2[📦 CRUD sản phẩm riêng]
    S --> S3[📈 Analytics bán hàng]
    S --> S4[💰 Rút tiền doanh thu]
    S --> S5[🎁 Tạo khuyến mãi]

    SH --> SH1[📦 Nhận đơn được giao]
    SH --> SH2[🚚 Cập nhật trạng thái]
    SH --> SH3[📸 Upload bằng chứng]
    SH --> SH4[📞 Liên hệ khách hàng]
    
    %% Styling cho từng cấp
    classDef level1 fill:#e74c3c,stroke:#fff,stroke-width:4px,color:#fff,font-weight:bold
    classDef level2 fill:#3498db,stroke:#fff,stroke-width:3px,color:#fff,font-weight:bold  
    classDef level3 fill:#27ae60,stroke:#fff,stroke-width:2px,color:#fff,font-weight:bold
    
    class SA level1
    class A,OM,S level2
    class SH,C level3
```

### 2. Ma Trận Phân Quyền Chi Tiết

```mermaid
flowchart LR
    subgraph "👑 Quyền Super Admin"
        SA1[👥 Quản lý người dùng<br/>100% toàn bộ modules]
        SA2[⚙️ Cấu hình hệ thống<br/>Tất cả cài đặt]
        SA3[📊 Truy cập toàn bộ dữ liệu<br/>Báo cáo toàn cục]
        SA4[🔐 Cài đặt bảo mật<br/>Vai trò & phân quyền]
        SA5[💾 Quản lý sao lưu<br/>Backup hệ thống]
    end

    subgraph "👨‍💼 Quyền Admin"
        A1[📦 Quản lý sản phẩm<br/>CRUD tất cả sản phẩm]
        A2[🛒 Quản lý đơn hàng<br/>Kiểm soát toàn bộ đơn]
        A3[👥 Quản lý khách hàng<br/>Quản lý người dùng]
        A4[📋 Kiểm soát tồn kho<br/>Quản lý kho hàng]
        A5[📊 Báo cáo bán hàng<br/>Phân tích kinh doanh]
        A6[💰 Quản lý giá cả<br/>Kiểm soát định giá]
        A7[🎨 Quản lý nội dung<br/>Blog, trang, slider]
        A8[🏷️ Thương hiệu & Danh mục<br/>Quản lý catalog]
    end

    subgraph "📦 Quyền Order Manager"
        OM1[📦 Xử lý đơn hàng<br/>Kiểm soát đầy đủ đơn]
        OM2[🚚 Quản lý vận chuyển<br/>Phân công & theo dõi]
        OM3[📊 Báo cáo giao hàng<br/>Phân tích logistics]
        OM4[⏰ Quản lý ETA<br/>Theo dõi thời gian]
        OM5[🔄 Xử lý đổi trả<br/>Quy trình hoàn tiền]
        OM6[📞 Hỗ trợ khách hàng<br/>Vấn đề đơn hàng]
    end

    subgraph "🏪 Quyền Seller"
        S1[🏪 Quản lý cửa hàng<br/>Chỉ cửa hàng riêng]
        S2[📦 CRUD sản phẩm<br/>Sản phẩm của mình]
        S3[📈 Phân tích bán hàng<br/>Hiệu suất cá nhân]
        S4[🎁 Công cụ khuyến mãi<br/>Coupon & giảm giá]
        S5[⭐ Quản lý đánh giá<br/>Review sản phẩm]
        S6[🏷️ Thuộc tính sản phẩm<br/>Biến thể & tùy chọn]
    end

    subgraph "🚚 Quyền Shipper"
        SH1[📦 Đơn được phân công<br/>Chỉ xem đơn của mình]
        SH2[🚚 Cập nhật trạng thái<br/>Tiến độ giao hàng]
        SH3[📸 Upload bằng chứng<br/>Chứng cứ giao hàng]
        SH4[📊 Báo cáo giao hàng<br/>Hiệu suất cá nhân]
    end

    subgraph "🛒 Quyền Customer"
        C1[🔍 Duyệt sản phẩm<br/>Xem catalog]
        C2[🛒 Đặt hàng<br/>Giỏ hàng]
        C3[📋 Lịch sử đơn hàng<br/>Chỉ đơn của mình]
        C4[⭐ Đánh giá sản phẩm<br/>Rating & bình luận]
        C5[💳 Xử lý thanh toán<br/>Checkout]
        C6[📞 Ticket hỗ trợ<br/>Dịch vụ khách hàng]
        C7[🔄 Yêu cầu đổi trả<br/>Đơn hàng của mình]
        C8[👤 Quản lý hồ sơ<br/>Thông tin cá nhân]
    end
```

### 3. Luồng Quy Trình Đăng Nhập và Phân Quyền

```mermaid
flowchart LR
    Start([👤 Người dùng truy cập hệ thống]) --> LoginChoice{🔐 Chọn phương thức đăng nhập}
    
    LoginChoice -->|📧 Email| EmailAuth[📧 Email + Password<br/>+ Captcha]
    LoginChoice -->|🌐 Social| SocialAuth[🌐 Google/Facebook<br/>OAuth 2.0]
    
    EmailAuth --> Validate{🔍 Xác thực}
    SocialAuth --> Validate
    
    Validate -->|❌ Fail| LoginFail[❌ Đăng nhập thất bại<br/>Retry hoặc Forgot Password]
    Validate -->|✅ Success| CheckRole{🎯 Kiểm tra vai trò}
    
    LoginFail --> Start
    
    CheckRole -->|👑| SADashboard[👑 Super Admin Dashboard<br/>🎛️ Kiểm soát toàn hệ thống]
    CheckRole -->|👨‍💼| ADashboard[👨‍💼 Admin Dashboard<br/>📊 Quản lý kinh doanh]
    CheckRole -->|📦| OMDashboard[📦 Order Manager Dashboard<br/>🚚 Kiểm soát đơn hàng & vận chuyển]
    CheckRole -->|🏪| SDashboard[🏪 Seller Dashboard<br/>📈 Quản lý cửa hàng]
    CheckRole -->|🚚| SHDashboard[🚚 Shipper Dashboard<br/>📦 Quản lý giao hàng]
    CheckRole -->|🛒| CDashboard[🛒 Customer Dashboard<br/>🛍️ Trải nghiệm mua sắm]

    SADashboard --> SAMenu{🎛️ Chức năng Super Admin}
    ADashboard --> AMenu{👨‍💼 Chức năng Admin}
    OMDashboard --> OMMenu{📦 Chức năng Order Manager}
    SDashboard --> SMenu{🏪 Chức năng Seller}
    SHDashboard --> SHMenu{🚚 Chức năng Shipper}
    CDashboard --> CMenu{🛒 Chức năng Customer}

    SAMenu -->|👥| UserMgmt[👥 Quản lý User<br/>Tạo/Sửa/Xóa tất cả vai trò]
    SAMenu -->|⚙️| SystemConfig[⚙️ Cấu hình hệ thống<br/>Cài đặt & Bảo mật]
    SAMenu -->|📊| GlobalReports[📊 Báo cáo toàn hệ thống<br/>Phân tích & KPIs]

    AMenu -->|📦| ProductMgmt[📦 Quản lý sản phẩm<br/>CRUD tất cả sản phẩm]
    AMenu -->|🛒| OrderMgmt[🛒 Quản lý đơn hàng<br/>Xử lý tất cả đơn hàng]
    AMenu -->|👥| CustomerMgmt[👥 Quản lý khách hàng<br/>Hỗ trợ & quản lý user]
    AMenu -->|🎨| ContentMgmt[🎨 Quản lý nội dung<br/>Blog, trang, banner]

    OMMenu -->|📦| OrderProcess[📦 Xử lý đơn hàng<br/>Trạng thái & quy trình]
    OMMenu -->|🚚| ShippingMgmt[🚚 Quản lý vận chuyển<br/>Phân công & theo dõi]
    OMMenu -->|📊| DeliveryReports[📊 Báo cáo giao hàng<br/>Phân tích logistics]

    SMenu -->|🏪| ShopMgmt[🏪 Quản lý cửa hàng<br/>Thiết lập & thiết kế store]
    SMenu -->|📦| MyProducts[📦 Sản phẩm của tôi<br/>Quản lý sản phẩm riêng]
    SMenu -->|📈| SalesAnalytics[📈 Phân tích bán hàng<br/>Theo dõi hiệu suất]

    SHMenu -->|📦| MyOrders[📦 Đơn hàng của tôi<br/>Giao hàng được phân công]
    SHMenu -->|🚚| UpdateStatus[🚚 Cập nhật trạng thái<br/>Tiến độ giao hàng]
    SHMenu -->|📸| UploadProof[📸 Upload bằng chứng<br/>Chứng cứ giao hàng]

    CMenu -->|🔍| BrowseProducts[🔍 Duyệt sản phẩm<br/>Mua sắm & tìm kiếm]
    CMenu -->|🛒| Shopping[🛒 Mua sắm<br/>Giỏ hàng & thanh toán]
    CMenu -->|📋| OrderTracking[📋 Theo dõi đơn hàng<br/>Trạng thái đơn hàng]
    CMenu -->|⭐| ReviewProducts[⭐ Đánh giá sản phẩm<br/>Rating & review]
```

### 4. Luồng Mua Bán Hàng Theo Role

```mermaid
sequenceDiagram
    participant C as 🛒 Khách hàng
    participant S as 🏪 Người bán
    participant A as 👨‍💼 Admin
    participant OM as 📦 Quản lý đơn hàng
    participant SH as 🚚 Shipper
    participant SYS as ⚙️ Hệ thống
    participant AI as 🤖 AI Engine

    Note over C,AI: 🔍 GIAI ĐOẠN KHÁM PHÁ SẢN PHẨM
    C->>SYS: 🔍 Duyệt danh mục/tìm kiếm
    SYS->>AI: 🤖 Lấy gợi ý cá nhân hóa
    AI->>SYS: 📊 Trả về gợi ý AI
    SYS->>C: 📦 Hiển thị sản phẩm + gợi ý
    
    C->>SYS: 👁️ Xem chi tiết sản phẩm
    SYS->>C: 📋 Hiển thị thông tin + đánh giá
    
    Note over C,SYS: 🛒 GIAI ĐOẠN MUA SẮM
    C->>SYS: ➕ Thêm vào giỏ hàng
    C->>SYS: 💰 Áp dụng mã giảm giá
    SYS->>C: 💳 Hiển thị trang thanh toán
    
    C->>SYS: 💳 Tiến hành thanh toán (VNPay/Banking/Wallet)
    SYS->>C: ✅ Xác nhận đơn hàng
    
    Note over SYS,OM: 📦 XỬ LÝ ĐƠN HÀNG
    SYS->>A: � Thông báo đơn hàng mới (Email)
    A->>OM: 📋 Phân công đơn hàng cho Order Manager
    OM->>SYS: ✅ Xác nhận xử lý đơn hàng
    
    OM->>S: � Thông báo người bán về đơn hàng (Email)
    S->>SYS: ✅ Xác nhận có hàng
    S->>SYS: 📦 Cập nhật tồn kho
    
    Note over OM,SH: 🚚 SHIPPING PHASE (Vận chuyển)
    OM->>SH: 🚚 Assign delivery to shipper
    SH->>SYS: ✅ Accept delivery assignment
    SYS->>C: � Email: "Đơn hàng đang được chuẩn bị"
    
    SH->>SYS: 📦 Update: "Đang lấy hàng"
    SYS->>C: � Email notification
    
    SH->>SYS: 🚚 Update: "Đang giao hàng"
    SYS->>C: � Phone call để xác nhận địa chỉ
    
    SH->>SYS: 📸 Upload delivery proof + signature
    SH->>SYS: ✅ Update: "Đã giao thành công"
    SYS->>C: 📧 "Đơn hàng đã được giao!"
    
    Note over C,SYS: ⭐ SAU KHI MUA HÀNG
    C->>SYS: ⭐ Đánh giá và review sản phẩm
    SYS->>S: 📊 Cập nhật rating người bán
    
    alt Khách hàng hài lòng
        C->>SYS: 🔄 Đặt lại sản phẩm tương tự
        SYS->>AI: 📈 Cập nhật sở thích khách hàng
    else Khách hàng không hài lòng
        C->>SYS: 🔄 Yêu cầu đổi trả/hoàn tiền
        SYS->>OM: ⚖️ Xử lý yêu cầu đổi trả
        OM->>C: ✅ Chấp thuận hoàn tiền
        SYS->>C: 💰 Xử lý hoàn tiền qua phương thức gốc
    end
    
    Note over A,SYS: 📊 PHÂN TÍCH & BÁO CÁO
    A->>SYS: 📊 Tạo báo cáo bán hàng
    SYS->>A: 📈 Dashboard phân tích kinh doanh
    
    S->>SYS: 📊 Xem hiệu suất cửa hàng của tôi
    SYS->>S: 📈 Phân tích người bán + doanh thu
    
    OM->>SYS: 📊 Báo cáo hiệu suất giao hàng
    SYS->>OM: 🚚 Phân tích logistics
```

### 5. Luồng Xử Lý Lỗi và Phân Quyền

```mermaid
flowchart TD
    Request[🔑 User Request<br/>Action + Resource] --> AuthCheck{🔐 Đã đăng nhập?}
    
    AuthCheck -->|❌ No| RedirectLogin[🔄 Redirect to Login<br/>Save intended URL]
    AuthCheck -->|✅ Yes| SessionCheck{⏰ Session hợp lệ?}
    
    SessionCheck -->|❌ Expired| ForceReauth[🔄 Force Re-authentication<br/>Clear invalid session]
    SessionCheck -->|✅ Valid| PermissionCheck{🔍 Kiểm tra quyền?}
    
    PermissionCheck -->|✅ Allow| ExecuteAction[✅ Thực hiện action<br/>Log successful access]
    PermissionCheck -->|❌ Deny| CheckInherit{🔄 Có inherit không?}
    PermissionCheck -->|🚫 Explicit Deny| AccessDenied[🚫 403 Forbidden<br/>Explicit denial]
    
    CheckInherit -->|✅ Has Parent| CheckParentRole[🔄 Check parent role permissions]
    CheckInherit -->|❌ No Parent| DefaultDeny[❌ Default Deny<br/>No permission found]
    
    CheckParentRole --> PermissionCheck
    
    AccessDenied --> LogSecurity[📋 Log security violation<br/>IP + User + Action + Time]
    DefaultDeny --> LogSecurity
    
    LogSecurity --> ErrorResponse{🎯 Error Response Type}
    
    ErrorResponse -->|🔐 Auth| Show401[🔐 401 Unauthorized<br/>Vui lòng đăng nhập]
    ErrorResponse -->|🚫 Permission| Show403[🚫 403 Forbidden<br/>Bạn không có quyền truy cập]
    ErrorResponse -->|❓ Not Found| Show404[❓ 404 Not Found<br/>Trang không tồn tại]
    ErrorResponse -->|💥 Server| Show500[💥 500 Server Error<br/>Lỗi hệ thống vui lòng thử lại]
    
    Show401 --> CheckRetry{🔄 Retry Logic}
    Show403 --> NotifyAdmin{🚨 Notify Admin?}
    Show404 --> LogAccess[📋 Log access attempt]
    Show500 --> AlertDevOps[🚨 Alert DevOps team]
    
    CheckRetry -->|< 3 attempts| RedirectLogin
    CheckRetry -->|≥ 3 attempts| LockAccount[🔒 Temporary account lock<br/>15 minutes cooldown]
    
    NotifyAdmin -->|Critical| ImmediateAlert[🚨 Immediate security alert<br/>SMS + Email + Slack]
    NotifyAdmin -->|Normal| DailyReport[📊 Include in daily security report]
    
    ForceReauth --> RedirectLogin
    RedirectLogin --> Request
    
    LogSecurity --> AIAnalysis[🤖 AI Security Analysis<br/>Pattern detection]
    AIAnalysis --> ThreatLevel{⚡ Threat Level?}
    ThreatLevel -->|🟢 Low| NormalLogging[📝 Standard logging]
    ThreatLevel -->|🟡 Medium| EnhancedMonitoring[👁️ Enhanced monitoring<br/>Watch user behavior]
    ThreatLevel -->|🔴 High| AutoBlock[🛡️ Auto-block suspicious IP<br/>Quarantine user session]
```

### 6. Phân Loại Lỗi Hệ Thống

```mermaid
flowchart LR
    SystemError[💥 System Error Detected] --> ErrorClassifier{🎯 Error Type Classification}
    
    ErrorClassifier -->|🌐| NetworkError[🌐 Network Error]
    ErrorClassifier -->|💾| DatabaseError[💾 Database Error]
    ErrorClassifier -->|💳| PaymentError[� Payment Error]
    ErrorClassifier -->|🔍| SearchError[🔍 Search Error]
    ErrorClassifier -->|📦| InventoryError[📦 Inventory Error]
    ErrorClassifier -->|🔐| AuthError[🔐 Authentication Error]
    ErrorClassifier -->|🚚| ShippingError[🚚 Shipping Error]
    ErrorClassifier -->|📱| AppError[📱 Application Error]
    
    NetworkError --> NetworkRecovery[🔄 Auto retry 3x<br/>Exponential backoff<br/>Switch to CDN]
    DatabaseError --> DatabaseRecovery[🔄 Database failover<br/>Read from replica<br/>Queue writes]
    PaymentError --> PaymentRecovery[💳 Retry payment<br/>Try alternative gateway<br/>Notify user]
    SearchError --> SearchRecovery[🔍 Fallback to cached results<br/>Suggest alternatives<br/>Simple search]
    InventoryError --> InventoryRecovery[� Real-time stock check<br/>Hide out-of-stock<br/>Suggest similar]
    AuthError --> AuthRecovery[🔐 Force re-authentication<br/>Clear invalid tokens<br/>Redirect to login]
    ShippingError --> ShippingRecovery[� Recalculate routes<br/>Notify customer<br/>Update ETA]
    AppError --> AppRecovery[📱 Restart service<br/>Log crash report<br/>Fallback UI]
    
    NetworkRecovery --> UserNotification[📱 User Notification]
    DatabaseRecovery --> UserNotification
    PaymentRecovery --> UserNotification
    SearchRecovery --> UserNotification
    InventoryRecovery --> UserNotification
    AuthRecovery --> UserNotification
    ShippingRecovery --> UserNotification
    AppRecovery --> UserNotification
    
    UserNotification --> LogError[📋 Log Error Details]
    LogError --> AlertTeam[🚨 Alert Technical Team]
```

### 7. Dashboard Giám Sát Bảo Mật

```mermaid
graph TB
    Monitor[🔍 Giám sát bảo mật] --> Metrics{📊 Các chỉ số chính}
    
    Metrics --> LoginAttempts[🔐 Lần đăng nhập<br/>Thành công vs Thất bại<br/>Theo dõi vị trí địa lý]
    Metrics --> PermissionViolations[🚫 Vi phạm quyền<br/>Tần suất theo user<br/>Mẫu truy cập tài nguyên]
    Metrics --> SystemHealth[⚡ Sức khỏe hệ thống<br/>Thời gian phản hồi<br/>Tỷ lệ lỗi]
    Metrics --> UserBehavior[👤 Hành vi người dùng<br/>Thời gian session<br/>Mẫu hành động]
    
    LoginAttempts --> Alert1{🚨 Alert Threshold}
    PermissionViolations --> Alert2{🚨 Alert Threshold}
    SystemHealth --> Alert3{� Alert Threshold}
    UserBehavior --> Alert4{🚨 Alert Threshold}
    
    Alert1 -->|Cao| ImmediateAction[🚨 Hành động ngay lập tức<br/>Chặn IP, Khóa tài khoản<br/>📧 Email team bảo mật]
    Alert2 -->|High| ImmediateAction
    Alert3 -->|High| ImmediateAction
    Alert4 -->|High| ImmediateAction
    
    Alert1 -->|Trung bình| DelayedAction[⏰ Hành động chậm<br/>Tăng cường giám sát<br/>📧 Email cho admin]
    Alert2 -->|Medium| DelayedAction
    Alert3 -->|Medium| DelayedAction
    Alert4 -->|Medium| DelayedAction
    
    Alert1 -->|Thấp| LogOnly[📝 Chỉ ghi log<br/>Báo cáo hàng ngày<br/>Không hành động ngay]
    Alert2 -->|Low| LogOnly
    Alert3 -->|Low| LogOnly
    Alert4 -->|Low| LogOnly
    
    ImmediateAction --> Recovery[🔄 Tự phục hồi<br/>Hệ thống tự chữa lành]
    DelayedAction --> Recovery
    LogOnly --> WeeklyReport[📊 Báo cáo bảo mật hàng tuần]
```

### 8. Bảng Phân Quyền Chi Tiết 20 Modules

```mermaid
graph LR
    subgraph "Module Permissions Matrix"
        A[Attributes] --> A1[SA: ✅ CRUD<br/>Admin: ✅ CRUD<br/>OM: ❌<br/>Seller: ✅ Own<br/>Shipper: ❌<br/>Customer: ❌]
        
        B[Blog] --> B1[SA: ✅ CRUD<br/>Admin: ✅ CRUD<br/>OM: ❌<br/>Seller: ❌<br/>Shipper: ❌<br/>Customer: 👁️ Read]
        
        C[Brands] --> C1[SA: ✅ CRUD<br/>Admin: ✅ CRU<br/>OM: 👁️ Read<br/>Seller: 👁️ Read<br/>Shipper: ❌<br/>Customer: 👁️ Read]
        
        D[Categories] --> D1[SA: ✅ CRUD<br/>Admin: ✅ CRU<br/>OM: 👁️ Read<br/>Seller: 👁️ Read<br/>Shipper: 👁️ Read<br/>Customer: 👁️ Read]
        
        E[Coupons] --> E1[SA: ✅ CRUD<br/>Admin: ✅ CRUD<br/>OM: 👁️ Read<br/>Seller: ✅ Own<br/>Shipper: ❌<br/>Customer: 👁️ Use]
        
        F[FlashSales] --> F1[SA: ✅ CRUD<br/>Admin: ✅ CRUD<br/>OM: 👁️ Read<br/>Seller: ✅ Own<br/>Shipper: ❌<br/>Customer: 👁️ Read]
        
        G[Menus] --> G1[SA: ✅ CRUD<br/>Admin: ✅ CRU<br/>OM: ❌<br/>Seller: ❌<br/>Shipper: ❌<br/>Customer: ❌]
        
        H[Options] --> H1[SA: ✅ CRUD<br/>Admin: ✅ CRU<br/>OM: ❌<br/>Seller: ✅ Own<br/>Shipper: ❌<br/>Customer: ❌]
        
        I[Orders] --> I1[SA: ✅ CRUD<br/>Admin: ✅ CRU<br/>OM: ✅ CRUD<br/>Seller: 📝 Own<br/>Shipper: 📝 Assigned<br/>Customer: 👁️ Own]
        
        J[Pages] --> J1[SA: ✅ CRUD<br/>Admin: ✅ CRUD<br/>OM: ❌<br/>Seller: ❌<br/>Shipper: ❌<br/>Customer: 👁️ Read]
    end
    
    subgraph "Legend"
        L1[✅ Full CRUD Access]
        L2[📝 Limited Edit]
        L3[👁️ View Only]
        L4[❌ No Access]
        L5[🔄 Inherit Permission]
    end
```

---

## Ma Trận Phân Quyền Chi Tiết (20 Modules - Logic Chuẩn E-commerce)

### Cấu Trúc Phân Quyền
- **Allow**: Cho phép thực hiện hành động
- **Deny**: Từ chối thực hiện hành động  
- **Inherit**: Kế thừa quyền từ vai trò cha

### Nguyên Tắc Phân Quyền Logic:
- **Super Admin**: Toàn quyền hệ thống
- **Admin**: Quản lý toàn bộ trừ cài đặt hệ thống
- **Quản Lý ĐH**: Chuyên về đơn hàng, vận chuyển, báo cáo
- **Người Bán**: Quản lý sản phẩm & đơn hàng của mình
- **Shipper**: Chỉ xem/cập nhật đơn hàng được giao
- **Khách Hàng**: Chỉ tương tác cơ bản (xem, mua, đánh giá)

### Danh Sách Module Chính (20 Modules)

#### 1. Attribute (Thuộc Tính Sản Phẩm)
| Module/Action | Super Admin | Admin | Quản Lý ĐH | Người Bán | Shipper | Khách Hàng |
|---------------|:-----------:|:-----:|:----------:|:---------:|:-------:|:----------:|
| **attributes.index** | Allow | Allow | Deny | Allow | Deny | Deny |
| **attributes.create** | Allow | Allow | Deny | Inherit | Deny | Deny |
| **attributes.edit** | Allow | Allow | Deny | Inherit | Deny | Deny |
| **attributes.delete** | Allow | Deny | Deny | Deny | Deny | Deny |

#### 2. Blog (Tin Tức/Bài Viết)
| Module/Action | Super Admin | Admin | Quản Lý ĐH | Người Bán | Shipper | Khách Hàng |
|---------------|:-----------:|:-----:|:----------:|:---------:|:-------:|:----------:|
| **blog.index** | Allow | Allow | Deny | Deny | Deny | Allow |
| **blog.create** | Allow | Allow | Deny | Deny | Deny | Deny |
| **blog.edit** | Allow | Allow | Deny | Deny | Deny | Deny |
| **blog.delete** | Allow | Allow | Deny | Deny | Deny | Deny |

#### 3. Brand (Thương Hiệu)
| Module/Action | Super Admin | Admin | Quản Lý ĐH | Người Bán | Shipper | Khách Hàng |
|---------------|:-----------:|:-----:|:----------:|:---------:|:-------:|:----------:|
| **brands.index** | Allow | Allow | Allow | Allow | Deny | Allow |
| **brands.create** | Allow | Allow | Deny | Deny | Deny | Deny |
| **brands.edit** | Allow | Allow | Deny | Deny | Deny | Deny |
| **brands.delete** | Allow | Deny | Deny | Deny | Deny | Deny |

#### 4. Category (Danh Mục)
| Module/Action | Super Admin | Admin | Quản Lý ĐH | Người Bán | Shipper | Khách Hàng |
|---------------|:-----------:|:-----:|:----------:|:---------:|:-------:|:----------:|
| **categories.index** | Allow | Allow | Allow | Allow | Allow | Allow |
| **categories.create** | Allow | Allow | Deny | Deny | Deny | Deny |
| **categories.edit** | Allow | Allow | Deny | Deny | Deny | Deny |
| **categories.delete** | Allow | Deny | Deny | Deny | Deny | Deny |

#### 5. Coupon (Mã Giảm Giá)
| Module/Action | Super Admin | Admin | Quản Lý ĐH | Người Bán | Shipper | Khách Hàng |
|---------------|:-----------:|:-----:|:----------:|:---------:|:-------:|:----------:|
| **coupons.index** | Allow | Allow | Allow | Allow | Deny | Allow |
| **coupons.create** | Allow | Allow | Deny | Allow | Deny | Deny |
| **coupons.edit** | Allow | Allow | Deny | Allow | Deny | Deny |
| **coupons.delete** | Allow | Allow | Deny | Deny | Deny | Deny |
| **coupons.use** | Allow | Allow | Allow | Allow | Deny | Allow |

#### 6. FlashSale (Flash Sale)
| Module/Action | Super Admin | Admin | Quản Lý ĐH | Người Bán | Shipper | Khách Hàng |
|---------------|:-----------:|:-----:|:----------:|:---------:|:-------:|:----------:|
| **flashsales.index** | Allow | Allow | Allow | Allow | Deny | Allow |
| **flashsales.create** | Allow | Allow | Deny | Allow | Deny | Deny |
| **flashsales.edit** | Allow | Allow | Deny | Allow | Deny | Deny |
| **flashsales.delete** | Allow | Allow | Deny | Deny | Deny | Deny |

#### 7. Menu (Menu Điều Hướng)
| Module/Action | Super Admin | Admin | Quản Lý ĐH | Người Bán | Shipper | Khách Hàng |
|---------------|:-----------:|:-----:|:----------:|:---------:|:-------:|:----------:|
| **menus.index** | Allow | Allow | Deny | Deny | Deny | Deny |
| **menus.create** | Allow | Allow | Deny | Deny | Deny | Deny |
| **menus.edit** | Allow | Allow | Deny | Deny | Deny | Deny |
| **menus.delete** | Allow | Deny | Deny | Deny | Deny | Deny |

#### 8. Option (Tùy Chọn Sản Phẩm)
| Module/Action | Super Admin | Admin | Quản Lý ĐH | Người Bán | Shipper | Khách Hàng |
|---------------|:-----------:|:-----:|:----------:|:---------:|:-------:|:----------:|
| **options.index** | Allow | Allow | Deny | Allow | Deny | Deny |
| **options.create** | Allow | Allow | Deny | Allow | Deny | Deny |
| **options.edit** | Allow | Allow | Deny | Allow | Deny | Deny |
| **options.delete** | Allow | Deny | Deny | Deny | Deny | Deny |

#### 9. Order (Đơn Hàng) - Module Quan Trọng Nhất
| Module/Action | Super Admin | Admin | Quản Lý ĐH | Người Bán | Shipper | Khách Hàng |
|---------------|:-----------:|:-----:|:----------:|:---------:|:-------:|:----------:|
| **orders.index** | Allow | Allow | Allow | Allow | Allow | Allow |
| **orders.create** | Allow | Allow | Allow | Deny | Deny | Allow |
| **orders.edit** | Allow | Allow | Allow | Allow | Deny | Inherit |
| **orders.delete** | Allow | Deny | Allow | Deny | Deny | Deny |
| **orders.status_update** | Allow | Allow | Allow | Allow | Allow | Deny |
| **orders.assign_shipper** | Allow | Allow | Allow | Deny | Deny | Deny |
| **orders.cancel** | Allow | Allow | Allow | Allow | Deny | Allow |
| **orders.refund** | Allow | Allow | Allow | Deny | Deny | Inherit |

#### 10. Page (Trang Nội Dung)
| Module/Action | Super Admin | Admin | Quản Lý ĐH | Người Bán | Shipper | Khách Hàng |
|---------------|:-----------:|:-----:|:----------:|:---------:|:-------:|:----------:|
| **pages.index** | Allow | Allow | Deny | Deny | Deny | Allow |
| **pages.create** | Allow | Allow | Deny | Deny | Deny | Deny |
| **pages.edit** | Allow | Allow | Deny | Deny | Deny | Deny |
| **pages.delete** | Allow | Allow | Deny | Deny | Deny | Deny |

#### 11. Product (Sản Phẩm) - Module Cốt Lõi
| Module/Action | Super Admin | Admin | Quản Lý ĐH | Người Bán | Shipper | Khách Hàng |
|---------------|:-----------:|:-----:|:----------:|:---------:|:-------:|:----------:|
| **products.index** | Allow | Allow | Allow | Allow | Allow | Allow |
| **products.create** | Allow | Allow | Deny | Allow | Deny | Deny |
| **products.edit** | Allow | Allow | Deny | Allow | Deny | Deny |
| **products.delete** | Allow | Allow | Deny | Allow | Deny | Deny |
| **products.approve** | Allow | Allow | Deny | Deny | Deny | Deny |
| **products.feature** | Allow | Allow | Deny | Deny | Deny | Deny |

#### 12. Report (Báo Cáo)
| Module/Action | Super Admin | Admin | Quản Lý ĐH | Người Bán | Shipper | Khách Hàng |
|---------------|:-----------:|:-----:|:----------:|:---------:|:-------:|:----------:|
| **reports.sales** | Allow | Allow | Allow | Allow | Deny | Deny |
| **reports.orders** | Allow | Allow | Allow | Allow | Allow | Deny |
| **reports.users** | Allow | Allow | Deny | Deny | Deny | Deny |
| **reports.financial** | Allow | Allow | Allow | Allow | Deny | Deny |
| **reports.inventory** | Allow | Allow | Allow | Allow | Deny | Deny |

#### 13. Review (Đánh Giá)
| Module/Action | Super Admin | Admin | Quản Lý ĐH | Người Bán | Shipper | Khách Hàng |
|---------------|:-----------:|:-----:|:----------:|:---------:|:-------:|:----------:|
| **reviews.index** | Allow | Allow | Allow | Allow | Deny | Allow |
| **reviews.create** | Allow | Allow | Deny | Deny | Deny | Allow |
| **reviews.edit** | Allow | Allow | Deny | Deny | Deny | Allow |
| **reviews.delete** | Allow | Allow | Deny | Deny | Deny | Allow |
| **reviews.approve** | Allow | Allow | Deny | Allow | Deny | Deny |
| **reviews.reply** | Allow | Allow | Deny | Allow | Deny | Deny |

#### 14. Setting (Cài Đặt)
| Module/Action | Super Admin | Admin | Quản Lý ĐH | Người Bán | Shipper | Khách Hàng |
|---------------|:-----------:|:-----:|:----------:|:---------:|:-------:|:----------:|
| **settings.general** | Allow | Deny | Deny | Deny | Deny | Deny |
| **settings.payment** | Allow | Inherit | Deny | Deny | Deny | Deny |
| **settings.shipping** | Allow | Allow | Allow | Deny | Inherit | Deny |
| **settings.email** | Allow | Allow | Inherit | Deny | Deny | Deny |
| **settings.seo** | Allow | Allow | Deny | Deny | Deny | Deny |

#### 15. Slider (Slider/Banner)
| Module/Action | Super Admin | Admin | Quản Lý ĐH | Người Bán | Shipper | Khách Hàng |
|---------------|:-----------:|:-----:|:----------:|:---------:|:-------:|:----------:|
| **sliders.index** | Allow | Allow | Deny | Deny | Deny | Deny |
| **sliders.create** | Allow | Allow | Deny | Deny | Deny | Deny |
| **sliders.edit** | Allow | Allow | Deny | Deny | Deny | Deny |
| **sliders.delete** | Allow | Allow | Deny | Deny | Deny | Deny |

#### 16. Tag (Thẻ Tag)
| Module/Action | Super Admin | Admin | Quản Lý ĐH | Người Bán | Shipper | Khách Hàng |
|---------------|:-----------:|:-----:|:----------:|:---------:|:-------:|:----------:|
| **tags.index** | Allow | Allow | Allow | Allow | Deny | Allow |
| **tags.create** | Allow | Allow | Deny | Allow | Deny | Deny |
| **tags.edit** | Allow | Allow | Deny | Allow | Deny | Deny |
| **tags.delete** | Allow | Deny | Deny | Deny | Deny | Deny |

#### 17. Tax (Thuế)
| Module/Action | Super Admin | Admin | Quản Lý ĐH | Người Bán | Shipper | Khách Hàng |
|---------------|:-----------:|:-----:|:----------:|:---------:|:-------:|:----------:|
| **taxes.index** | Allow | Allow | Allow | Inherit | Deny | Deny |
| **taxes.create** | Allow | Allow | Deny | Deny | Deny | Deny |
| **taxes.edit** | Allow | Allow | Deny | Deny | Deny | Deny |
| **taxes.delete** | Allow | Deny | Deny | Deny | Deny | Deny |

#### 18. Transaction (Giao Dịch)
| Module/Action | Super Admin | Admin | Quản Lý ĐH | Người Bán | Shipper | Khách Hàng |
|---------------|:-----------:|:-----:|:----------:|:---------:|:-------:|:----------:|
| **transactions.index** | Allow | Allow | Allow | Allow | Deny | Allow |
| **transactions.create** | Allow | Allow | Deny | Deny | Deny | Allow |
| **transactions.refund** | Allow | Allow | Allow | Deny | Deny | Inherit |
| **transactions.withdraw** | Allow | Allow | Deny | Allow | Deny | Deny |
| **transactions.approve** | Allow | Allow | Allow | Deny | Deny | Deny |

#### 19. User (Người Dùng)
| Module/Action | Super Admin | Admin | Quản Lý ĐH | Người Bán | Shipper | Khách Hàng |
|---------------|:-----------:|:-----:|:----------:|:---------:|:-------:|:----------:|
| **users.index** | Allow | Allow | Inherit | Deny | Deny | Deny |
| **users.create** | Allow | Allow | Deny | Deny | Deny | Deny |
| **users.edit** | Allow | Allow | Inherit | Inherit | Inherit | Inherit |
| **users.delete** | Allow | Deny | Deny | Deny | Deny | Deny |
| **users.roles** | Allow | Deny | Deny | Deny | Deny | Deny |
| **users.ban** | Allow | Allow | Deny | Deny | Deny | Deny |

#### 20. Variation (Biến Thể Sản Phẩm)
| Module/Action | Super Admin | Admin | Quản Lý ĐH | Người Bán | Shipper | Khách Hàng |
|---------------|:-----------:|:-----:|:----------:|:---------:|:-------:|:----------:|
| **variations.index** | Allow | Allow | Deny | Allow | Deny | Deny |
| **variations.create** | Allow | Allow | Deny | Allow | Deny | Deny |
| **variations.edit** | Allow | Allow | Deny | Allow | Deny | Deny |
| **variations.delete** | Allow | Deny | Deny | Allow | Deny | Deny |

### Cấu Trúc Hệ Thống Phân Quyền

Hệ thống sử dụng cấu trúc database với 20 modules chính, mỗi module có các action như index, create, edit, delete. Mỗi quyền được quản lý bằng permission_key dạng "module.action" (ví dụ: attributes.create, orders.index).

### Logic Phân Quyền Chi Tiết

#### Super Admin (Toàn Quyền)
- **Allow ALL**: Tất cả quyền trong hệ thống
- **Chịu trách nhiệm**: Cài đặt hệ thống, phân quyền, quản lý tối cao

#### Admin (Quản Lý Tổng)
- **Allow**: Hầu hết các chức năng trừ cài đặt hệ thống cốt lõi
- **Deny**: settings.general, users.roles (chỉ Super Admin)
- **Chịu trách nhiệm**: Vận hành hàng ngày, quản lý nội dung

#### Quản Lý Đơn Hàng (Order Specialist)
- **Allow**: Tất cả về orders, reports, shipping settings
- **Deny**: Quản lý sản phẩm, người dùng, cài đặt
- **Chịu trách nhiệm**: Xử lý đơn hàng, vận chuyển, báo cáo

#### Người Bán (Seller)
- **Allow**: Quản lý sản phẩm của mình, đơn hàng liên quan
- **Deny**: Cài đặt hệ thống, quản lý người dùng khác
- **Chịu trách nhiệm**: Bán hàng, quản lý kho, customer service

#### Shipper (Delivery Person)
- **Allow**: Xem và cập nhật đơn hàng được giao
- **Deny**: Hầu hết chức năng khác
- **Chịu trách nhiệm**: Giao hàng, cập nhật trạng thái

#### Khách Hàng (Customer)
- **Allow**: Xem, mua, đánh giá, quản lý đơn hàng của mình
- **Deny**: Tất cả chức năng admin
- **Chịu trách nhiệm**: Mua sắm, đánh giá, phản hồi

### Cách Triển Khai Trong Hệ Thống

#### Nguyên Tắc Phân Quyền
1. **Deny luôn thắng**: Nếu có Deny thì sẽ từ chối dù có Allow
2. **Inherit từ vai trò cha**: Kế thừa quyền từ role cha hoặc default
3. **Least Privilege**: Mặc định không có quyền, phải cấp rõ ràng
4. **Granular Control**: Kiểm soát chi tiết đến từng hành động

### Ưu Điểm Của Cách Tiếp Cận Này
- **Linh Hoạt**: Có thể cấp/thu hồi quyền chi tiết
- **Bảo Mật**: Kiểm soát chặt chẽ từng chức năng
- **Dễ Quản Lý**: Giao diện trực quan như trong hình
- **Khả Năng Mở Rộng**: Dễ thêm module/permission mới

---

## Các Tính Năng Chính

### Tính Năng Mua Sắm Cốt Lõi
1. **Giao Diện UI/UX Hiện Đại**: Giao diện đẹp mắt, hiện đại, dễ tiếp cận và sử dụng
2. **Đăng Ký Đơn Giản**: Yêu cầu ít thông tin ban đầu, nâng cấp dần theo nhu cầu
3. **Loại Tài Khoản**: Tài khoản người tiêu dùng và chủ cửa hàng
4. **Giỏ Hàng & Thanh Toán**: Chức năng thương mại điện tử hoàn chỉnh
5. **Thông Tin Khách Hàng**: Lưu trữ số điện thoại, địa chỉ, họ tên
6. **Lịch Sử Mua Hàng**: Theo dõi hoàn chỉnh lịch sử mua sắm
7. **Danh Mục Sản Phẩm**: Phân loại sản phẩm có tổ chức
8. **Khuyến Mãi & Flash Sale**: Công cụ marketing và khuyến mãi
9. **Quản Lý Giao Hàng**: Quản lý địa chỉ và phương thức vận chuyển
10. **Phương Thức Thanh Toán**: Nhiều tùy chọn thanh toán
11. **Đánh Giá Sản Phẩm**: Hệ thống đánh giá và nhận xét của khách hàng

### Tính Năng Xã Hội & Tương Tác
12. **Bảng Tin Cá Nhân Hóa**: Nội dung tùy chỉnh theo sở thích người dùng
13. **Đăng Bài**: Nội dung ảnh, video và văn bản (do admin quản lý)
14. **Tương Tác Xã Hội**: Chức năng like, comment và chia sẻ
15. **Tìm Kiếm Nâng Cao**: Tìm kiếm sản phẩm, người dùng và nội dung với bộ lọc
16. **Nhắn Tin Trực Tiếp**: Chức năng chat 1-1
17. **Hệ Thống Theo Dõi**: Theo dõi người dùng và cửa hàng
18. **Thông Báo Đẩy**: Cập nhật thời gian thực

### Tính Năng Thương Mại Điện Tử Nâng Cao
19. **Trang Chi Tiết Sản Phẩm**: Thông tin sản phẩm toàn diện (không hiển thị thông tin liên hệ người bán)
20. **Cổng Thanh Toán**: Tích hợp ví điện tử và thẻ
21. **Quản Lý Đơn Hàng**: Quản lý toàn bộ vòng đời đơn hàng
22. **Tích Hợp Vận Chuyển**: Tích hợp dịch vụ vận chuyển bên thứ ba
23. **Theo Dõi Đơn Hàng**: Theo dõi giao hàng thời gian thực
24. **Chính Sách Trả Hàng/Hoàn Tiền**: Hệ thống trả hàng và hoàn tiền hoàn chỉnh
25. **Mã Giảm Giá**: Hệ thống mã khuyến mãi
26. **Chương Trình Khách Hàng Thân Thiết**: Chương trình giữ chân khách hàng

### Tính Năng Người Bán
27. **Trang Cửa Hàng Cá Nhân**: Gian hàng riêng của từng người bán
28. **Quản Lý Sản Phẩm**: Tải lên và quản lý danh sách sản phẩm
29. **Phân Tích Bán Hàng**: Dashboard hiệu suất bán hàng cơ bản
30. **Hệ Thống Rút Tiền**: Rút tiền thanh toán cho người bán

### Tính Năng Nâng Cao & AI
31. **Live Streaming**: Phiên bán hàng trực tiếp do admin kiểm soát
32. **Tương Tác Live**: Chat và quà tặng ảo trong suốt buổi stream
33. **Gắn Thẻ Sản Phẩm**: Liên kết sản phẩm với live stream
34. **Affiliate Marketing**: Hệ thống giới thiệu và hoa hồng
35. **Gợi Ý AI**: Đề xuất sản phẩm bằng machine learning
36. **Chatbot Hỗ Trợ Khách Hàng**: Hỗ trợ khách hàng tự động

### Tính Năng Quản Trị (Dựa trên 20 Modules Chính)

#### Quản Lý Sản Phẩm & Catalog (37-43)
37. **Quản Lý Thuộc Tính (Attributes)**: Tạo và quản lý thuộc tính sản phẩm (kích thước, màu sắc, chất liệu)
38. **Quản Lý Thương Hiệu (Brands)**: Tạo và quản lý danh sách thương hiệu
39. **Quản Lý Danh Mục (Categories)**: Tổ chức cây danh mục sản phẩm có tính phân cấp
40. **Quản Lý Sản Phẩm (Products)**: CRUD sản phẩm, phê duyệt, featured products
41. **Quản Lý Biến Thể (Variations)**: Quản lý các phiên bản khác nhau của sản phẩm
42. **Quản Lý Tùy Chọn (Options)**: Cấu hình các tùy chọn sản phẩm
43. **Quản Lý Thẻ Tag (Tags)**: Gắn thẻ và phân loại sản phẩm

#### Quản Lý Bán Hàng & Marketing (44-49)
44. **Quản Lý Đơn Hàng (Orders)**: Xử lý đơn hàng, phân công shipper, cập nhật trạng thái
45. **Quản Lý Mã Giảm Giá (Coupons)**: Tạo và quản lý các chương trình khuyến mãi
46. **Quản Lý Flash Sale**: Tạo và điều hành các đợt giảm giá có thời hạn
47. **Quản Lý Đánh Giá (Reviews)**: Kiểm duyệt và quản lý đánh giá sản phẩm
48. **Quản Lý Thuế (Taxes)**: Cấu hình thuế suất theo khu vực
49. **Quản Lý Giao Dịch (Transactions)**: Theo dõi thanh toán, rút tiền, hoàn tiền

#### Quản Lý Nội Dung & Giao Diện (50-53)
50. **Quản Lý Blog**: Tạo và quản lý nội dung tin tức, bài viết
51. **Quản Lý Trang (Pages)**: Tạo các trang tĩnh (About, Contact, Terms)
52. **Quản Lý Menu**: Cấu hình menu điều hướng website
53. **Quản Lý Slider/Banner**: Quản lý banner quảng cáo và slider trang chủ

#### Quản Lý Hệ Thống & Cấu Hình (54-56)
54. **Quản Lý Người Dùng (Users)**: Quản lý tài khoản, phân quyền
55. **Cài Đặt Hệ Thống (Settings)**: Cấu hình chung, thanh toán, vận chuyển
56. **Báo Cáo Tổng Hợp (Reports)**: Dashboard analytics, báo cáo bán hàng, tài chính, người dùng

---

## Luồng Quản Lý Người Dùng

### 1. Đăng Ký & Xác Thực
- **Đăng Ký Đơn Giản**: Đăng ký kiểu Shopee với ít thông tin ban đầu
- **Nâng Cấp Dần**: Yêu cầu thông tin bổ sung khi cần tính năng nâng cao
- **Loại Tài Khoản**: Người tiêu dùng, Admin nhập hàng & bán hàng, Shipper
- **Xác Thực Đa Lớp**: Email/Mạng xã hội
- **Quản Lý Mật Khẩu**: Chức năng quên/đặt lại mật khẩu

### 2. Quản Lý Hồ Sơ & Thông Tin
- **Thông Tin Cơ Bản**: Số điện thoại, địa chỉ, họ tên (lưu trữ khách hàng)
- **Địa Chỉ Giao Hàng**: Quản lý nhiều địa chỉ theo Phường/Xã
- **Giới Hạn Địa Lý**: Chỉ trong tỉnh, chia nhỏ theo khu vực
- **Bảo Mật Tài Khoản**: Thay đổi mật khẩu và cài đặt bảo mật

### 3. Phân Quyền & Vai Trò
- **Super Admin**: Toàn quyền 20 modules, phân công vai trò
- **Admin Nhập Hàng & Bán Hàng**: Quản lý kho, khách hàng, shipper, đơn hàng
- **Quản Lý Đơn Hàng**: Chuyên về orders, reports, shipping
- **Người Bán**: Quản lý sản phẩm & đơn hàng của mình
- **Shipper**: Chỉ cập nhật đơn hàng được giao, báo cáo giao hàng
- **Khách Hàng**: Mua sắm, đánh giá, theo dõi đơn hàng

### 4. Luồng Mua Sắm & Đơn Hàng
- **Khám Phá Sản Phẩm**: Hàng thiết yếu gia dụng + món ăn nấu sẵn
- **Gợi Ý AI**: Đề xuất sản phẩm thông minh
- **Giỏ Hàng & Thanh Toán**: VNPay, ví điện tử, chuyển khoản
- **Theo Dõi Đơn Hàng**: Thời gian thực từ đặt hàng → giao hàng
- **Sau Mua Hàng**: Đánh giá, hoàn tiền, đổi trả

### 5. Hoạt Động Người Bán
- **Thiết Lập Cửa Hàng**: Trang cửa hàng cá nhân
- **Quản Lý Sản Phẩm**: Upload, edit, quản lý kho theo danh mục
- **Quản Lý Thuộc Tính**: Attributes, variations, options, tags
- **Xử Lý Đơn Hàng**: Xác nhận, đóng gói, phân công shipper
- **Phân Tích Bán Hàng**: Dashboard doanh thu, báo cáo
- **Hệ Thống Rút Tiền**: VNPay transfer, ngân hàng, ví điện tử

### 6. Luồng Shipper & Giao Hàng
- **Nhận Đơn**: Được admin/quản lý đơn hàng phân công
- **Cập Nhật Trạng Thái**: Đang lấy hàng → Đang giao → Đã giao
- **Báo Cáo Giao Hàng**: Upload ảnh bằng chứng, ghi chú
- **Xử Lý Vấn Đề**: Báo cáo khách không nhận, địa chỉ sai
- **Dự Kiến Thời Gian**: Cập nhật ETA cho khách hàng

### 7. Luồng Marketing
- **Tương Tác Real-time**: Chat
- **Flash Sale**: Tạo và quản lý đợt giảm giá có thời hạn
- **Mã Giảm Giá**: Coupons

### 8. Luồng Tính Năng Xã Hội
- **Đăng Bài**: Chỉ admin tạo nội dung, khách hàng xem
- **Nhắn Tin**: Chat 1-1 hỗ trợ khách hàng thông qua zalo, facebook

### 9. Luồng Hỗ Trợ & AI
- **Chatbot AI**: Gợi ý món ăn, hỗ trợ đặt hàng
- **Giải Quyết Tranh Chấp**: Hoàn tiền, đổi trả, khiếu nại

### 10. Luồng Quản Trị Hệ Thống
- **Dashboard Analytics**: Tổng quan doanh thu, đơn hàng, user
- **Quản Lý Catalog**: Categories, brands, attributes theo hierarchy  
- **Quản Lý Nội Dung**: Blog, pages, menu, sliders
- **Cài Đặt Hệ Thống**: Payment, shipping
- **Báo Cáo Tổng Hợp**: Sales, financial, inventory, user reports
