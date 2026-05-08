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

###  Khách hàng & Hợp đồng (Mối quan hệ 1-N)
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

    <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/4ea71ba8-f2f9-41f5-a78f-5086a1f67a98" />

### Kết quả từ hình ảnh:
Khách hàng Đỗ Thị B (Mã HĐ 5): Với gốc 5tr và quá hạn từ 01/05, hệ thống đã tính ra tổng nợ là **5,564,039đ** tại ngày 07/05 (Lãi kép)

Nguyễn Văn ABC (Mã HĐ 2): Minh chứng nợ lãi kép dài hạn, từ gốc 5tr vọt lên **9,275,298đ**.

Nguyễn Thị II (Mã HĐ 3): Thể hiện quy tắc 1 hợp đồng - nhiều tài sản (gồm iPhone, Apple Watch, Nhẫn vàng, Giấy tờ xe).
### Trạng thái hợp đồng

- Đang vay
- Quá hạn (nợ xấu)
- Đã thanh toán
- Đã thanh lý tài sản

### Quy tắc trả hàng

- Khách có thể trả nợ từng phần.
- Chỉ được lấy lại tài sản khi:
  - Giá trị các tài sản còn lại >= tổng dư nợ hiện tại.;
    <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/54eb6d48-6105-4370-a1f4-9d0f6d7b9cbc" />
    
Lãi kép (HĐ 2 & 5):** Hệ thống báo ** Quá hạn**. Hợp đồng 2 vay 5tr từ tháng 2, nợ hiện tại đã vọt lên **9,275,298đ**

Rút đồ (HĐ 3):** Nguyễn Thị II có 4 tài sản (53tr) > Dư nợ (16.2tr) nên báo ** Đủ đ/k rút bớt đồ**.

Thanh lý (HĐ 2):** Trạng thái ** Đã thanh lý**, hệ thống dừng tính toán lãi và rút đồ.

Trả nợ gốc (HĐ 1):** Gốc giảm từ 10tr xuống **8,000,000đ**, lãi sẽ giảm theo dư nợ mới.

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

- Vẽ sơ đồ ERD:\
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/5432676e-8ce8-439f-84f3-a0308281e6bc" />

  -Thực thể (Entities): Chính là các bảng như KhachHang, HopDong, TaiSan, LichSuThanhToan.
  
  Thuộc tính (Attributes): Các cột trong bảng như MaKH, TenKH, SoTienVay,....
  
  Mối quan hệ (Relationships): Các đường kẻ nối giữa các bảng thể hiện quan hệ $1:N$ (một-nhiều).
  
  Ví dụ: Một khách hàng có nhiều hợp đồng.
  
  Khóa chính/Khóa ngoại: Có biểu tượng chiếc chìa khóa (PK) và các đường nối thể hiện khóa ngoại (FK)

### Quan hệ dữ liệu

- 1 Khách hàng có thể có nhiều Hợp đồng.
- 1 Hợp đồng có thể cầm cố nhiều Tài sản.
- 1 Hợp đồng phát sinh theo thời gian nhiều lần biến động trạng thái hoặc số tiền nợ.


1. Bảng Khách Hàng (KhachHang)
   
Lưu trữ thông tin định danh và liên lạc duy nhất của từng khách hàng.

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/6cee7902-a043-4e7d-b496-b2d2b71b85c5" />


MaKH (PK): Khóa chính, định danh duy nhất cho mỗi khách hàng.

TenKH: Họ và tên khách hàng.

SDT: Số điện thoại liên lạc.

CCCD: Số Căn cước công dân (Duy nhất).

2. Bảng Hợp Đồng (HopDong)

Quản lý các khoản vay vốn. Chứa khóa ngoại để xác định chủ sở hữu hợp đồng.
   
   <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/a5fa60fe-8653-4124-b2ae-1a7880e3ed4d" />

MaHD (PK): Khóa chính của hợp đồng.

MaKH (FK): Khóa ngoại nối với bảng KhachHang.

SoTienVay: Dư nợ gốc của hợp đồng.

Deadline1: Mốc thời gian quy định lãi suất đơn.

TrangThai: Tình trạng hợp đồng (Đang vay, Quá hạn, Đã tất toán).

3. Bảng Tài Sản (TaiSan)

Quản lý danh sách các món đồ cầm cố. Một hợp đồng có thể cầm cố nhiều tài sản khác nhau.

   <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/ede4f3ea-7cd5-4ca7-8405-479a071b3ac5" />

MaTS (PK): Khóa chính của tài sản.

MaHD (FK): Khóa ngoại nối với bảng HopDong.

TenTS: Tên gọi hoặc mô tả tài sản.

GiaTriDinhGia: Giá trị tài sản sau khi thẩm định.

4. Bảng Nhật Ký Biến Động (LichSuThanhToan)

