# BT3.VIGHONGMAI

## Thông tin sinh viên

- Họ tên: Vi Hồng Mai
- MSSV: K235480206049
- Môn học: Hệ quản trị CSDL
- Lớp: 59KMT
- Giảng viên: Đỗ Duy Cốp

# BÀI TẬP VỀ NHÀ 03: THIẾT KẾ VÀ CÀI ĐẶT CSDL QUẢN LÝ CẦM ĐỒ

## 1. Mô tả bài toán

Hệ thống cần quản lý các hợp đồng vay tiền thế chấp tài sản. Điểm đặc thù của hệ thống là cơ chế tính lãi linh hoạt, quản lý danh mục tài sản thế chấp và xử lý thanh lý đồ khi quá hạn.

## 2. Các quy tắc nghiệp vụ

### Khách hàng & Tài sản

- Một khách hàng có thể có nhiều hợp đồng cầm cố.
- Một hợp đồng có thể bao gồm nhiều tài sản thế chấp khác nhau.

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/5300ae4e-6bb6-42d7-86dd-cbc9a770efa1" />

 Mối quan hệ giữa các thực thể trong CSDL

Hệ thống được thiết kế để giải quyết các quy tắc nghiệp vụ sau:

 **Khách hàng & Hợp đồng (Mối quan hệ 1-N)
* **Đoạn thể hiện:** Ràng buộc `FK_HopDong_KhachHang` trong bảng `HopDong`.
 Một khách hàng có thể có nhiều hợp đồng cầm cố khác nhau. Khóa ngoại `MaKH` trong bảng `HopDong` đảm bảo mọi hợp đồng đều thuộc về một khách hàng cụ thể và cho phép một khách hàng mở nhiều khoản vay theo thời gian.
### Hợp đồng & Tài sản (Mối quan hệ 1-N)
* **Đoạn thể hiện:** Ràng buộc `FK_TaiSan_HopDong` trong bảng `TaiSan`.
 Một hợp đồng có thể bao gồm nhiều tài sản thế chấp khác nhau. Điều này cho phép khách hàng dùng nhiều món đồ (ví dụ: xe máy và điện thoại) để đảm bảo cho cùng một khoản vay. Tất cả tài sản này đều liên kết với một mã hợp đồng (`MaHD`) duy nhất, hỗ trợ việc quản lý và trả đồ từng phần.



### Cơ chế lãi suất

#### Lãi đơn (Trước Deadline 1)

- 5.000đ / 1.000.000đ gốc / ngày.

#### Lãi kép (Từ sau Deadline 1)

- Lãi được tính dựa trên:
  - Gốc + lãi đơn đã tích lũy.

### Trạng thái hợp đồng

- Đang vay
- Quá hạn (nợ xấu)
- Đã thanh toán
- Đã thanh lý tài sản

### Quy tắc trả hàng

- Khách có thể trả nợ từng phần.
- Chỉ được lấy lại tài sản khi:
  - Giá trị các tài sản còn lại >= tổng dư nợ hiện tại.

## 3. Chức năng chính của hệ thống

### 1. Quản lý khách hàng

- Lưu thông tin khách hàng:
  - Họ tên
  - Số điện thoại
  - CCCD
  - Địa chỉ
- Theo dõi lịch sử vay của khách hàng.

### 2. Quản lý hợp đồng cầm cố

- Tạo hợp đồng vay mới.
- Cập nhật trạng thái hợp đồng.
- Theo dõi thời hạn thanh toán.
- Gia hạn hợp đồng.

### 3. Quản lý tài sản thế chấp

- Lưu danh sách tài sản cầm cố.
- Định giá tài sản.
- Theo dõi trạng thái tài sản:
  - Đang cầm cố
  - Đã trả khách
  - Sẵn sàng thanh lý
  - Đã bán thanh lý

### 4. Quản lý công nợ

- Tính lãi đơn.
- Tính lãi kép.
- Tính tổng số tiền cần thanh toán.
- Theo dõi dư nợ hiện tại.

### 5. Xử lý thanh toán

- Khách hàng trả nợ từng phần.
- Ghi nhận lịch sử thanh toán.
- Cập nhật số tiền còn nợ.
- Hoàn trả tài sản khi đủ điều kiện.

### 6. Quản lý nợ xấu

- Danh sách khách hàng quá hạn.
- Tính số ngày quá hạn.
- Thống kê tổng nợ hiện tại.
- Dự đoán số nợ sau thời gian tiếp theo.

### 7. Quản lý thanh lý tài sản

- Tự động chuyển trạng thái quá hạn.
- Đưa tài sản sang trạng thái thanh lý.
- Cập nhật trạng thái đã bán thanh lý.

