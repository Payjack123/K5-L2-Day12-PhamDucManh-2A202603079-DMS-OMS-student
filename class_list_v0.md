# Danh sách lớp v0 — Phạm Đức Mạnh · G01

Danh sách dựa trên Guideline Cabin v1.0, schema hiện tại và các bản export của bộ G01. Phần DMS sử dụng ảnh NIR thật D01–D06; phần OMS sử dụng các cặp RGB và IR mô phỏng S01–S08. Các mục dưới đây gồm lớp đối tượng và thuộc tính, kèm chức năng mà chúng hỗ trợ.

## DMS

| # | Lớp / thuộc tính | Giá trị | Để làm gì cho DMS | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | `person`, `seat` | Box người; `seat=driver` trong ảnh driver | Định vị tài xế và vùng cơ thể cần theo dõi. | Thường nhận ra hình dạng; cơ thể có thể bị che hoặc chìm trong vùng tối. |
| 2 | `face` | Box từ trán đến cằm, tai đến tai | Định vị mặt để xử lý mắt và điểm mốc. | Có khi mặt đủ rõ; bỏ box nếu không thấy mặt theo mục 4.5. |
| 3 | `eye_left`, `eye_right` | `open`, `closed`, `unknown` | Mô tả riêng từng mắt; chuỗi khung hình có thể hỗ trợ theo dõi nhắm mắt kéo dài. | Có thể khó đọc mí khi kính phản xạ, bị che hoặc ảnh tối; dùng `unknown` khi không chắc. |
| 4 | `glasses` | `unknown`, `none`, `clear`, `sun` | Nhận biết kính đang đeo và khả năng quan sát vùng mắt. | Có thể thấy gọng; loại tròng khó xác định vì kính râm có thể trông trong hơn trên NIR. |
| 5 | `gaze_zone` | `road`, `mirror_l`, `mirror_r`, `mirror_c`, `cluster`, `center`, `lap`, `other` | Phân biệt vùng nhìn của tài xế để hỗ trợ theo dõi sự chú ý. | Phụ thuộc khả năng đọc mắt và đầu; không chắc dùng `other`. |
| 6 | `face13` | 13 điểm mắt, mũi, miệng; cờ `occluded`, `outside` | Cung cấp vị trí các bộ phận mặt để theo dõi hình học khuôn mặt. | Gán khi box mặt rộng ít nhất 60 px; điểm bị che xử lý theo mục 4.6. |
| 7 | `hand` | `whose=driver/passenger`; `side=left/right`; `on_wheel=yes/no/unknown` | Xác định tay thuộc ai và trạng thái tiếp xúc với vô lăng. | Dựa vào hình dạng và vị trí tiếp xúc; có thể bị che. Tay rời vô lăng không tự chứng minh hành vi bất thường trong bộ Drive&Act. |
| 8 | `phone` | `state=held/mounted/lap` | Nhận biết điện thoại và trạng thái cầm hoặc đặt máy. | Chỉ gán khi thấy một phần cạnh, góc hoặc màn hình; không suy từ động tác tay gần tai. |
| 9 | `person.seatbelt` | `unknown`, `worn_correct`, `worn_incorrect`, `not_worn` | Mô tả tình trạng dây an toàn của tài xế. | Cần thấy đường dây đủ rõ; tối, bị che hoặc đang thắt dở thì dùng `unknown`. |

## OMS

| # | Lớp / thuộc tính | Giá trị | Để làm gì cho OMS | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | `person` | Box phần cơ thể người nhìn thấy | Nhận biết người xuất hiện trên hàng ghế sau trong phạm vi gán nhãn. | Dựa vào hình dạng cơ thể; thuộc tính không nhìn rõ không được suy đoán. |
| 2 | `seat` | Với OMS bộ G01: `rear_left`, `rear_middle`, `rear_right` | Gắn người hoặc vật với đúng vị trí ghế theo xe. | Dựa vào vị trí hình học; trái ảnh là `rear_right`. |
| 3 | `face` | Box mặt khi quan sát đủ rõ | Định vị vùng mặt của người trong cabin. | Chỉ cần box trong phần OMS; thuộc tính mắt và vùng nhìn không phải yêu cầu đầy đủ như DMS. |
| 4 | `child_seat`, `occupied` | Schema hiện tại: `unknown`, `no`, `yes` | Nhận biết ghế trẻ em và trạng thái bên trong khi quan sát được. | Cần nhìn rõ bên trong. Lựa chọn `yes` đang khác GUIDE gốc và được đưa vào câu hỏi leo thang bên dưới. |
| 5 | `infant_seat`, `facing` | `rear`, `front` | Nhận biết nôi và hướng sử dụng theo xe. | Dựa vào hình dạng và hướng cấu trúc; có nôi chưa đủ để kết luận có em bé. |
| 6 | `object.type` | `other`, `bag`, `box`, `cup` | Phân loại đồ vật mang theo trên ghế. | Dùng hình dạng và ngữ cảnh; ảnh IR không cung cấp thông tin màu RGB. |
| 7 | `person.seatbelt` | Với SVIRO của bài: `not_worn`, `unknown` | Mô tả tình trạng dây an toàn trong phạm vi bộ ảnh. | Không rõ thì `unknown`; dữ liệu này không có mẫu để chứng minh khả năng nhận ra dây đang đeo. |
| 8 | `frame_meta` | `modality=rgb/ir`; `light=unknown` cho SVIRO; `camera_blocked=yes/no` | Ghi loại ảnh và điều kiện quan sát của cả khung. | IR mô phỏng S## cần được phân biệt với NIR thật D## khi diễn giải hiện tượng. |

## Hai câu hỏi leo thang

1. **Phiên bản nào là quy định chính thức cho `child_seat.occupied` và trường hợp có trẻ trong ghế?**

   Khung ví dụ: `S03_rgb.png`, `S03_ir.png`, `S05_rgb.png`, `S05_ir.png`.

   GUIDE mục 4.1 và 4.8 chỉ cho `no` hoặc `unknown`, trong khi schema hiện tại nhận thêm `yes`. Export cá nhân và peer đều có `occupied=yes`: S03 tại `rear_left`; S05 tại `rear_left` và `rear_right`.

   Cách gán hiện tại: giữ `yes` theo export và schema đang dùng. Cần người viết guideline hoặc coach xác nhận phiên bản áp dụng và cách gán người trong ghế; chưa ghi nhận xác nhận đó trong dữ liệu được cung cấp.

2. **Có cho phép đọc được trạng thái mắt nhưng chưa định vị chắc đủ bốn điểm mốc mắt không, và xử lý cảnh báo thế nào?**

   Khung ví dụ: `D01.png`, mắt trái.

   Bản v2 có `eye_left=open` và cả bốn điểm `left_eye_*` có `occluded=1`; bản v3 đổi trạng thái mắt thành `unknown`. Mục 4.5 hướng dẫn đọc trạng thái mí, còn mục 4.6 hướng dẫn độ chắc của vị trí điểm. Cần làm rõ trường hợp nhìn thấy khe mắt nhưng không đặt chắc đủ bốn mốc.

   Cách gán hiện tại: `eye_left=unknown` theo bản driver mới; giữ các cờ điểm trong export đã gửi. Cần tiêu chí phân biệt không đọc được trạng thái mắt với không định vị được đủ bốn điểm mốc.

Các câu hỏi trên được đề xuất từ dữ liệu và bất đồng thực tế; chưa coi là nội dung đã được coach trả lời.
