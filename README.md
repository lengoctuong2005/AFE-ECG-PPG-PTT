# AFE ECG + PPG PAT

Đồ án nghiên cứu thu nhận ECG một chuyển đạo bằng AD8232 và ADS1115, kết hợp PPG từ module MAX30102 qua ESP32-DevKitC V4. PAT là thời gian từ đỉnh R ECG đến chân sóng PPG, bao gồm tiền tống máu PEP, không phải PTT thuần.

> **Chỉ dùng làm nguyên mẫu nghiên cứu trên bàn thử.** PCB không được đánh giá an toàn tiếp xúc cơ thể và không phải thiết bị y tế. Không gắn điện cực lên người chỉ vì dùng pin hoặc CAD đã sạch. Không kết nối USB, bộ sạc hoặc thiết bị đo có đường tới điện lưới khi đang gắn điện cực.

## Nội dung

- `AFE_ECG_PPG_PTT.kicad_pro`, `.kicad_sch`, `.kicad_pcb`: thiết kế KiCad 10, bo hai lớp 92 × 70 mm, giảm 19,5% diện tích so với bản đầu 100 × 80 mm.
- `libs/`, `sym-lib-table`, `fp-lib-table`: thư viện của dự án và tham chiếu thư viện chuẩn KiCad.
- `firmware/esp32_ptt_streamer/`: mã ESP-IDF cho ESP32 và kiểm thử host.
- `software/`: bộ đọc telemetry và phân tích dữ liệu mô phỏng; dữ liệu firmware live chỉ kiểm chất lượng, PAT chưa được mở cho timestamp chưa hiệu chuẩn.
- `tests/`: kiểm tra netlist, parity và drill.
- `outputs/print_preflight_20261114/`: Gerber, drill, BOM, placement và kết quả CAD hiện hành 92 × 70 mm, **chưa phải gói chế tạo/lắp ráp đã phê duyệt**.
- `outputs/final_verification_20261113/`: dữ liệu lịch sử 100 × 80 mm, không dùng đặt bo theo PCB hiện hành.
- `DANH_SACH_LINH_KIEN.md`: linh kiện cho một bo và số lượng mua dự phòng.
- `BaoCao_DoAn.html`: báo cáo kỹ thuật đã loại thông tin định danh sinh viên khỏi bản công khai.

## Trạng thái kiểm thử

Bản 92 × 70 mm dịch ESP32 sang trái 8 mm, giữ một ECG ba điện cực qua J1 và một PPG qua J3. Jack 3.5 mm sát cạnh trên. KiCad 10.0.8 kiểm lại mọi severity và all-track-errors: DRC 0, unrouted 0, parity 0, không thêm ignored checks; 90 lỗ/slot khớp drill. Footprint analog giữ vị trí, fanout giao tiếp và ground return C8 đã sửa; chưa đo nhiễu thực.

Ngày 13/11/2026, KiCad 10.0.8 báo ERC 0 với hai loại kiểm tra không áp dụng bị bỏ qua, DRC 0, unrouted 0 và schematic parity 0, không bỏ qua kiểm tra DRC. Tám mươi sáu lỗ và slot đã được đối chiếu với PCB. Firmware nguồn trước khi bỏ cấu hình mạng mẫu đã build ESP-IDF v5.5 cho target ESP32; **bản công khai đã thay cấu hình mạng nên cần cấu hình và build lại**. Chưa flash hoặc thử trên phần cứng thật.

MAX30102 module, mức logic và thứ tự chân, cơ khí ESP32 DevKit/cáp, MPN linh kiện và quy ước lắp ráp chưa xác nhận bằng mẫu thực. Chưa đo đáp ứng analog, FIFO/IRQ, sai số đồng bộ hoặc an toàn tiếp xúc cơ thể. Gerber viewer sử dụng cho lần kiểm trước không hiểu thuộc tính metadata X2; cần review CAM phù hợp với nhà gia công trước khi đặt bo.

## Cấu hình và kiểm thử

Sao chép file mẫu `network_config.example.h` thành `network_config.local.h` trong cùng thư mục, sau đó điền cấu hình mạng cho môi trường thử riêng. File local bị Git bỏ qua; giá trị rỗng trong mẫu chỉ là placeholder và không kết nối được mạng.

```bash
cp firmware/esp32_ptt_streamer/main/network_config.example.h firmware/esp32_ptt_streamer/main/network_config.local.h
```

```bash
make -B -C firmware/esp32_ptt_streamer test
```

```bash
python3 software/test_protocol_regression.py
```

```bash
python3 software/ptt_live_analyzer.py --simulate --duration 12
```

```bash
python3 tests/check_analog_netlist.py && python3 tests/check_feedback_netlist.py && python3 tests/check_pcb_netlist.py && python3 tests/check_compact_layout.py && python3 tests/check_fabrication_drills.py
```

Test CAD yêu cầu KiCad với `kicad-cli` và Python `pcbnew`; test DSP yêu cầu các gói trong `software/requirements.txt`. Test host không thay thế build ESP-IDF hoặc kiểm trên phần cứng.
