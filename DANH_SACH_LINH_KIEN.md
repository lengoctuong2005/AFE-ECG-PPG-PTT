# Danh sách linh kiện cho 1 bo AFE ECG + PPG PAT

Đối chiếu BOM của thiết kế hiện hành: `outputs/print_preflight_20261114/BOM.csv`.

**Mua theo cột “Cần dùng”; cột “Nên mua” chỉ là gợi ý dự phòng khi hàn.** Chưa có giá hoặc mã nhà bán được xác minh. Đây là danh sách chuẩn bị prototype, không phải BOM lắp ráp đã được phê duyệt đầy đủ MPN.

## 1. Điện trở

Toàn bộ là **điện trở dán SMD 0603 imperial, tương đương 1608 metric, kích thước thân 1.6 × 0.8 mm**. Chọn sai số 1%, công suất và điện áp làm việc theo datasheet của mã mua. Không mua điện trở chân dài để lắp trực tiếp lên bo này. Không nhầm với 0603 metric nhỏ hơn.

| Trị số | Vị trí trên PCB | Cần dùng | Nên mua |
|---|---|---:|---:|
| 360 kΩ | R1, R2, R3 | 3 | 5 |
| 10 MΩ | R4, R5, R6, R8, R9, R10 | 6 | 10 |
| 1 MΩ | R11, R12, R14 | 3 | 5 |
| 100 kΩ | R13 | 1 | 5 |
| 1 kΩ | R15 | 1 | 5 |
| 4.7 kΩ | R16, R17 | 2 | 5 |
| 1.4 MΩ | R18 | 1 | 5 |
| 10 kΩ | R19 | 1 | 5 |
| **Tổng** | **18 điện trở** | **18** | **45** |

R7 không có trong thiết kế hiện hành. Không thay 1.4 MΩ hoặc 10 MΩ bằng trị số gần đúng khi chưa tính và kiểm lại mạch.

## 2. Tụ điện

Toàn bộ là **tụ ceramic dán SMD 0603 imperial / 1608 metric, không phân cực**. Các thông số điện môi, dung sai và điện áp dưới đây là yêu cầu lựa chọn mua cho prototype, không phải thông tin đã có đầy đủ trong BOM gốc. Không thay bằng tụ hóa hoặc tụ chân dài mà không sửa footprint và kiểm lại tính năng.

| Điện dung | Vị trí trên PCB | Loại nên chọn | Cần dùng | Nên mua |
|---|---|---|---:|---:|
| 330 nF = 0.33 µF | C1, C2 | X7R, ±10% hoặc tốt hơn, điện áp định mức ≥10 V; ưu tiên cặp cùng mã/dung sai | 2 | 5 |
| 1 nF = 1000 pF | C3 | C0G/NP0, ±5% hoặc tốt hơn, ≥16 V | 1 | 5 |
| 100 nF = 0.1 µF | C4, C8, C11 | X7R, ±10% hoặc tốt hơn, ≥10 V | 3 | 5 |
| 1.5 nF = 1500 pF | C5 | C0G/NP0, ±5% hoặc tốt hơn, ≥16 V | 1 | 5 |
| 10 nF = 0.01 µF | C6, C7 | C0G/NP0 ưu tiên, ±5% hoặc tốt hơn, ≥16 V; đặc biệt C6 thuộc bộ lọc | 2 | 5 |
| 1 µF | C9, C10 | X7R, điện áp định mức ≥10 V; kiểm điện dung hiệu dụng và ESR của đúng mã mua | 2 | 5 |
| **Tổng** | **11 tụ** | | **11** | **30** |

**C10 là tụ đầu ra LDO 2.8 V:** chọn mã có điện dung hiệu dụng tối thiểu 1 µF và ESR trong khoảng 0–2 Ω tại điều kiện sử dụng theo MCP1700. Chỉ nhìn chữ “1 µF” trên trang bán chưa đủ vì dung sai và DC bias có thể làm giảm điện dung. C9 là tụ đầu vào LDO trên rail 3.3 V. Các tụ lọc khác cũng cần được đánh giá theo dung sai và điện dung hiệu dụng; danh sách này chưa xác nhận một mã thương mại cụ thể.

