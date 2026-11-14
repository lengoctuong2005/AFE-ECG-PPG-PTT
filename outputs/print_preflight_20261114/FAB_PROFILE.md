# Profile kiểm PCB trần, tra ngày 14/11/2026

Profile tham chiếu: [JLCPCB PCB capabilities](https://jlcpcb.com/capabilities/pcb-capabilities). Đây là đối chiếu bảng năng lực công khai, không phải báo giá, xác nhận đơn hàng hoặc phê duyệt CAM. Nếu chọn xưởng khác phải đối chiếu lại.

## Cấu hình đề xuất cho prototype

PCB trần 2 lớp FR-4, 92 × 70 mm, dày danh định 1,6 mm, copper thành phẩm 1 oz, soldermask xanh, silkscreen trắng, outline routed không V-score. Đề xuất ENIG để thuận lợi mặt phẳng hàn IC LFCSP/VSSOP pitch 0,5 mm; chưa có báo giá nên không cam kết ngân sách. Không đặt PCBA tự động theo BOM/CPL hiện tại. Stencil top là lựa chọn lắp phù hợp cần thỏa thuận thickness/aperture với người hàn hoặc xưởng, không tự chốt profile.

## Đối chiếu

| Mục | Bảng năng lực tham chiếu | Thiết kế sau kiểm ngày 14/11/2026 |
|---|---|---|
| 1 oz track/space | 0,10/0,10 mm cho 1–2 lớp | Track ≥0,20 mm, clearance dự án 0,20 mm |
| Drill | Bảng hỗ trợ nhỏ hơn 0,30 mm, tùy chi phí/quy trình | Via 0,60/0,30 mm, 38 via |
| PTH annular ring 1 oz hai lớp | Recommended 0,25 mm, absolute min 0,18 mm | Minimum đo pad-through-hole 0,35 mm; via ring 0,15 mm theo mục via riêng |
| Plated slot | Width ≥0,5 mm, length ≥2×width | Jack có 3 slot danh định 2 × 1 mm, ở ranh tỷ lệ 2:1; yêu cầu CAM xác nhận slot/PTH |
| Copper tới routed edge | ≥0,20 mm | Rule dự án 0,50 mm |
| Mask expansion | Cho phép 1:1; khoảng tới trace lân cận ≥0,09 mm | Expansion 0; phải xem chính mask xuất và CAM |
| Mask bridge xanh 1 oz | 0,10 mm | Rule web 0,10 mm |
| Legend height/line/pad distance | 1,0 mm / 0,15 mm / 0,15 mm | Đã chỉnh text ≥1,0/0,15 mm, graphic ≥0,15 mm; kiểm tạm min_silk_clearance 0,15 mm đạt 0 lỗi, rules điện nguồn không đổi |
| Board size/thickness | Hỗ trợ 92 × 70 mm, 1,6 mm trong dải công khai | Cấu hình này không đòi panel HDI/microvia |

Không chọn plugged/filled via chỉ vì CAD tented; tenting, plugging và filled-capped khác nhau. Yêu cầu xưởng giữ mask theo Gerber, review via gần pad và vùng pin 1/EP. Text quá nhỏ hoặc silk bị sửa bởi CAM cần được xác nhận trước chấp thuận.

## Xác nhận với xưởng trước thanh toán

- Preview nhận đúng 92 × 70 mm, 2 lớp và outline kín.
- Có 90 feature khoan/slot: 38 via 0,3 mm, 48 lỗ/slot tool 1 mm gồm 3 slot J1, 4 lỗ M3 3,2 mm có mạ. NPTH file rỗng có chủ ý.
- Giữ ba slot J1 đúng hướng, đúng đơn vị/origin; không chuyển lỗ M3 thành NPTH khi chưa chấp thuận.
- Review mask/EP/paste/legend và tenting; không thay net, không xóa đồng hoặc khoan theo đề xuất CAM mà chưa kiểm lại.
- Bare-board electrical test theo netlist và phạm vi xưởng xác nhận. Không giả đã được kiểm chỉ vì có file xuất.

Giá, thời gian giao hàng, quantity, finish cuối cùng và khả năng lắp phải xem tại đơn hàng thực. Gói chỉ để gửi review chế tạo prototype, không chứng minh an toàn tiếp xúc cơ thể hay mạch hoạt động.
