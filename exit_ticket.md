# Exit ticket — Ngày 12

**Họ tên:** Phạm Đức Mạnh. **Mã:** G01.

Các câu trả lời dưới đây có hỗ trợ của AI theo yêu cầu của người học và được khai báo trong `prompts.md`. Phép tính được kiểm tra trực tiếp; không ghi nhận đây là bài tự làm độc lập trong 10 phút.

**Câu 1 · Chọn một.** Camera DMS trên nhiều xe tự chiếu đèn LED cận hồng ngoại khoảng 940 nm lên mặt tài xế. Lý do chính là gì?

- A. Để đo nhiệt độ da và phát hiện tài xế bị sốt.
- B. Để có ảnh mặt ổn định cả ngày lẫn đêm mà không làm chói mắt tài xế.
- C. Để có ảnh màu đẹp hơn cho cuộc gọi video.
- D. Để camera nhìn xuyên qua mọi loại kính râm.

**Đáp án: B.**

Chiếu sáng NIR chủ động giúp camera thu được vùng mặt khi điều kiện sáng thay đổi, kể cả trong tối. Bước sóng này nằm ngoài vùng nhìn thấy thông thường nên hạn chế gây chói hoặc xao nhãng như chiếu đèn khả kiến. NIR 940 nm không phải phép đo nhiệt độ và không bảo đảm nhìn xuyên mọi loại kính.

Nguồn đối chiếu: [ams OSRAM về camera ô tô và chiếu sáng NIR 940 nm](https://ams-osram.com/news/press-releases/the-first-automotive-camera-with-infrared-and-visible-capabilities-enables-advancements-in-driver-safety-accident-avoidance).

**Câu 2 · Số, hai chữ số thập phân.** Camera DMS chạy 30 khung hình/giây. Model ước lượng yaw của đầu tài xế lớn hơn 30° liên tục từ khung hình số 240 đến khung hình số 314, tính cả hai đầu. Tài xế không nhìn đường trong bao nhiêu giây?

**Đáp án: 2.50 s.**

Số khung hình = 314 − 240 + 1 = 75 khung.

Thời gian = 75 / 30 = 2.50 giây. Cộng 1 vì đề tính cả khung 240 và khung 314.

**Câu 3 · Chọn tất cả đáp án đúng.** Những câu nào đúng về dữ liệu cabin so với dữ liệu camera ngoài xe?

- A. Không thể làm mờ mặt tài xế như làm mờ mặt người qua đường, vì model DMS cần chính khuôn mặt.
- B. Ban đêm, ảnh cabin thường là ảnh hồng ngoại đen trắng, nên thuộc tính màu áo không gán được.
- C. Camera OMS nhìn về phía sau xe, nên ghế ở bên trái ảnh là ghế bên phải của xe.
- D. Vật trong cabin thường ở xa và nhỏ, nhiều vật trong một ảnh.
- E. Cảnh cabin cố định nên không cần guideline hay QC riêng.

**Đáp án: A, B, C, trong phạm vi bài lab.**

- A đúng trong phạm vi DMS của bài: làm mờ toàn bộ mặt sẽ mất chi tiết mắt, mũi, miệng và hướng đầu cần cho model. Không suy rộng thành khẳng định không tồn tại bất kỳ phương pháp ẩn danh nào cho DMS.
- B đúng: ảnh NIR không mang thông tin màu RGB nên không dùng để đoán màu áo.
- C đúng với cấu hình camera OMS của bộ ảnh: camera đặt phía trước nhìn về sau, nên trái ảnh là phải xe.
- D sai: mô tả vật xa, nhỏ và nhiều phù hợp hơn với bối cảnh camera ngoài xe; cabin là không gian quan sát gần và giới hạn.
- E sai: cảnh cố định vẫn cần guideline, tự kiểm và review để bảo đảm nhất quán.

Căn cứ nội dung bài: GUIDE mục 3, 4.4 và các yêu cầu tự kiểm, review chéo.