## 3. IC rời cần hàn lên bo

| Vị trí | Linh kiện / mã cần đối chiếu | Package khớp PCB | Cần dùng | Gợi ý mua |
|---|---|---|---:|---|
| U1 | AD8232ACPZ, đúng IC AD8232 của Analog Devices; hậu tố đóng gói mua phải được đối chiếu | LFCSP 20 chân + exposed pad, thân 4 × 4 mm, pitch 0.5 mm, EP 2.6 × 2.6 mm | 1 | Có thể mua thêm 1 nếu dự kiến hàn thử |
| U2 | ADS1115IDGST hoặc hậu tố cùng package DGS đã xác nhận | VSSOP-10 DGS, thân 3 × 3 mm, pitch 0.5 mm; footprint KiCad có tên `TSSOP-10_3x3mm_P0.5mm` | 1 | Không mua bản SOIC hoặc breakout thay cho IC rời |
| U3 | MCP1700T-2802E/TT, đầu ra cố định 2.8 V | SOT-23, chân 1 GND, chân 2 VOUT, chân 3 VIN | 1 | Không mua bản 3.0 V/3.3 V hoặc TO-92 để thay trực tiếp |

U1/U2/U3 trên PCB là **IC rời**, không phải vị trí cắm module AD8232/ADS1115 có sẵn. AD8232 có chân đáy, cần phương án hàn paste/reflow hoặc khò phù hợp; chỉ có mỏ hàn thường sẽ khó lắp đúng.

## 4. Module, đầu nối và phụ kiện

| Mục | Cần dùng | Yêu cầu trước khi mua/lắp |
|---|---:|---|
| ESP32-DevKitC V4 dùng ESP32-WROOM-32E, 38 chân | 1 board | Thiết kế theo hai hàng 19 chân, pitch dọc 2.54 mm, khoảng cách tâm hai hàng 25.4 mm. Đối chiếu đúng bản vẽ, thứ tự chân và chiều USB/anten; không coi mọi “ESP32 38 pin” là tương thích. |
| Socket cái thẳng 1×19, pitch 2.54 mm | 2 thanh | Hàn vào J2 để cắm ESP32 có chân đực. Có thể dùng thanh dài hơn rồi cắt chính xác. Không dùng header 2×19 hai hàng sát nhau. |
| Module MAX30102 | 1 module | **Chưa chốt mã module thương mại.** J3 giả định chân 1–7 là VIN 3.3 V, SCL, SDA, INT, RD, IRD, GND. Phải xác nhận nguồn, level-shift và pull-up/INT của module; không cắm trực tiếp breakout chưa rõ pinout. |
| Đầu nối 1×7, pitch 2.54 mm cho J3 | 1 thanh | Dùng header và dây tới đầu PPG rời. Hai hàng J3/J2 chỉ cách tâm 5 mm, chưa xác nhận breakout cắm trực tiếp. Kiểm mapping từng dây, mức nguồn/I²C/INT, chiều đầu cắm và chống kéo; RD/IRD không dùng. |
| Jack stereo 3.5 mm SJ1-3533NG | 1 | Đúng loại chân và hướng nằm ngang theo footprint J1; không mua jack 3.5 mm bất kỳ chỉ vì cùng đường kính. |
| Cáp TRS 3.5 mm ba dây | 1 | Mapping bo: Tip → RA, Ring → LA, Sleeve → RL. Kiểm thông mạch cáp thực trước sử dụng; nhãn màu không chứng minh thứ tự dây. Chuẩn bị cho nguồn tín hiệu giả lập, chưa dùng người làm tải thử. |
| Cáp USB phù hợp ESP32 DevKit thực | 1 | Để nạp/chạy thử trên bàn với tín hiệu giả lập; DevKitC V4 chính hãng dùng Micro-USB. Không cấp đồng thời nhiều nguồn khi chưa kiểm backfeed. |
| Dây jumper / dây đo nhỏ | 1 bộ | Đấu bench theo sơ đồ và kiểm pinout trước cấp nguồn. |
| Vít M3 và trụ đỡ phù hợp | 4 bộ | Bo có 4 lỗ 3.2 mm có pad GND. Chọn chiều dài/trụ đỡ theo module, mặt dưới và vỏ; tránh gây chạm mạch. |

