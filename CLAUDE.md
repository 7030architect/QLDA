# Quy ước dự án QLDA – Cải tạo Tầng 2 nhà phố (Phú Nhuận, TP.HCM)

## Quy ước chung
- **Tầng trệt = Tầng 1**, sau đó đến Tầng 2, Tầng 3. Chỉ cải tạo **Tầng 2**.
- Trao đổi và hồ sơ viết bằng tiếng Việt.
- Trục và lưới theo bản vẽ `ban-ve/MB-hien-trang-va-phuong-an.pdf`. Chiều cao tầng 2 là 3 m. "Sân trước" là Sân trục 5–6 (18 m², nằm trên hiệu thuốc).

## Ràng buộc thi công
- Tầng 1 mặt tiền cho thuê làm hiệu thuốc. Lối lên Tầng 2 phải đi qua hiệu thuốc; ban ngày được đi nhưng hạn chế.
- Xà bần phải đóng bao. **Chở xà bần ra chỉ được làm sau 22h.** Vật tư chở vào không bị giới hạn giờ.
- Mục tiêu: xong phá dỡ, xây mới, hoàn thiện trước 30/01/2027 (23 tháng Chạp). Nội thất và thiết bị làm sau Tết.

## File báo giá `bao-gia/Tu-house_baogia_261126.xlsx`
- Cấu trúc: Bia → THop (tổng hợp) → Prelim / Fit / Mep.
- Thành tiền luôn là công thức `=M*L`, không nhập tay. Tổng nhóm và tổng sheet dùng `SUBTOTAL(9,…)`. THop C18/C20/C24 tham chiếu dòng tổng của từng sheet, nên khi thêm hoặc bớt dòng phải cập nhật lại.
- **Đơn giá:** chủ nhà/nhà thầu tự điền và gửi lại. Sau khi có bộ đơn giá đó, Claude được **chủ động điền đơn giá** cho các hạng mục mới, dựa trên bộ đơn giá đã được xác nhận.
- Sau mỗi lần sửa: tính lại bằng LibreOffice, kiểm tra không có ô lỗi `#...`, xem bản PDF để kiểm tra dòng không bị tràn chữ.
