# Tự đánh giá — Phạm Đức Mạnh · G01

## 1. Rà soát bốn khung từ lịch sử sửa nhãn

Bảng ghi nhận thay đổi có trong các bản export của chính bài làm: hai khung OMS và hai khung driver.

| Ảnh | Đối tượng | Loại lỗi / vấn đề | Ghi chú | Đã sửa? |
|---|---|---|---|---|
| S01_rgb.png | `infant_seat.seat` | Sai thuộc tính vị trí ghế | Bản đầu ghi `driver`; bản hiện tại ghi `rear_right`, đúng với nôi bên trái ảnh và quy ước ghế theo xe. | Có, thể hiện trong export hiện tại. |
| S02_rgb.png | `frame_meta.light` | Sai metadata `light` | Bản đầu ghi `day`; đã đổi thành `unknown` vì SVIRO là ảnh dựng. | Có. |
| D02.png | `face.eye_left`, `face.eye_right` | Chưa nhất quán giữa trạng thái mắt và cờ điểm | Bản v2 ghi hai mắt `open`, trong khi các điểm mắt được đánh dấu che khuất; ảnh có phản xạ kính và vùng mắt khó đọc. Bản mới ghi cả hai `unknown`. | Có, trong driver `3.zip` và bản gộp v3. |
| D03.png | `face.eye_left` | Khó xác định trạng thái mắt | Bản v2 ghi `open`; bản mới đổi thành `unknown` khi vùng mắt khó xác định. | Có, trong driver `3.zip` và bản gộp v3. |

Ở S01, thay đổi được xác nhận là thuộc tính `seat` từ `driver` thành `rear_right`; nhãn `infant_seat` được giữ nguyên.

## 2. Vấn đề lặp lại và cách tránh

Vấn đề lặp lại nhiều nhất là trạng thái mắt và cờ điểm chưa nhất quán: trong bản v2 có năm thuộc tính mắt ghi `open` khi cả bốn điểm tương ứng mang cờ `occluded` hoặc `outside`. Bản driver mới đã đổi năm thuộc tính đó thành `unknown` và lần tự kiểm hiện tại không còn cảnh báo.

Về lý do ban đầu: lúc đó tôi nhìn thấy được mắt nên chọn `open`. Sau khi chạy script, tôi đọc cảnh báo rằng nếu không nhìn thấy rõ thì ghi `unknown`, rồi sửa lại. Đây là trình tự tôi đã giải thích trong quá trình làm bài.

Cách tránh ở lần sau: phóng to vùng mắt, chỉnh brightness/contrast hiển thị khi cần, kiểm tra riêng từng mắt và từng điểm mốc. Chỉ chọn `open` hoặc `closed` khi đọc được mí; nếu không xác định chắc thì dùng `unknown`. Đồng thời cần phân biệt khả năng đọc trạng thái mắt với khả năng đặt chính xác từng khóe mắt và mép mí.

## 3. Một dòng review đã dẫn đến sửa nhãn

Ở `D02.png`, thuộc tính `eye_left`, bản cá nhân ban đầu là `open`, bản review của Nguyễn Thị Ngọc Mai là `unknown`. Lịch sử đối chiếu ghi `verdict=peer`, quy tắc 4.5; bản driver mới đã đổi thành `unknown`.

Bài học từ ca này là dùng `unknown` khi không đủ chắc để đọc trạng thái mí và rà lại các cờ điểm thay vì xem cảnh báo như kết luận tự động về ảnh. Các khác biệt khác chưa chốt vẫn được giữ trong bảng đối chiếu mới.

Căn cứ: export trước sửa trong lịch sử Git commit `279274c`, `export_final_v2.zip`, `export_final.zip`, `merge_report_v3.txt` và `disagreement_log.csv`. Nội dung được AI hỗ trợ tổng hợp từ dữ liệu; phần lý do chọn `open` dựa trên câu trả lời trực tiếp của người học.
