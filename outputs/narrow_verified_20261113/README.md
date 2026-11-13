# PCB 92 × 70 mm

Bộ xuất hiện hành, giảm 8% diện tích từ 100 × 70 mm và 19,5% từ 100 × 80 mm. ESP32 dịch trái 8 mm; J1 sát cạnh trên. Một ECG ba điện cực RA/LA/RL qua J1 và một MAX30102 PPG qua J3. Schematic, BOM, firmware và project rules không đổi trong lần sửa layout.

KiCad 10.0.8, mọi severity và all-track-errors: DRC 0, unrouted 0, parity 0, ignored_checks rỗng. ERC 0, hai loại không áp dụng ghi trong report. Netlist 46 footprint/151 node, geometry và 86 lỗ/slot khớp drill đều PASS.

Vùng anten x=60…92, y=0…12 mm trên hai lớp. Footprint analog giữ vị trí; fanout và đường GND C8 đã sửa. C8 có via GND tại (59,275;46,1) mm; chưa đo chất lượng analog hoặc nhiễu thực.

Gerber đã render bằng gerbv 2.10.0. Viewer không hiểu metadata X2 và cảnh báo nhận diện lớp đáy rỗng/mask dạng region không aperture. Chưa duyệt CAM với xưởng. Bản lắp Assembly_1to1.pdf cần in ở 100%, không fit page, để so module thực.

Không dùng dữ liệu lịch sử 100 × 80 mm trong thư mục final_verification_20261113 cho PCB hiện hành. Chưa xác nhận module/plug/vỏ, RF, analog, timing hoặc an toàn tiếp xúc cơ thể. Không dùng trên người. Bản công khai cần cấu hình mạng riêng và build ESP-IDF lại trước thử bench.
