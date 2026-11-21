# Danh sách lớp v0 — Chu Thiên Phú · G09

Viết tiếp từ slide 54 bài giảng. Mỗi lớp trả lời: **model cần nhận ra cái này để làm gì?**

## DMS (ít nhất 6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng DMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | face box | mỗi khung hình một mặt tài xế | | |
| 2 | eye_left/right | open · closed · unknown | | |
| 3 | gaze_zone | road · mirror_l · mirror_r · mirror_c · cluster · center · lap · other | | |
| 4 | glasses | unknown · none · clear · sun | | |
| 5 | hand box | whose · side · on_wheel | | |
| 6 | phone box | held · mounted · lap | | |
| 7 | camera_blocked | yes · no | | |

## OMS (ít nhất 6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng OMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | person box | seat · seatbelt | | |
| 2 | seat | driver · front_passenger · rear_left · rear_middle · rear_right | | |
| 3 | seatbelt | worn_correct · worn_incorrect · not_worn · unknown | | |
| 4 | child_seat box | seat · occupied (yes · no · unknown) | | |
| 5 | infant_seat box | seat · facing (rear · front) | | |
| 6 | object box | seat · type (bag · box · cup · other) | | |
| 7 | metadata khung hình | modality · light · camera_id | | |

## 2 câu hỏi leo thang

Câu hỏi bạn muốn hỏi người viết guideline (hoặc khách hàng) vì guideline v1.0 chưa trả lời. Mỗi câu kèm **tên khung** làm ví dụ.

1. Câu hỏi: Ghế trẻ em có trẻ em đang ngồi thì gán thế nào? Guideline v1.0 chỉ cho `child_seat.occupied` = `no` / `unknown` và dặn "thấy hình giống trẻ em thì báo coach, không gán". Làm vậy thì ghế có người nhưng không có box người nào, nên model OMS không học được ca quan trọng nhất của ghế trẻ em: nhắc quên trẻ trong xe.
   Khung ví dụ: G09 S02_rgb và S02_ir, ghế `rear_left`.
   Bạn tạm gán thế nào và vì sao: vẽ `child_seat`, `occupied = yes` theo chỉ thị của coach (mentor cập nhật `cabin_schema.py` cho phép `yes`); không vẽ `person` cho trẻ vì guideline chỉ có `person` cho người lớn. Có vẽ box `face` cho mặt trẻ; coach đã xác nhận giữ box này.
2. Câu hỏi: Em bé nằm trong nôi (`infant_seat`) thì gán thế nào? `infant_seat` không có thuộc tính `occupied` nên không phân biệt được nôi trống với nôi có em bé, và guideline không nói có vẽ box `face` cho em bé không (`face` chỉ đi kèm `person` người lớn).
   Khung ví dụ: G09 S01 ghế `rear_right`, S05 ghế `rear_right`, S06 ghế `rear_middle` (cả ảnh RGB và IR).
   Bạn tạm gán thế nào và vì sao: vẽ `infant_seat` với `seat` và `facing`, thêm box `face` cho mặt em bé để không mất thông tin "nôi có người"; không vẽ `person`. Đề xuất cho v1.x: thêm `infant_seat.occupied` (yes / no / unknown) giống `child_seat`.
