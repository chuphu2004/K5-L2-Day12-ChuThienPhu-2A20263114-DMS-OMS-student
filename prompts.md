# Khai báo dùng AI — Chu Thiên Phú

Không dùng AI thì xóa bảng và ghi: **Không dùng.**

Nhắc lại: không đưa ảnh cabin hay ảnh tài xế (kể cả ảnh chụp màn hình) cho bất kỳ công cụ AI nào.

| # | Công cụ | Bạn hỏi gì (tóm tắt) | Bạn dùng kết quả thế nào | Bạn có kiểm lại không? Bằng gì? |
|---|---|---|---|---|
| 1 | Claude Code (CLI) | Setup môi trường: giải nén G09, tạo project Day12 + task Day12-G09 (22 ảnh) qua API CVAT local; tóm tắt guideline và chỉ ra chỗ guideline/script chưa rõ thành 1 file HTML | Dùng làm checklist khi gán; tự gán nhãn toàn bộ, AI không xem ảnh | Có: kiểm task 22 ảnh trên CVAT, đối chiếu tóm tắt với GUIDE.md |
| 2 | Claude Code (CLI) | Nâng CVAT local 2.74.1 → 2.82.0 (để copy nhiều shape); chạy cabin_check ở Checkpoint A, B, lần cuối; so XML để tìm box dán trùng, seat lệch phía ảnh, trái/phải face13; xoá các box/tag trùng qua API theo yêu cầu của mình | Tự sửa nhãn trên CVAT (seat S04, mắt D01/D03/D05/D06, D06); AI chỉ đọc XML, không xem ảnh | Có: chạy lại cabin_check sau mỗi lần sửa, mở CVAT kiểm danh sách object |
| 3 | Claude Code (CLI) | Làm trang HTML gợi ý quan sát cho ir_log và tạo task Day12-G09-extra (S09–S10) | Tự quan sát ảnh và tự viết các dòng ir_log | Có: đối chiếu yêu cầu E4 trong SUBMISSION/RUBRIC |
| 4 | Claude Code (CLI) | Thử file cabin_schema.py mentor gửi (thêm occupied=yes) rồi thay vào scripts/; export + check lại sau khi sửa D02; sửa dòng D02 trong ir_log; điền bảng lỗi đã gặp vào self_review từ kết quả cabin_check | Phần "vì sao / cách tránh", class_list_v0 và exit ticket tự viết | Có: chạy cabin_check với giá trị sai để chắc script vẫn bắt lỗi |
| 5 | Claude Code (CLI) | Chép danh sách lớp mình soạn vào class_list_v0, thêm `unknown` cho glasses; soạn 2 câu hỏi leo thang từ 2 ca mình đã gặp và đã hỏi coach (S02 trẻ trong ghế trẻ em; em bé trong nôi S01/S05/S06) | Đọc lại, giữ vì đúng cách mình đã gán; cột "Để làm gì" và "Nhìn thấy trên IR" tự viết | Có: đối chiếu với nhãn trong export_final và chỉ thị của coach |
