# Kịch bản demo — Quản lý Công việc

> Dùng khi trình bày cho giám đốc, trưởng nhóm của văn phòng, agency, đội dự án. Thời lượng 12–15 phút. Đi theo một ngày làm việc: quản lý xem tình hình, giao việc, thành viên cập nhật, quản lý duyệt và theo dõi tiến độ.

---

## 1. Chuẩn bị trước buổi demo

- [ ] Mở sẵn link demo, thử "Đăng nhập nhanh" cả 3 vai trò; đăng nhập thử tài khoản `nhanvien2`
- [ ] Đặt lại dữ liệu demo (thanh công cụ demo → Đặt lại dữ liệu) để hạn công việc tính lại theo hôm nay
- [ ] Đổi tên, logo, màu theo thương hiệu khách (Cài đặt → Thương hiệu) nếu đã biết
- [ ] Chuẩn bị một ảnh thiết kế mẫu dưới 10 MB (vd `banner-trang-chu.png`) để đính kèm khi bình luận
- [ ] Mở link demo trên điện thoại để cho thấy thành viên cập nhật việc khi không ngồi máy tính
- [ ] Ghi nhớ dữ liệu mẫu: dự án APP đang chậm tiến độ (thực tế 58%, kế hoạch 85%); dự án WEB 62%; Phạm Đức Anh quá tải 52 giờ; `WEB-15` "Thiết kế banner trang chủ" của Nguyễn Thu Hà có bật Cần duyệt, checklist 3/5; `MKT-09` của Hà trễ 2 ngày

| Link | Ghi chú |
| :--- | :--- |
| FE | `http://localhost:3115` hoặc link online |
| Swagger | `https://localhost:7115/swagger` (khi khách hỏi về tích hợp) |

| Tài khoản | Vai trò | Dùng để cho xem |
| :--- | :--- | :--- |
| `admin` | Quản trị viên | Phân quyền, thương hiệu |
| `quanly` | Quản lý dự án (Lê Minh Quân) | Tổng quan, tạo dự án, giao việc, duyệt, cân đối khối lượng |
| `nhanvien` | Thành viên (Nguyễn Thu Hà, thiết kế) | Việc của tôi, Kanban, checklist, bình luận |
| `nhanvien2` | Thành viên (Phạm Đức Anh, lập trình) | Chứng minh mỗi người chỉ thấy dự án mình tham gia |

Mật khẩu: giá trị `DEMO_PASSWORD` trong `.env`, hoặc bấm "Đăng nhập nhanh" (riêng `nhanvien2` đăng nhập bằng mật khẩu).

---

## 2. Câu chuyện demo

> Mở đầu: "Anh/chị hình dung sáng thứ Hai, công ty đang chạy cùng lúc mấy dự án cho khách. Thay vì hỏi từng người trên Zalo, em mở phần mềm để anh/chị thấy một ngày giao việc và theo dõi diễn ra thế nào."

