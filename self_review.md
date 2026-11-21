# Tự đánh giá — Chu Thiên Phú · G09

## 1. Tự rà soát 4 cảnh

Nghỉ tay 1 phút, mở lại bài của mình, chọn 4 ảnh (2 S##, 2 D##), đọc như người lạ.

Loại lỗi: `seat_flip`, `wrong_class`, `guess`, `box`, `missing`, `extra`, `lr_flip` (trái/phải mặt), `flag` (thiếu cờ điểm), `ok`.

| Ảnh | Đối tượng | Loại lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|
| S01_rgb | mọi box (child_seat, object, face, infant_seat) | `extra` | Dán shape 2 lần lên chính ảnh RGB, box trùng khít nên trên canvas trông như 1 | Có (xoá bản trùng, Checkpoint A) |
| S04_rgb / S04_ir | infant_seat bên trái ảnh | `seat_flip` | Ghi `rear_left` theo ảnh; trái ảnh là `rear_right` (GUIDE §4.4-3) | Có |
| D03 | face: eye_left, eye_right | `flag` | Ghi `open` nhưng cả 4 điểm mỗi mắt bật `occluded`, hai thông tin mâu thuẫn | Có |
| D02 | person.seatbelt | `guess` | Tài xế đang thắt dở mà ghi `not_worn`; guideline §4.7 là `unknown` | Có |

## 2. Lỗi mình lặp lại nhiều nhất hôm nay

Lỗi: dán shape trùng (Ctrl+V hai lần), gặp 3 lần: S01_rgb/S02_rgb (cả tag frame_meta), S03_ir, và cả 4 ảnh task bonus S09–S10.

Vì sao mình mắc: … (bạn tự viết; gợi ý từ dữ liệu: box trùng có toạ độ khít nhau nên nhìn canvas không thấy, mình chỉ kiểm bằng mắt trên ảnh)

Lần sau tránh bằng cách: … (bạn tự viết)

## 3. Ghi chú về disagreement_log

Một dòng bạn của mình đúng và mình sai. Mình học được gì từ dòng đó: review chéo với Lưu Nhật Nam (45 dòng bất đồng ở 22 ảnh chính) không có dòng nào `verdict = peer`; Nam xác nhận bản của mình đúng. …
