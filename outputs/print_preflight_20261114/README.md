# Gói kiểm trước đặt PCB trần, 14/11/2026

## Phạm vi bàn giao

PCB prototype 92 × 70 mm, hai lớp, bench với tín hiệu giả lập. Nguồn CAD gốc đã cập nhật legend dễ đọc hơn; tracks, pad/net, footprint placement, bốn return GND mới, nguồn 2,8 V và rules giữ nguyên so với baseline. Không thay firmware. Không phải hồ sơ PCBA hàng loạt, không chứng minh mạch hoạt động hay an toàn dùng trên người.

**File gửi CAM:** `GERBER_ONLY_92x70_NOT_CAM_APPROVED.zip`. Có đúng 11 file cấp gốc: 9 Gerber và 2 Excellon, không PDF/README/BOM/build. `.gbrjob` nằm ngoài ZIP. Không dùng ZIP các revision trước.

## Kiểm đã làm

- KiCad 10.0.8 DRC sau refill/save, mọi severity, all-track-errors, schematic parity: 0 violation, 0 unconnected, 0 parity; ignored DRC rỗng.
- ERC 0, vẫn ghi hai kiểm không áp dụng: SPICE và global label chỉ xuất hiện một lần.
- Kiểm tạm profile min_silk_clearance 0,15 mm đạt 0 lỗi; không đổi file rules nguồn 0,1 mm để giả đã thay toàn bộ profile.
- 46 ref visible cao 1,0 mm, nét 0,15 mm; 2 dòng cảnh báo cùng kích thước; graphic silkscreen nhỏ được tăng lên 0,15 mm. Chỉ dời reference TP3/C11 và hai cảnh báo để tránh cấn. Pin 1 và pad geometry không thay.
- 46 footprint, 151 node, outline 92 × 70 mm, hai keepout anten và return GND đúng kiểm regression.
- 90 lỗ/slot khớp PCB trong 0,0011 mm: 38 via drill 0,3 mm; 48 lỗ/slot tool 1 mm gồm 3 slot J1; 4 lỗ M3 3,2 mm có mạ. NPTH file rỗng là chủ ý.
- ZIP: inventory, CRC và byte từng member khớp thư mục `gerbers/`. Manifest ghi hash nguồn/output.
- Gerber/drill top/bottom/mask/paste đã render bằng gerbv 2.10.0 độc lập. Viewer bỏ qua X2 metadata và có cảnh báo lớp rỗng/mask region không aperture; toàn bộ giữ trong `gerbv_logs.json`, không chỉnh Gerber để che warning.

## Cách đặt

Đọc `FAB_PROFILE.md` và `DAT_PCB_TRAN.md`. Profile tham chiếu JLCPCB, chưa phải order/CAM approval. Đề xuất FR-4 1,6 mm, 1 oz, green mask/white legend, ENIG, routed outline. Xem báo giá thực, không có cam kết giá hoặc giao hàng. Không chọn via filled/plugged khi chỉ cần tented.

In `Assembly_1to1.pdf` ở actual size 100% và đối chiếu đúng DevKitC V4, hai socket cách tâm 25,4 mm, jack SJ1-3533NG, TRS plug và trụ M3. J3 dùng dây tới PPG rời; pin 2 SCL, pin 3 SDA, không đảo theo lời mô tả ngoài.

## Các cổng chưa đóng

1. Trước thanh toán: xác nhận preview xưởng đúng kích thước/lớp, slot/mạ/origin, mask/legend, tenting và thay đổi CAM; mẫu module/jack/plug/vỏ chưa được kiểm thực.
2. Trước lắp/cấp nguồn: C10 phải có MPN và effective C ≥1 µF, ESR 0–2 Ω theo điều kiện MCP1700; tương thích LOD 2,8→3,3 V còn thiếu worst-case; module PPG cần xác nhận pinout/nguồn/level-shift/pull-up/INT.
3. Sau lắp: kiểm nguồn hạn dòng và tín hiệu giả lập, analog/RF/timing. PAT live vẫn khóa. Dùng pin không cho phép bỏ đánh giá an toàn tiếp xúc cơ thể.

Baseline và candidate giữ trong hai thư mục cùng tên để truy xuất. Report root do review trước tạo nằm trong `review_reports/`, không phải bằng chứng cho mọi revision. Không commit/push hoặc đặt hàng trong đợt kiểm này.
