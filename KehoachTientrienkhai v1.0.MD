# Kế hoạch tiền triển khai (Pre-Launch Plan) cho MVP ứng dụng hỗ trợ chữa cháy và sơ cứu

Tôi đề xuất phát triển MVP theo triết lý **"Tối thiểu nhưng hữu ích"**: tập trung vào việc giúp người dùng **tìm nguồn lực cứu hộ gần nhất và nhận hướng dẫn xử lý ban đầu trong vòng 30–60 giây**.

---

# 1. Mục tiêu MVP

## Mục tiêu kinh doanh

* Chứng minh nhu cầu thị trường.
* Thu hút 5.000–10.000 người dùng đầu tiên.
* Thu thập phản hồi để cải tiến sản phẩm.
* Tạo nền tảng dữ liệu ban đầu cho các phiên bản sau.

## Mục tiêu kỹ thuật

* Ứng dụng Android/iOS hoạt động ổn định.
* Thời gian tải bản đồ < 3 giây.
* Tìm kiếm địa điểm gần nhất trong < 2 giây.
* Tỷ lệ crash < 1%.

---

# 2. Phạm vi MVP

## Chức năng đưa vào

### 2.1 Bản đồ

* Hiển thị vị trí hiện tại.
* Phóng to/thu nhỏ.
* Tìm kiếm địa chỉ.
* Dẫn đường bằng ứng dụng bản đồ trên thiết bị.

### 2.2 Hiển thị các điểm quan trọng

* 🚒 Trạm chữa cháy.
* 🏥 Bệnh viện.
* 🚑 Cơ sở cấp cứu.
* 💧 Trụ nước chữa cháy (nếu có dữ liệu).
* 🧯 Bình chữa cháy công cộng hoặc do đối tác cung cấp (nếu có).

### 2.3 Tìm điểm gần nhất

Ví dụ:

```
Bạn đang ở:
Số 12 Nguyễn Chí Thanh

Điểm gần nhất:
-------------------------
🚒 Trạm PCCC      650m
🏥 Bệnh viện      1.2km
💧 Trụ nước       280m
🧯 Bình chữa cháy 90m
```

### 2.4 Hướng dẫn xử lý nhanh

Bao gồm:

* Cháy điện.
* Cháy xăng dầu.
* Cháy trong chung cư.
* Cháy xe máy.
* Cháy ô tô.
* Cách sử dụng bình chữa cháy.

### 2.5 Hướng dẫn sơ cứu cơ bản

* Đuối nước.
* Điện giật.
* Chảy máu.
* Bỏng.
* Người bất tỉnh.
* Hóc dị vật.

### 2.6 Gọi hỗ trợ nhanh

Một nút duy nhất:

* Gọi số khẩn cấp phù hợp.
* Chia sẻ vị trí hiện tại cho người thân (nếu người dùng đã thiết lập).

---

# 3. Chức năng chưa đưa vào MVP

* AI nhận diện cháy qua camera.
* Báo cháy cộng đồng theo thời gian thực.
* Quản lý QR cho bình chữa cháy.
* Chatbot AI hướng dẫn.
* Cảnh báo theo vùng.
* Đồng bộ với camera IoT.
* Quản lý tòa nhà.
* Gamification.

---

# 4. Kiến trúc hệ thống

```text
          Mobile App
         (Flutter)

             │
        REST / GraphQL API
             │
     -----------------------
     |                     |
Backend Service      Authentication
     |
Spatial Database
(PostgreSQL + PostGIS)

     |
Geospatial Data
- Fire stations
- Hospitals
- Hydrants
- Fire extinguishers
```

---

# 5. Thiết kế màn hình

## Trang chủ

```
------------------------
🔍 Tìm kiếm

🗺️ Bản đồ

📍 Tôi đang ở đây

[🚒] [🏥] [🧯] [💧]

-------------
HƯỚNG DẪN NHANH

🔥 Cháy

⚡ Điện giật

🌊 Đuối nước

🩸 Chảy máu

❤️ CPR

-------------
SOS
```

---

## Trang sự cố "Cháy điện"

```
⚠️ Cháy điện

Bước 1:
Ngắt nguồn điện nếu có thể thực hiện an toàn.

↓

Bước 2:
Không dùng nước để dập lửa.

↓

Bước 3:
Sử dụng bình chữa cháy phù hợp nếu đã được huấn luyện.

↓

Bước 4:
Rời khỏi khu vực nếu đám cháy vượt khả năng kiểm soát.

↓

☎️ Gọi hỗ trợ khẩn cấp.
```

---

# 6. Dữ liệu cần chuẩn bị

## Giai đoạn đầu

