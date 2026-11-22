# Báo cáo đối chiếu nhãn DMS OMS bộ ảnh G01

**Họ tên:** Phạm Đức Mạnh

**MSSV:** 2A202603079

**Ngày đối chiếu:** 22/11/2026

**Bộ ảnh:** G01, gồm 16 ảnh OMS và 6 ảnh driver.

Bản cá nhân `export_final_v2.zip` được đối chiếu với `peer_export_final.zip` của bạn review cùng mã G01. Hai bản có đủ 22 tên ảnh tương ứng và cùng kích thước ảnh. Kết quả so sánh ghi nhận 55 điểm khác biệt trên 14 ảnh, tập trung ở thuộc tính khuôn mặt và cờ điểm mốc `face13`.

Kết quả kiểm tra bằng `scripts/cabin_check.py`:

| Nội dung | Bản cá nhân | Bản review |
|---|---:|---:|
| Số ảnh | 22 | 22 |
| Số tag `frame_meta` | 22 | 22 |
| Số box `face` | 8 | 10 |
| Số skeleton `face13` | 6 | 6 |
| Lỗi ERROR | 0 | 0 |
| Cảnh báo WARN | 5 | 0 |

Kết quả trên sử dụng `cabin_schema.py` hiện tại, trong đó `child_seat.occupied` cho phép `unknown`, `no` và `yes`.

Các điểm khác biệt được tổng hợp theo nhóm:

| Nhóm nhãn | Số điểm khác | Nội dung |
|---|---:|---|
| `face13` | 31 | Cờ `occluded` và `outside` của các điểm mặt |
| `face` | 16 | Trạng thái mắt, kính, vùng nhìn và box mặt |
| `infant_seat` | 4 | Hướng nôi `front` hoặc `rear` |
| `person` | 2 | Tình trạng dây an toàn |
| `hand` | 1 | Tay có chạm vô lăng hay không |
| `frame_meta` | 1 | Loại ảnh RGB hoặc IR |
| **Tổng** | **55** | |

Những khác biệt cần lưu ý khi review:

| Ảnh | Nội dung | Bản cá nhân | Bản review | Căn cứ xử lý |
|---|---|---|---|---|
| D01 | Mắt phải; dây an toàn; tay trên vô lăng | `open`; `unknown`; `yes` | `unknown`; `worn_incorrect`; `no` | Kiểm tra vùng mắt, đường dây và tiếp xúc tay với vô lăng theo mục 4.5 và 4.7. |
| D02 | Hai mắt; kính; vùng nhìn; dây an toàn | Hai mắt `open`; `clear`; `road`; `unknown` | Hai mắt `unknown`; `sun`; `other`; `worn_correct` | Ảnh tối và phản xạ kính gây khó quan sát. Đối chiếu mục 4.5, 4.6 và 4.7. |
| D03 | Mắt trái; vùng nhìn | `open`; `road` | `unknown`; `lap` | Kiểm tra khả năng đọc mí mắt và hướng mắt, đầu theo mục 4.5. |
| D04 | Vùng nhìn | `road` | `other` | Không chắc đích nhìn thì dùng `other` và ghi lý do theo mục 4.5. |
| D05 | Hai mắt; kính; vùng nhìn | Hai mắt `open`; `clear`; `road` | Hai mắt `closed`; `sun`; `cluster` | Kiểm tra riêng từng mắt, loại kính đang đeo và hướng nhìn theo mục 4.5. |
| S02 RGB và IR | Vùng nhìn | `other` | `mirror_c` | OMS chỉ yêu cầu box `face`; bản cá nhân có thể giữ `other`. |
| S04 RGB và IR | Box mặt | Chưa có box `face` | Có box `face` | Bổ sung nếu thấy mặt đủ rõ; nếu mặt quay đi hoặc bị che gần hết, ghi lý do theo mục 4.5. |
| S06_rgb | Loại ảnh | `rgb` | `ir` | Theo tên file và mục 4.3-1, `rgb` là giá trị đúng. |
| S07 RGB và IR | Hướng nôi | `rear` | `front` | Xác định hướng nôi theo xe: `front` về đầu xe, `rear` về đuôi xe. |
| S08 RGB và IR | Hướng nôi | `rear` | `front` | Kiểm tra hướng sử dụng của nôi theo mục 4.8. |