Không dùng module MAX30100 hoặc MAX30105 thay MAX30102 nếu chưa sửa và kiểm phần cứng/firmware tương ứng.

## 5. Những mục trên BOM không phải linh kiện cần mua

- **H1–H4:** lỗ bắt vít có pad GND, đã được nhà sản xuất PCB tạo trên bo. Phần cần mua là vít/trụ đỡ ở mục 4.
- **TP1–TP7:** pad đồng đo tròn đường kính 1.5 mm, không có lỗ cắm. Không cần mua bảy linh kiện testpoint để khớp footprint này. Chạm probe hoặc hàn dây nhỏ theo kế hoạch thử.

| Điểm đo | Tín hiệu |
|---|---|
| TP1 | ECG_OUT |
| TP2 | REFOUT, danh định khoảng 1.4 V, cần đo thực |
| TP3 | LOD+ |
| TP4 | LOD− |
| TP5 | +VS_A, nguồn analog danh định 2.8 V |
| TP6 | +3V3 |
| TP7 | GND |

## 6. Dụng cụ chuẩn bị, không tính vào linh kiện bo

- Nhíp, kính phóng đại, dụng cụ ESD và phương tiện hàn SMD phù hợp package.
- Kem hàn/flux và vật tư vệ sinh phù hợp; vệ sinh kỹ các nút MΩ, không để flux dẫn rò.
- Đồng hồ đo, nguồn bench có giới hạn dòng và nguồn tín hiệu ECG/PPG giả lập phù hợp.
- Dụng cụ đo timing/dao động ký cần kiểm phương án nối đất trước sử dụng. Không ngắt protective earth của thiết bị đo.

## 7. Kiểm trước khi đặt hàng

- [ ] Tất cả điện trở/tụ dán chọn đúng **0603 imperial / 1608 metric**.
- [ ] Trị số và số lượng khớp bảng: 18 điện trở, 11 tụ, 3 IC rời, 1 ESP32 và 1 module MAX30102.
- [ ] Đã chọn MPN cụ thể, kiểm điện áp/công suất/dung sai, riêng C10 đạt điều kiện ổn định LDO.
- [ ] Đã xác nhận kích thước/pinout module, jack, cáp và socket bằng bản vẽ hoặc mẫu thực.
- [ ] Không tự thay gần đúng trị số hoặc package khi cửa hàng thiếu hàng.

**Giới hạn:** chưa có báo giá, xác nhận nguồn hàng, kết quả lắp ráp hay thử trên người. Danh sách này không thay thế đánh giá an toàn. Không gắn điện cực lên người chỉ vì dùng pin, build firmware PASS hoặc DRC bằng 0.

Nguồn thông số cần đối chiếu khi chọn MPN:
- [AD8232 datasheet](https://www.analog.com/media/en/technical-documentation/data-sheets/AD8232.pdf)
- [ADS1115 datasheet](https://www.ti.com/lit/ds/symlink/ads1115.pdf)
- [MCP1700 datasheet](https://ww1.microchip.com/downloads/en/DeviceDoc/MCP1700-Low-Quiescent-Current-LDO-20001826E.pdf)
- [ESP32-DevKitC V4](https://docs.espressif.com/projects/esp-dev-kits/en/latest/esp32/esp32-devkitc/user_guide.html)
