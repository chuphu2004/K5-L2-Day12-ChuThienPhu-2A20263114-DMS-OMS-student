# Danh sách lớp v0 — Chu Thiên Phú · G09

Viết tiếp từ slide 54 bài giảng. Mỗi lớp trả lời: **model cần nhận ra cái này để làm gì?**

## DMS (ít nhất 6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng DMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | face box | mỗi khung hình một mặt tài xế | Định vị mặt tài xế, làm nền cho mọi chức năng sau (mắt, hướng nhìn, nhận ra tài xế) | Có: đèn NIR chủ động nên ảnh mặt ổn định cả ngày lẫn đêm |
| 2 | eye_left/right | open · closed · unknown | Phát hiện buồn ngủ: mắt nhắm lâu, chớp mắt chậm (PERCLOS) | Có, trừ khi đốm phản xạ trên kính hoặc kính râm che mắt → `unknown` |
| 3 | gaze_zone | road · mirror_l · mirror_r · mirror_c · cluster · center · lap · other | Phát hiện mất tập trung (không nhìn đường quá lâu), kiểm tra tài xế có nhìn gương trước khi chuyển làn | Hướng đầu thấy rõ; hướng mắt khó hơn khi đeo kính hoặc có phản xạ |
| 4 | glasses | unknown · none · clear · sun | Cho biết trạng thái mắt đáng tin đến đâu; đeo kính râm thì phải dựa vào hướng đầu | Kính trong thấy được; kính râm có thể trông trong suốt trên NIR nên dễ ghi nhầm `none` |
| 5 | hand box | whose · side · on_wheel | Cảnh báo tay rời vô lăng, kiểm tra tài xế sẵn sàng tiếp quản ở xe tự lái | Có; tay gần camera có thể bị cháy sáng |
| 6 | phone box | held · mounted · lap | Phát hiện dùng điện thoại khi lái (gọi, nhắn tin) | Có, nhưng màn hình không sáng như ảnh màu; nhận ra máy bằng cạnh, góc |
| 7 | camera_blocked | yes · no | Biết khi nào hệ thống không nhìn thấy gì, để cảnh báo thay vì kết luận sai | Có: khung ảnh tối đều hoặc bị che |

## OMS (ít nhất 6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng OMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | person box | seat · seatbelt | Đếm người, biết ghế nào có người: nhắc thắt dây ghế sau, điều khiển túi khí | Có, nhận bằng hình dạng |
| 2 | seat | driver · front_passenger · rear_left · rear_middle · rear_right | Gắn mỗi đối tượng với đúng ghế để cảnh báo hay bật/tắt túi khí đúng ghế | Có: dựa vào vị trí, không cần màu |
| 3 | seatbelt | worn_correct · worn_incorrect · not_worn · unknown | Nhắc thắt dây theo từng ghế, phát hiện thắt sai cách | Hạn chế: dây và áo tối mất tương phản nên nhiều `unknown`; SVIRO không ai thắt dây nên chưa dạy được `worn_*` |
| 4 | child_seat box | seat · occupied (yes · no · unknown) | Nhắc quên trẻ trong xe (`occupied = yes`, theo chỉ thị coach ca S02); tắt túi khí ghế trước khi có ghế trẻ em | Thấy được ghế; bên trong ghế tối nên khó, dễ phải ghi `occupied = unknown` |
| 5 | infant_seat box | seat · facing (rear · front) | Tắt túi khí ghế trước khi nôi quay về phía sau (`facing = rear`), nhắc quên em bé | Thấy được hình dạng nôi; hướng nôi có thể khó phân biệt |
| 6 | object box | seat · type (bag · box · cup · other) | Nhắc quên đồ khi rời xe; phân biệt đồ vật với người để không báo nhầm có người | Vị trí, kích thước thấy được; loại vật dễ mất vì không có màu → `other` |
| 7 | metadata khung hình | modality · light · camera_id | `modality`, `light` để chọn model/ngưỡng theo loại ảnh và đánh giá theo điều kiện; `camera_id` phân biệt camera DMS/OMS khi xe có nhiều camera | Không áp dụng (thuộc tính của cả khung hình) |

## 2 câu hỏi leo thang

Câu hỏi bạn muốn hỏi người viết guideline (hoặc khách hàng) vì guideline v1.0 chưa trả lời. Mỗi câu kèm **tên khung** làm ví dụ.

1. Câu hỏi: Ghế trẻ em có trẻ em đang ngồi thì gán thế nào? Guideline v1.0 chỉ cho `child_seat.occupied` = `no` / `unknown` và dặn "thấy hình giống trẻ em thì báo coach, không gán". Làm vậy thì ghế có người nhưng không có box người nào, nên model OMS không học được ca quan trọng nhất của ghế trẻ em: nhắc quên trẻ trong xe.
   Khung ví dụ: G09 S02_rgb và S02_ir, ghế `rear_left`.
   Bạn tạm gán thế nào và vì sao: vẽ `child_seat`, `occupied = yes` theo chỉ thị của coach (mentor cập nhật `cabin_schema.py` cho phép `yes`); không vẽ `person` cho trẻ vì guideline chỉ có `person` cho người lớn. Có vẽ box `face` cho mặt trẻ; coach đã xác nhận giữ box này.
2. Câu hỏi: Em bé nằm trong nôi (`infant_seat`) thì gán thế nào? `infant_seat` không có thuộc tính `occupied` nên không phân biệt được nôi trống với nôi có em bé, và guideline không nói có vẽ box `face` cho em bé không (`face` chỉ đi kèm `person` người lớn).
   Khung ví dụ: G09 S01 ghế `rear_right`, S05 ghế `rear_right`, S06 ghế `rear_middle` (cả ảnh RGB và IR).
   Bạn tạm gán thế nào và vì sao: vẽ `infant_seat` với `seat` và `facing`, thêm box `face` cho mặt em bé để không mất thông tin "nôi có người"; không vẽ `person`. Đề xuất cho v1.x: thêm `infant_seat.occupied` (yes / no / unknown) giống `child_seat`.
