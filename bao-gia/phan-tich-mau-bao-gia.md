# Phân tích file báo giá mẫu `Tu-house_baogia_261126.xlsx` (bản gốc xem lịch sử git)

## Cấu trúc

| Sheet | Vai trò | Liên kết |
|---|---|---|
| **Bia** | Bìa phụ lục báo giá | Lấy tên công ty, SĐT, dự án, hạng mục, mã số, số báo giá từ THop |
| **THop** | Tổng hợp báo giá | A = Prelim!N12, B = Fit!N18, C = Nội thất (trống), D = Mep!N24. Cộng và làm tròn đến triệu trước VAT |
| **Prelim** | Công tác chuẩn bị, phá dỡ | Bảng khối lượng chi tiết |
| **Fit** | Thi công thô và hoàn thiện | Bảng khối lượng chi tiết |
| **Mep** | Điện nước và thiết bị | Bảng khối lượng chi tiết |

Các sheet chi tiết dùng chung một bố cục:

| Cột | A | C | D | E | F–J | K | L | M | N | O |
|---|---|---|---|---|---|---|---|---|---|---|
| Nội dung | STT | Hạng mục | Hình ảnh | Mô tả vật liệu | Kích thước (ẩn bớt) | Đơn vị | Khối lượng | Đơn giá | Thành tiền | Ghi chú |

Tổng các sheet dùng `SUBTOTAL(9,…)`.

## Giá trị hiện tại (sau khi tính lại)

| Phần | Giá trị |
|---|---|
| A. Chuẩn bị | 1.300.000 |
| B. Thô và hoàn thiện | 20.964.000 |
| C. Nội thất | 0 |
| D. M&E | 5.000.000 (phần thiết bị đang = 0) |
| Cộng | 27.264.000 |
| Làm tròn trước VAT | 27.000.000 |

## Lỗi và điểm cần sửa

### Lỗi công thức và số liệu
1. **Prelim N9 = 1.300.000 nhập tay**, trong khi M9×L9 = 1.200.000. Thành tiền không khớp với đơn giá.
2. **Mep N9 = 5.000.000 nhập tay**, trong khi M9×L9 = 4.000.000. Cũng không khớp.
3. **Mep N10 và N12–N23 không có công thức** nên toàn bộ phần Thiết bị (khoảng 10,7 triệu nếu tính theo đơn giá đang có) **không được cộng vào tổng**.
4. **Fit: các mục 6 (cửa phòng, cửa sổ), 7 (cửa WC), 9 (gác lửng) chưa có đơn giá** nên đang tính bằng 0.
5. **Prelim mục 2 và 3** chưa có đơn giá, chưa có công thức.
6. **Bìa (Bia) lấy sai ô:** F12, F13, F17 tham chiếu THop!D9, D10, D11, nhưng các ô này trống. Nội dung thật đang nằm chung chuỗi chữ ở cột C. E18 tham chiếu THop!E1 (số báo giá) cũng trống, nên bìa hiện trống hoặc hiện "0".
7. **THop E2 = TODAY()**: ngày báo giá tự đổi mỗi lần mở file. Nên nhập ngày cố định.
8. Có 16 tên vùng (named range) bị lỗi `#REF!`, sót lại từ mẫu cũ. Chúng không ảnh hưởng kết quả, có thể xóa.

### Nội dung còn sót từ dự án hoặc mẫu cũ
- Tiêu đề khu vực ghi **"TẦNG TRỆT"**, cần đổi thành **"TẦNG 2"**.
- Prelim có các dòng bằng tiếng Anh (gypsum partition, backdoor, tarpaulin). Phần mô tả ở cả 3 dòng bị chép giống nhau.
- Fit mục 5 ghi "WC shop". Mep mục 1 ghi chú "đồng hồ riêng từng phòng chdv" (căn hộ dịch vụ).
- Tên phần B ghi "THI CÔNG THÔ / FIT-OUT WORKS", còn tiêu đề sheet Fit lại ghi "Trang trí nội thất". Hai tên không thống nhất.

## Đề xuất cho dự án này

- **Prelim** bổ sung các dòng theo kế hoạch phá dỡ:
  - che chắn lối đi qua hiệu thuốc và cầu thang;
  - cô lập điện nước Tầng 2;
  - phá dỡ theo từng hạng mục (gạch, trần, tường, thiết bị…);
  - đóng bao xà bần;
  - **vận chuyển ban đêm sau 22h** (tính theo chuyến, gồm công vác từ Tầng 2 xuống);
  - vệ sinh hằng ngày.
- **Nội thất (phần C)**: để trống ở báo giá đợt này, vì nội thất và thiết bị làm sau Tết. Cân nhắc tách thiết bị (Mep phần B) sang báo giá đợt 2 nếu lắp sau Tết.
- Ghi chú chung bổ sung: tiến độ hoàn thành trước 30/01/2027, ràng buộc giờ vận chuyển, trách nhiệm với hiệu thuốc.

## Đã sửa (26/11/2026)

- [x] Prelim N9–N11, Mep N9, N10, N12–N23: thành tiền tính bằng công thức `=M*L`.
- [x] THop: tách nhãn và giá trị (D9 dự án, D10 hạng mục, D12 địa điểm) để bìa hiển thị đúng. Ngày báo giá cố định 26/11/2026.
- [x] Bìa: địa điểm và số báo giá lấy từ THop, không còn hiện "0" khi ô trống.
- [x] Đổi "TẦNG TRỆT" thành "TẦNG 2". Việt hóa các dòng Prelim. Bỏ ghi chú "shop" và "chdv". Thống nhất tên phần B.
- [x] Phần C Nội thất ghi "Thực hiện giai đoạn 2 (sau Tết)".
- [x] Xóa 16 tên vùng lỗi `#REF!`.
- [ ] Chưa có đơn giá: Fit mục 6, 7, 9 (cửa Xingfa, cửa WC, gác lửng). Chủ nhà sẽ cung cấp.

Tổng sau khi sửa: A 1.200.000 · B 20.964.000 · D 14.710.000 (M&E 5.750.000 + thiết bị 8.960.000) → **37.000.000 trước VAT**.