| Dữ liệu            | Nguồn                                                               |
| ------------------ | ------------------------------------------------------------------- |
| Trạm chữa cháy     | Dữ liệu công khai hoặc đối tác cung cấp                             |
| Bệnh viện          | Dữ liệu công khai                                                   |
| Cơ sở cấp cứu      | Dữ liệu công khai                                                   |
| Trụ nước chữa cháy | Thu thập hoặc đối tác cung cấp                                      |
| Bình chữa cháy     | Ban đầu có thể do cộng đồng hoặc đối tác bổ sung và được kiểm chứng |

---

# 7. Roadmap 12 tuần

| Tuần | Công việc                                               |
| ---- | ------------------------------------------------------- |
| 1    | Xác định yêu cầu, thiết kế UI/UX, mô hình dữ liệu       |
| 2    | Thiết kế cơ sở dữ liệu và API                           |
| 3    | Tích hợp bản đồ và định vị                              |
| 4    | Hiển thị trạm chữa cháy, bệnh viện                      |
| 5    | Thêm lớp dữ liệu trụ nước và bình chữa cháy             |
| 6    | Tìm kiếm, lọc và dẫn đường                              |
| 7    | Xây dựng thư viện hướng dẫn chữa cháy                   |
| 8    | Xây dựng thư viện sơ cứu cơ bản                         |
| 9    | Hoàn thiện màn hình SOS và chia sẻ vị trí               |
| 10   | Kiểm thử chức năng, sửa lỗi                             |
| 11   | Thử nghiệm với nhóm người dùng nhỏ, tối ưu hiệu năng    |
| 12   | Chuẩn bị phát hành phiên bản beta và tài liệu hướng dẫn |

---

# 8. Nhân sự tối thiểu

| Vai trò                                      | Số lượng |
| -------------------------------------------- | -------- |
| Product Manager                              | 1        |
| UI/UX Designer                               | 1        |
| Lập trình Mobile                             | 1–2      |
| Backend Developer                            | 1        |
| QA/Tester                                    | 1        |
| Chuyên gia nội dung sơ cứu & PCCC (cộng tác) | 1        |

Nhóm 5–7 người là đủ để xây dựng MVP trong khoảng 3 tháng.

---

# 9. Ước tính chi phí (tham khảo)

| Hạng mục                          | Chi phí dự kiến      |
| --------------------------------- | -------------------- |
| Thiết kế UI/UX                    | 20–40 triệu VNĐ      |
| Phát triển Mobile                 | 80–150 triệu VNĐ     |
| Backend & API                     | 60–120 triệu VNĐ     |
| Kiểm thử                          | 20–40 triệu VNĐ      |
| Hạ tầng (cloud, bản đồ, giám sát) | 5–15 triệu VNĐ/tháng |
| Nội dung chuyên môn và pháp lý    | 20–50 triệu VNĐ      |

Tổng chi phí MVP thường nằm trong khoảng **200–400 triệu VNĐ** nếu thuê đội ngũ trong nước, chưa bao gồm chi phí thu thập dữ liệu quy mô lớn.

# 10. Ba đề xuất chiến lược để tăng khả năng thành công

## A. Tập trung vào khu vực thí điểm

Thay vì triển khai toàn quốc ngay từ đầu, hãy chọn một địa bàn như một quận ở Hà Nội hoặc TP.HCM để xây dựng dữ liệu chất lượng cao và kiểm chứng mô hình.

## B. Xây dựng cơ chế dữ liệu nhiều tầng

Phân loại rõ:

* **Dữ liệu đã xác minh** (cơ quan, đối tác hoặc kiểm duyệt nội bộ).
* **Dữ liệu do cộng đồng đóng góp** (chưa hoặc đang xác minh).
* **Dữ liệu đang chờ rà soát**.

Điều này giúp tăng độ tin cậy và minh bạch.

## C. Ưu tiên trải nghiệm trong 30 giây đầu

Người dùng khi mở ứng dụng trong tình huống khẩn cấp nên có thể ngay lập tức:

1. Xem vị trí của mình trên bản đồ.
2. Tìm được trạm chữa cháy hoặc bệnh viện gần nhất.
3. Mở hướng dẫn xử lý phù hợp chỉ với 1–2 thao tác.
4. Gọi hỗ trợ hoặc chia sẻ vị trí nhanh chóng.

Với định hướng này, MVP có thể tạo ra giá trị thực tế ngay cả trước khi tích hợp các tính năng nâng cao như AI, cảnh báo cộng đồng hay quản lý thiết bị cứu hỏa. Điều đó cũng giúp giảm rủi ro phát triển và tạo nền tảng vững chắc cho các giai đoạn tiếp theo.
