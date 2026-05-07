# BT3.VIGHONGMAI

## Thông tin sinh viên

- Họ tên: Vi Hồng Mai
- MSSV: K235480206049
- Môn học: Hệ quản trị cơ sở dữ liệu
- Lớp: 59KMT
- Giảng viên: Đỗ Duy Cốp

---

# BÀI TẬP VỀ NHÀ 03
## THIẾT KẾ VÀ CÀI ĐẶT CSDL QUẢN LÝ CẦM ĐỒ

## 1. Mô tả bài toán

Hệ thống quản lý các hợp đồng vay tiền thế chấp tài sản.

Chức năng chính:
- Quản lý khách hàng
- Quản lý hợp đồng cầm cố
- Quản lý tài sản thế chấp
- Tính lãi đơn và lãi kép
- Xử lý thanh lý tài sản quá hạn

---

## 2. Quy tắc nghiệp vụ

### Khách hàng và tài sản

- Một khách hàng có thể có nhiều hợp đồng cầm cố
- Một hợp đồng có thể bao gồm nhiều tài sản thế chấp

### Cơ chế lãi suất

- Lãi đơn trước Deadline 1:
  - 5.000đ / 1.000.000đ / ngày
- Lãi kép sau Deadline 1:
  - Tính trên gốc + lãi đơn tích lũy

### Trạng thái hợp đồng

- Đang vay
- Quá hạn
- Đã thanh toán
- Đã thanh lý tài sản

### Quy tắc trả hàng

- Khách được trả nợ từng phần
- Chỉ được nhận lại tài sản khi:
  - Giá trị tài sản còn lại >= dư nợ hiện tại

---

## 3. Nhiệm vụ thực hiện

### Thiết kế CSDL

- Vẽ sơ đồ ERD
- Thiết kế bảng dữ liệu
- Chuẩn hóa dữ liệu đến 3NF

### Cài đặt SQL

#### Event 1: Đăng ký hợp đồng mới

- Tạo Store Procedure lưu:
  - Thông tin khách hàng
  - Danh sách tài sản
  - Giá trị định giá
  - Số tiền vay
  - Deadline 1 và Deadline 2

#### Event 2: Tính công nợ

- Function tính tiền theo giao dịch
- Function tính tổng nợ hợp đồng
- Hỗ trợ tính lãi kép

#### Event 3: Xử lý trả nợ

- Cập nhật số tiền trả
- Ghi log thanh toán
- Cập nhật trạng thái hợp đồng
- Gợi ý tài sản được trả lại

#### Event 4: Danh sách nợ xấu

Hiển thị:
- Tên khách hàng
- Số điện thoại
- Số ngày quá hạn
- Tổng tiền hiện tại
- Tổng tiền sau 1 tháng

#### Event 5: Trigger tự động

- Chuyển trạng thái quá hạn
- Chuyển trạng thái thanh lý
- Cập nhật trạng thái tài sản

---

## 4. Chức năng bổ sung

### Gia hạn hợp đồng

- Khách trả lãi để gia hạn deadline

### Audit Log

- Lưu lịch sử trả tiền
- Theo dõi người thu tiền
- Theo dõi số tiền còn nợ

---

## 5. File bài tập

- File báo cáo PDF
- File script SQL
- README.md
- Ảnh minh họa quá trình làm bài

### Link file PDF

[📄 Xem file PDF](btvn03_VHM.pdf)

---

## 6. Hạn nộp bài

23:59:59 ngày 12/05/2026
vết dòng tiền.