Mục đích: Theo dõi chi tiết các lần trả nợ từng phần theo thời gian.

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/5b023d40-3d2d-41e4-a120-22a21dd6bc8f" />


MaLog (PK): Khóa chính bản ghi nhật ký.

MaHD (FK): Khóa ngoại nối với bảng HopDong.

NgayTra: Ngày giờ thực hiện thanh toán.

SoTienTra: Số tiền thanh toán thực tế (Gốc/Lãi).

NguoiThu: Tên nhân viên tiếp nhận giao dịch.
## Nhiệm vụ 2: Cài đặt SQL (Yêu cầu viết Scripts)

### Event 1: Đăng ký hợp đồng mới (Vay tiền)

Viết Store Procedure tiếp nhận hợp đồng:

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/cfe3c272-a3e4-4ad0-bbd3-48e998480fc8" />

Lưu thông tin khách hàng (Customer Handling):

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/33464303-3b96-4222-b413-ef20a1508614" />


Sử dụng logic kiểm tra CCCD để phân loại:

Khách mới: Thực hiện INSERT vào bảng KhachHang.

Khách cũ: Tự động lấy MaKH hiện có để liên kết hợp đồng.

Sử dụng SCOPE_IDENTITY() để truy xuất ID vừa tạo, phục vụ nối khóa ngoại (FK).

Quản lý Danh sách tài sản & Định giá (Assets Management):

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/d15fee87-bdd2-41a4-aa38-2cf94beb27cf" />



Tiếp nhận danh sách tài sản thông qua Table-Valued Parameter (@DanhSachTS).

Cho phép một hợp đồng cầm cố nhiều tài sản cùng lúc ($1:N$).

Lưu trữ chi tiết tên tài sản và giá trị định giá thẩm định.Số tiền vay gốc (Principal Amount):

Lưu trữ khoản nợ gốc tại bảng HopDong.Đây là cơ sở dữ liệu đầu vào để hệ thống tính toán lãi đơn và lãi kép dựa trên biến động thời gian thực.

Thiết lập 2 mốc Deadline tự động (Deadlines Setup):

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/a0565f0b-bc20-4b0d-914d-6aafe9daa425" />


Sử dụng hàm DATEADD để tự động hóa hoàn toàn các mốc thời gian quan trọng:Deadline1 (+30 ngày): Hạn chốt tính lãi đơn. Sau ngày này hệ thống tự động chuyển trạng thái tính lãi kép.Deadline2 (+60 ngày): 

Hạn cuối thanh lý tài sản. Nếu hợp đồng chưa tất toán, hệ thống sẽ đánh dấu tài sản sẵn sàng để bán thu hồi vốn.


### Event 2: Tính toán công nợ thời gian thực

Viết Function:

#### fn_CalcMoneyTransaction(TransactionID, TargetDate)

- Tính số tiền phải trả của TransactionID đến ngày TargetDate. Tính số tiền khách đã trả trong 1 giao dịch cụ thể tính đến ngày chốt (TargetDate)
  
  <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/2dd5f4a5-7399-4349-abee-3c23483a3b50" />

Sử dụng điều kiện NgayTra <= @TargetDate.

Nếu ngày khách trả tiền nằm sau ngày chốt, hàm trả về 0.

Nếu ngày khách trả tiền nằm trước hoặc đúng ngày chốt, hàm trả về số tiền thực tế đã trả.

Giúp báo cáo công nợ chính xác tại bất kỳ thời điểm nào trong quá khứ mà không bị lẫn lộn với các giao dịch phát sinh sau đó.

#### fn_CalcMoneyContract(ContractID, TargetDate)

- Tính tổng số tiền khách phải trả. Tính tổng nợ thực tế (Gốc + Lãi) của một hợp đồng tại thời điểm bất kỳ.
  - Gốc

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/b344cdbe-4673-46b7-b9b1-b8a24bb6bb24" />

Tiền gốc: Giá trị vay ban đầu được lấy từ bảng HopDong
  - Lãi đơn

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/1912bdbf-4e60-4da1-aa19-58e549c5c822" />
    

 Lãi đơn: Áp dụng công thức $Gốc + (Gốc \times r \times n)$ cho giai đoạn trong hạn (trước mốc Deadline1).   
  - Lãi kép
    
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/1e0b4667-a1ff-4aff-a758-99826f518310" />

Nếu ngày kiểm tra vượt quá Deadline1, hệ thống dùng hàm POWER để tính lãi kép chồng lên tổng nợ cũ (Gốc + Lãi đơn). Đây là cách tính toán nợ theo cấp số nhân cho giai đoạn quá hạn.



### Event 3: Xử lý trả nợ và hoàn trả tài sản

Viết Store Procedure xử lý khi khách mang tiền đến.

