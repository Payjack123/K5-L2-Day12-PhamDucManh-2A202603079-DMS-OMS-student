# Báo cáo đối chiếu nhãn DMS OMS bộ ảnh G01

**Họ tên:** Phạm Đức Mạnh

**MSSV:** 2A202603079

**Ngày cập nhật:** 22/11/2026

**Bộ ảnh:** G01, gồm 16 ảnh OMS và 6 ảnh driver.

Bản cá nhân mới nhất là `export_final_v3.zip`, được gộp từ bản OMS đã kiểm tra và phần driver cập nhật trong `3.zip`. File `export_final.zip` có cùng nội dung để dùng với lệnh kiểm tra mặc định. Bản cá nhân và bản review cùng có đủ 22 tên ảnh tương ứng.

| Nội dung | Bản cá nhân v2 trước sửa | Bản cá nhân v3 hiện tại | Bản review |
|---|---:|---:|---:|
| Số ảnh | 22 | 22 | 22 |
| Số tag frame_meta | 22 | 22 | 22 |
| Lỗi ERROR | 0 | 0 | 0 |
| Cảnh báo WARN | 5 | 0 | 0 |

Kết quả sử dụng `cabin_schema.py` hiện tại, trong đó `child_seat.occupied` cho phép `unknown`, `no` và `yes`.

Trước cập nhật, năm cảnh báo nằm ở vùng mắt trong ảnh D01–D03. Ảnh NIR tối, vùng kính có phản xạ hoặc che khuất khiến khó xác định chính xác điểm mốc cần đánh, nhất là khóe mắt và mép mí. Bản driver mới đã cập nhật các thuộc tính sau:

| Ảnh | Thuộc tính | Trước sửa | Bản driver mới |
|---|---|---|---|
| D01.png | `eye_left` | `open` | `unknown` |
| D01.png | `eye_right` | `open` | `unknown` |
| D02.png | `eye_left` | `open` | `unknown` |
| D02.png | `eye_right` | `open` | `unknown` |
| D03.png | `eye_left` | `open` | `unknown` |

Sau khi gộp và kiểm tra lại, bản v3 đạt **0 lỗi, 0 cảnh báo**. Các giải thích của lần kiểm tra trước vẫn được giữ trong `check_final_v2.txt`; kết quả hiện tại nằm trong `check_final.txt` và `check_final_v3.txt`.

Bảng đối chiếu ban đầu giữa v2 và peer có 55 dòng khác biệt trên 14 ảnh. `disagreement_log.csv` giữ lịch sử này và đã ghi nhận 5 dòng có kết luận:

| Ảnh | Nội dung đối chiếu | Kết luận và xử lý |
|---|---|---|
| S06_rgb.png | Cá nhân rgb, peer ir | `mine`, mục 4.3-1. Bản cá nhân đúng theo tên file; peer cần sửa modality thành rgb. |
| D01.png | eye_right: open hoặc unknown | `peer`, mục 4.5. Bản driver mới đã đổi thành unknown do vùng mắt khó quan sát. |
| D02.png | eye_left: open hoặc unknown | `peer`, mục 4.5. Bản driver mới đã đổi thành unknown. |
| D02.png | eye_right: open hoặc unknown | `peer`, mục 4.5. Bản driver mới đã đổi thành unknown. |
| D03.png | eye_left: open hoặc unknown | `peer`, mục 4.5. Bản driver mới đã đổi thành unknown. |

So sánh bản v3 với peer hiện còn **52 điểm khác trên 14 ảnh**, được lưu riêng trong `disagreement_log_v3.csv`:

| Nhóm nhãn | Số điểm khác hiện tại |
|---|---:|
| `face` | 13 |
| `face13` | 31 |
| `frame_meta` | 1 |
| `hand` | 1 |
| `infant_seat` | 4 |
| `person` | 2 |

Một khác biệt mới là mắt trái D01: bản cá nhân hiện chọn `unknown`, bản peer là `open`. Cần đọc lại khe mắt trên ảnh và áp dụng mục 4.5; giữ `unknown` khi chưa đủ chắc để xác định trạng thái mí. Các khác biệt về cờ điểm mặt, kính, hướng nhìn, dây an toàn, tay, box mặt S04 và hướng nôi S07–S08 tiếp tục được rà theo các mục 4.5–4.8. Kết quả tự kiểm hỗ trợ phát hiện sự không nhất quán; kết luận nhãn dựa trên ảnh và guideline.

Các tệp kèm theo:

- [export_final.zip](export_final.zip): bản gộp hiện tại đủ 22 ảnh, không kèm ảnh gốc.
- [check_final.txt](check_final.txt): kết quả tự kiểm hiện tại.
- [check_final_v2.txt](check_final_v2.txt): kết quả và giải thích cảnh báo của phiên bản trước.
- [disagreement_log.csv](disagreement_log.csv): lịch sử 55 dòng đối chiếu, đã ghi nhận các kết luận và thay đổi nêu trên.
- [disagreement_log_v3.csv](disagreement_log_v3.csv): bảng so sánh mới sau cập nhật.
- [face13_coordinate_diff.csv](face13_coordinate_diff.csv): tọa độ điểm mặt hỗ trợ rà soát.
- [GUIDE.md](GUIDE.md): Guideline Cabin v1.0.