### 8. Audit Log

- Lưu lịch sử giao dịch.
- Theo dõi người thu tiền.
- Theo dõi thời gian thanh toán.
- Theo dõi biến động số dư.

## 4. Nhiệm vụ cụ thể của sinh viên
### Nhiệm vụ 1: Thiết kế CSDL

- Vẽ sơ đồ ERD:
  - Thể hiện rõ thực thể
  - Thuộc tính
  - Khóa chính
  - Khóa ngoại

- Chuyển sơ đồ thành các bảng.
- Chuẩn hóa tối thiểu mức 3NF.

### Quan hệ dữ liệu

- 1 Khách hàng có thể có nhiều Hợp đồng.
- 1 Hợp đồng có thể cầm cố nhiều Tài sản.
- 1 Hợp đồng phát sinh theo thời gian nhiều lần biến động trạng thái hoặc số tiền nợ.

## Nhiệm vụ 2: Cài đặt SQL (Yêu cầu viết Scripts)

### Event 1: Đăng ký hợp đồng mới (Vay tiền)

Viết Store Procedure tiếp nhận hợp đồng:
- Lưu thông tin khách hàng.
- Danh sách tài sản.
- Giá trị định giá.
- Số tiền vay gốc.
- Thiết lập 2 mốc:
  - Deadline1
  - Deadline2

### Event 2: Tính toán công nợ thời gian thực

Viết Function:

#### fn_CalcMoneyTransaction(TransactionID, TargetDate)

- Tính số tiền phải trả của TransactionID đến ngày TargetDate.

#### fn_CalcMoneyContract(ContractID, TargetDate)

- Tính tổng số tiền khách phải trả:
  - Gốc
  - Lãi đơn
  - Lãi kép

Gợi ý:
- Sử dụng hàm tính lũy thừa hoặc vòng lặp để xử lý lãi kép.

### Event 3: Xử lý trả nợ và hoàn trả tài sản

Viết Store Procedure xử lý khi khách mang tiền đến.

#### Nếu tài sản đã bị thanh lý
(Sau Deadline 2 và có cờ IsSold)

- Thông báo không thu tiền.
- Không trả đồ.

#### Nếu tài sản chưa bị thanh lý

- Tính tổng nợ.
- Trừ số tiền khách trả vào hệ thống.

#### Nếu trả hết tiền

- Trả hết đồ.
- Cập nhật trạng thái hợp đồng:
  - Đã thanh toán đủ.

#### Nếu chưa trả hết tiền gốc + lãi

- Cập nhật trạng thái hợp đồng:
  - Đang trả góp.

- Ghi nhận vào LOG:
  - Số tiền đã trả.
  - Số tiền còn nợ.

### Danh sách gợi ý trả lại tài sản

Điều kiện:
- Giá trị tài sản còn lại >= dư nợ còn lại.

### Event 4: Truy vấn danh sách nợ xấu (Nợ khó đòi)

Xuất danh sách các khách hàng:
- Đã quá Deadline 1.
- Chưa thanh toán.

### Các cột yêu cầu

- Tên KH
- Số điện thoại
- Số tiền vay gốc
- Số ngày quá hạn
- Tổng tiền phải trả hiện tại
- Tổng số tiền phải trả sau 1 tháng

Gợi ý:
- Nên viết Function hỗ trợ.

### Event 5: Quản lý thanh lý tài sản

#### Trigger 1

Tự động chuyển trạng thái hợp đồng sang:
- Quá hạn (nợ xấu)

Điều kiện:
- Hợp đồng đang ở trạng thái "Đang vay"
- Ngày vượt quá Deadline 1

#### Trigger 2

Tự động chuyển trạng thái tài sản sang:
- Sẵn sàng thanh lý

Điều kiện:
- Hợp đồng đang ở trạng thái "Quá hạn (nợ xấu)"
- Ngày vượt quá Deadline 2

#### Tự động chuyển trạng thái tài sản thành:
- Đã bán thanh lý

Điều kiện:
- Trạng thái hợp đồng chuyển sang:
  - Đã thanh lý

### Trạng thái tài sản

- Đang cầm cố
- Đã trả khách
- Đã bán thanh lý

## 5. Các sự kiện bổ sung

### Gia hạn hợp đồng

Khách đến trả toàn bộ tiền lãi tính đến thời điểm hiện tại để:
- Dời Deadline 1
- Dời Deadline 2
- Tránh bị tính lãi kép

### Lịch sử hợp đồng (Audit Log)

CSDL cần có bảng Log để ghi lại:
- Ngày trả
- Số tiền trả
- Người thu tiền

Mục đích:
- Tránh việc ghi đè số tổng nợ
- Theo dõi lịch sử dòng tiền