#### Nếu tài sản đã bị thanh lý
(Sau Deadline 2 và có cờ IsSold)

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/c1e2a55a-bdbe-475f-b001-574893dcf99b" />

Trong ảnh: (IF EXISTS): Đóng vai trò là "người gác cổng". Hệ thống sẽ lục soát trong bảng TaiSan xem có món đồ nào của hợp đồng này đã bị bán (IsSold = 1) hay chưa.

(SELECT): Thay vì báo lỗi hệ thống khó hiểu, câu lệnh này xuất ra một cái Bảng thông báo đã thanh lý,  để nhân viên biết rõ lý do từ chối thu tiền.

(ROLLBACK & RETURN): Đây là lệnh bảo mật. ROLLBACK xóa sạch lệnh thu tiền vừa nhập, và RETURN bắt máy tính dừng lại ngay, không chạy tiếp các bước trả đồ hay trừ nợ bên dưới.

Kết quả: bảng LichSuThanhToan không hề tăng thêm tiền, đảm bảo tính an toàn tuyệt đối khi tài sản không còn trong kho.


#### Nếu tài sản chưa bị thanh lý

 Tính tổng nợ
 
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/230e794e-920f-4bdb-b2f1-9c945744efab" />

Lệnh đặc trưng: (@TongGiaTriTaiSan - GiaTriDinhGia) >= @DuNoConLaiGiải thích thực tế: Nhìn vào bảng kết quả thứ 3 trong Ảnh 3, bạn thấy Xe máy Honda và iPhone 15.Hệ thống không chỉ liệt kê tài sản khách đang cầm.Nó tính toán: "Nếu trả lại cái xe máy (25 triệu), thì số đồ còn lại có đủ giá trị để bù cho khoản nợ 8,35 triệu không?".Vì $25.000.000 > 8.350.000$, nên nó hiện ra để gợi ý cho nhân viên biết là "Trả đồ này cho khách vẫn an 

- Trừ số tiền khách trả vào hệ thống.

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/b3ff8a98-2f74-4c19-9352-6e5c1092a956" />

vd: Dòng tiền vào: Bạn truyền vào tham số @SoTienTra = 2.000.000.Xử lý hệ thống: * Hệ thống gọi hàm fn_CalcMoneyContract để biết tổng nợ hiện tại (ví dụ là 10.350.000).Nó thực hiện phép trừ: $10.350.000 - 2.000.000 = 8.350.000$.Kết quả trên màn hình: Tại cột NoConLai, bạn thấy con số 8.350.000. Điều này chứng minh số tiền khách trả đã được trừ vào tổng nợ thành công.Ghi nhận nhật ký (Log): Ngay sau khi trừ, lệnh INSERT INTO LichSuThanhToan sẽ lưu lại con số 2.000.000 này kèm theo dư nợ còn lại để làm bằng chứng thu tiền (như bạn thấy trong bảng Log có 8 dòng ở cuối ảnh)
#### Nếu trả hết tiền
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/1233c59c-09c5-478a-8dc1-62745232bdd9" />


Khi trả hết tiền	Khối IF @DuNoConLai <= 0	Tự động chuyển trạng thái hợp đồng thành "Đã thanh toán đủ" và giải phóng tài sản kho

Nhật ký Giao dịch (Logging)

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/c0440580-eb0d-4e9f-b6f4-fb693f6839ef" />

Ghi nhận: Mọi khoản tiền khách mang đến đều được INSERT vào bảng LichSuThanhToan.

Minh bạch: Việc lưu lại MaHD, NgayTra, SoTienTra giúp chủ tiệm có thể đối soát dòng tiền theo ngày, tránh nhân viên gian lận hoặc nhầm lẫn

### Danh sách gợi ý trả lại tài sản

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/ca16fb3f-bffb-4125-90d8-b5067835024e" />

Điều kiện:
- Giá trị tài sản còn lại >= dư nợ còn lại.

 Đây là phần quan trọng nhất để bảo vệ nguồn vốn của chủ tiệm. Hệ thống chỉ gợi ý trả lại một món đồ cụ thể nếu tổng giá trị định giá của các món đồ còn lại trong kho vẫn đủ lớn hơn hoặc bằng số nợ khách chưa trả xong.

 (Tổng giá trị các tài sản hiện có) - (Giá trị món đồ định trả) >= Dư nợ còn lại.

 Giúp chủ tiệm có thể linh hoạt trả bớt đồ cho khách để giải phóng kho bãi nhưng vẫn giữ lại đủ tài sản có giá trị làm vật thế chấp an toàn cho số nợ còn lại.

 Trong hình ảnh kết quả, khi món đồ 'Xe máy Honda' có IsSold = 1, hệ thống đã xuất bảng CẢNH BÁO và chặn đứng giao dịch thành công theo đúng yêu cầu đề bài. 

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