| # | Vai trò | Thao tác | Điểm cần nhấn mạnh |
| :---: | :--- | :--- | :--- |
| 1 | Quản lý | Đăng nhập `quanly`, mở Tổng quan: 3 dự án đang chạy, dự án APP màu đỏ Chậm tiến độ, danh sách việc trễ, biểu đồ khối lượng có Phạm Đức Anh quá tải 52 giờ | Không cần hỏi ai, mở máy là biết dự án nào chậm, việc nào trễ, ai đang ôm quá nhiều việc |
| 2 | Quản lý | Bấm cột của Đức Anh, mở `WEB-20` "Kết nối cổng thanh toán" (16 giờ), đổi người làm sang Trần Quốc Bảo; quay lại Tổng quan | Cân lại việc trong một phút; Đức Anh còn 36 giờ, hết nhãn quá tải; Bảo nhận thông báo ngay |
| 3 | Quản lý | Tạo dự án "Website khách sạn Biển Xanh", mã `HTL`, 4 tuần; thêm Hà, Đức Anh, Bảo, Hân làm thành viên | Mỗi dự án có thành viên riêng, người ngoài dự án không nhìn thấy |
| 4 | Quản lý | Trên Kanban `HTL`, thêm việc "Thiết kế trang chủ" giao Nguyễn Thu Hà, hạn thứ Sáu, ưu tiên Cao, 16 giờ, bật Cần duyệt, checklist 4 mục; thêm nhanh 3 việc khác chỉ bằng tiêu đề | Giao việc có đủ người làm, hạn, ưu tiên, các bước; ô người làm hiện ngay ai đang rảnh, ai đang bận |
| 5 | Thành viên | Đổi vai trò sang Nhân viên; bấm chuông thấy "Bạn được giao HTL-1"; mở Việc của tôi | Một chỗ duy nhất cho mọi việc trên mọi dự án: việc trễ `MKT-09` nằm trên cùng, rồi hôm nay, tuần này |
| 6 | Thành viên | Mở Dự án: chỉ có WEB, MKT, BRD, HTL; không có APP, HR | Thành viên chỉ thấy dự án mình tham gia; thông tin dự án khác không lộ |
| 7 | Thành viên | Mở `WEB-15` banner trang chủ: tick 2 mục checklist còn lại, bình luận "@Lê Minh Quân em gửi bản cuối" kèm ảnh thiết kế; kéo thẻ sang Hoàn thành | Trao đổi ngay trên công việc, không trôi tin như nhóm chat; việc cần duyệt tự vào cột Chờ duyệt, không tự đóng được |
| 8 | Thành viên | Thử kéo `WEB-20` của Trần Quốc Bảo | Hệ thống chặn: mỗi người chỉ cập nhật việc của mình, không ai kéo nhầm việc người khác |
| 9 | Quản lý | Đổi sang Quản lý; chuông có "Nguyễn Thu Hà gửi duyệt WEB-15"; xem ảnh, bấm Duyệt (nói thêm: chưa đạt thì bấm Trả lại kèm lý do, việc về Đang làm) | Kiểm soát chất lượng trước khi tính là xong; tiến độ WEB tự tăng từ 62% lên 63%, không ai phải cập nhật báo cáo |
| 10 | Quản lý | Mở WEB tab Lịch, kéo một việc sang ngày khác để dời hạn; tab Danh sách nhóm theo người làm | Cùng dữ liệu xem theo bảng, danh sách, lịch; dời hạn kéo một lần, có lịch sử ai dời |
| 11 | Quản lý | Mở dự án APP: tiến độ thực tế 58% so với kế hoạch 85%, lọc việc trễ hạn; mở dự án HR đang Tạm dừng | Biết vì sao dự án chậm, việc nào kéo lùi; dự án tạm dừng không gửi nhắc, không làm nhiễu số liệu |
| 12 | Quản trị viên | Đổi sang Quản trị viên, bỏ quyền "Tạo công việc" của vai trò Nhân viên; đổi sang Nhân viên để thấy nút Thêm công việc biến mất; đổi màu thương hiệu | Phân quyền tới từng nút theo cách công ty muốn vận hành |

> Kết: "Toàn bộ dữ liệu anh/chị vừa thấy là dữ liệu mẫu. Bản triển khai sẽ dùng dự án, thành viên và quy trình duyệt của công ty mình."

---

## 3. Câu hỏi khách hay hỏi

| Câu hỏi | Trả lời gợi ý |
| :--- | :--- |
| Có nhắc việc qua Zalo, email, Slack không? | Demo nhắc trong ứng dụng lúc 08:00 hằng ngày. Bản triển khai có thể gửi thêm qua email, Zalo OA, Slack hoặc Teams, cần khảo sát kênh công ty đang dùng. |
| Có chat nhóm như Zalo không? | Không làm chat riêng; trao đổi bằng bình luận ngay trên từng công việc để không trôi tin. Bản triển khai có thể thêm cập nhật tức thời khi nhiều người cùng mở bảng. |
| Có biểu đồ Gantt, việc này xong mới làm việc kia không? | Demo chưa có. Bản triển khai có thể thêm Gantt và liên kết phụ thuộc giữa công việc. |
| Có chấm giờ làm thực tế để tính chi phí dự án không? | Demo có ước lượng giờ để cân khối lượng. Ghi giờ thực tế (timesheet) và tính chi phí theo đơn giá nhân sự là phần mở rộng khi triển khai. |
| Khách hàng của agency có xem được tiến độ không? | Demo chưa có. Có thể thêm vai trò Khách hàng chỉ xem tiến độ và duyệt các việc được chia sẻ. |
| Đang dùng Trello, Excel thì chuyển sang thế nào? | Khi triển khai sẽ nhập danh sách dự án, công việc từ Excel hoặc file xuất của Trello. |
| Tệp đính kèm lưu ở đâu, giới hạn bao nhiêu? | Demo cho tối đa 10 MB mỗi tệp. Bản triển khai lưu trên máy chủ riêng hoặc dịch vụ lưu trữ đám mây, giới hạn theo gói. |
| Có app điện thoại không? | Giao diện web dùng tốt trên điện thoại: xem việc, đổi trạng thái, bình luận. App riêng có thông báo đẩy cần khảo sát thêm. |
| Có mẫu dự án dùng lại cho dự án giống nhau không? | Demo có công việc lặp lại (bản P3). Mẫu dự án với danh sách việc dựng sẵn có thể thêm khi triển khai. |

---

## 4. Sau buổi demo

- [ ] Ghi lại yêu cầu khách nêu thêm vào `01-TONG-QUAN-NGHIEP-VU.md`
- [ ] Ghi lại số người, số dự án chạy song song, quy trình duyệt việc, kênh nhắc việc khách đang dùng
- [ ] Gửi link demo và tài khoản `nhanvien`, `quanly` cho khách tự trải nghiệm (nếu đồng ý)