Đối với `S06_rgb.png`, bản cá nhân đúng về `modality`. Dòng này đã được ghi `verdict = mine`, `guideline_rule = 4.3-1` trong `disagreement_log.csv`. Các mục còn lại được ghi nhận để tiếp tục đối chiếu và thống nhất cách xử lý.

Năm cảnh báo của bản cá nhân đều liên quan đến mắt trong ảnh driver. Ảnh NIR tối, vùng kính có phản xạ hoặc che khuất khiến khó xác định chính xác các điểm cần đánh, nhất là khóe mắt và mép mí. Đồng thời, bản export đang có thuộc tính mắt `open` nhưng cả bốn điểm tương ứng được đánh dấu `occluded` hoặc `outside`, nên script yêu cầu rà soát sự nhất quán.

| Cảnh báo | Giải thích và hướng rà soát |
|---|---|
| D01, mắt trái | Vùng kính và bóng tối làm khó xác định chính xác mép mí, khóe mắt. Ảnh vẫn thấy được một phần khe mắt; cần kiểm tra từng điểm và bỏ cờ che khuất ở điểm thực sự nhìn thấy. |
| D01, mắt phải | Vùng mắt bị phản xạ hoặc che khuất qua kính, khó đọc trạng thái mí và vị trí điểm mốc. Khi không phân biệt được mắt mở hay nhắm, chọn `unknown` theo mục 4.5. |
| D02, mắt trái | Ảnh tối, phản xạ trên tròng kính che vùng mắt nên khó xác định các điểm cần đánh. Cần rà lại trạng thái mắt; dùng `unknown` nếu không đọc được mí. |
| D02, mắt phải | Các đốm phản xạ trên kính làm giảm khả năng quan sát khe mắt và điểm mốc. Không đủ căn cứ xác định mở hoặc nhắm thì dùng `unknown`. |
| D03, mắt trái | Tài xế cúi đầu, vùng mắt và kính tối nên khó xác định mép mí, khóe mắt. Cần rà lại thuộc tính mắt và cờ điểm theo mục 4.5–4.6. |

Theo mục 4.6, điểm nhìn thấy rõ được đặt trực tiếp tại mép mí hoặc khóe mắt. Điểm bị che nhưng ước lượng chắc vị trí dùng `occluded`; không xác định được vị trí thì dùng `outside` theo quy ước của bài lab. Bản export được đối chiếu trong báo cáo vẫn có **0 lỗi và 5 cảnh báo**; các nhận xét trên là giải thích điều kiện quan sát và hướng rà soát.

Tại thời điểm lập báo cáo, bảng đối chiếu có một dòng đã xác định kết luận bằng quy tắc tên ảnh. Hai người review cần thống nhất thêm ít nhất bốn dòng để đạt yêu cầu tối thiểu năm dòng đã xử lý của E3. Sau khi thống nhất, cập nhật `verdict`, `guideline_rule`, `action`; các nhãn cần sửa được chỉnh trên CVAT, lưu và export lại để kiểm tra.

Các tệp kèm theo:

- [disagreement_log.csv](disagreement_log.csv): 55 dòng đối chiếu và nội dung xử lý.
- [check_final_v2.txt](check_final_v2.txt): kết quả tự kiểm bản cá nhân và giải thích cảnh báo.
- [check_peer.txt](check_peer.txt): kết quả tự kiểm bản review.
- [face13_coordinate_diff.csv](face13_coordinate_diff.csv): tọa độ điểm mặt hỗ trợ rà soát; khoảng cách được tính khi hai điểm đều có `outside=0` và ảnh cùng kích thước.
- [GUIDE.md](GUIDE.md): Guideline Cabin v1.0, các mục 4.3–4.8.
