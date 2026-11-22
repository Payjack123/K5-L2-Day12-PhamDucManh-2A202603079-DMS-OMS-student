# Khai báo dùng AI — Phạm Đức Mạnh

Công cụ sử dụng: **ChatGPT/Codex** trong phiên hỗ trợ bài lab Ngày 12, bộ G01. Bảng dưới tổng hợp các nhóm yêu cầu đã thực hiện. Các phép kiểm chứng được ghi theo tài liệu, file và lệnh có trong phiên hỗ trợ; không khẳng định mọi kiểm tra đều do người học tự thực hiện độc lập.

| # | Công cụ | Đã hỏi hoặc yêu cầu gì | Dùng kết quả thế nào | Kiểm chứng có trong phiên làm việc |
|---|---|---|---|---|
| 1 | ChatGPT/Codex | Giải thích đề bài, thư mục, cài CVAT và quy trình gán nhãn | Theo các bước tạo project, task và chuẩn bị dữ liệu | Đọc README, GUIDE, INSTALL_CVAT và các mẫu trong repo. |
| 2 | ChatGPT/Codex | Clone repo cá nhân, giải nén G01 vào đúng vị trí | Chuẩn bị thư mục làm bài trên máy | Kiểm tra tên ảnh, manifest và quy tắc gitignore. |
| 3 | ChatGPT/Codex | Giải thích các thuộc tính seat, occupied, facing, seatbelt, gaze_zone, whose, on_wheel, state và quy tắc điểm mặt | Hiểu trường nhãn và rà lại những chỗ đã gán | Đối chiếu GUIDE và schema; chưa coi mọi nhận xét của AI là đáp án chuẩn. |
| 4 | ChatGPT/Codex | Nhận xét ảnh cabin và cảnh báo mắt ở D01–D03 | Xem xét khả năng quan sát mắt, cờ điểm và đề xuất unknown khi không xác định chắc | Đối chiếu ảnh gốc, thuộc tính trong export và cảnh báo script. Có sử dụng ảnh trong quá trình hỗ trợ. |
| 5 | ChatGPT/Codex | Gộp các export OMS/driver và kiểm tra nhiều phiên bản | Tạo export đủ 22 ảnh; giữ lịch sử các lần sửa | So sánh annotation trước/sau gộp, số ảnh, cờ điểm, checksum; chạy cabin_check. |
| 6 | ChatGPT/Codex | So sánh với export của Nguyễn Thị Ngọc Mai (MSSV 2A202603188) cùng G01 | Tạo bảng khác biệt, tham chiếu guideline và ghi các thay đổi đã có trong driver mới | Bảng đầu 55 dòng; năm dòng có kết luận. Bảng sau cập nhật có 52 khác biệt còn được lưu để rà tiếp. |
| 7 | ChatGPT/Codex | Soạn báo cáo đối chiếu và giải thích cảnh báo do vùng mắt tối, phản xạ kính, khó xác định điểm mốc | Ghi nhận điều kiện quan sát và lịch sử sửa trạng thái mắt | Bản v2 có năm cảnh báo; bản driver 3.zip và bản gộp v3 hiện có 0 lỗi, 0 cảnh báo theo schema đang dùng. |
| 8 | ChatGPT/Codex | Kiểm tra và push các file bài làm lên repo cá nhân | Lưu export, báo cáo và lịch sử sửa trên GitHub | Đã xác nhận commit 808796b trên nhánh main trước khi chuẩn bị sáu file bổ sung này. |
| 9 | ChatGPT/Codex | Điền ir_log, đề xuất danh sách lớp và câu hỏi về guideline, tổng hợp tự đánh giá và TEAM | Soạn các file từ dữ liệu thực tế; thông tin cá nhân do người học cung cấp | Người học xác nhận làm cá nhân, tên peer và lý do ban đầu chọn open. Các quan sát IR và thay đổi nhãn được đối chiếu với ảnh/export. |
| 10 | ChatGPT/Codex | Hỗ trợ đáp án và giải thích exit ticket | Chuẩn bị câu trả lời có khai báo AI hỗ trợ | Câu 2 kiểm tra trực tiếp phép tính 314−240+1=75 khung, 75/30=2.50 giây; câu 1 và 3 đối chiếu kiến thức của bài và nguồn sơ cấp khi cần. |

## Dữ liệu đã dùng trong trao đổi

Có gửi ảnh cabin và ảnh chụp giao diện CVAT trong hội thoại. Công cụ AI cũng đã xem các ảnh gốc S01, D01–D03 trên máy để hỗ trợ nhận xét. Các file export annotation không kèm ảnh được dùng để gộp và đối chiếu. Ảnh gốc trong G01 và ZIP gốc của người review được giữ ngoài các file đã push lên GitHub.

## Phạm vi hỗ trợ

AI hỗ trợ giải thích, kiểm tra dữ liệu và diễn đạt báo cáo. Bản `exit_ticket.md` có AI hỗ trợ giải đáp; không ghi là người học đã tự làm độc lập trong 10 phút. Phần tự đánh giá sử dụng lời giải thích trực tiếp của người học về quá trình chọn `open` và sửa thành `unknown`, cùng lịch sử thay đổi trong export.
