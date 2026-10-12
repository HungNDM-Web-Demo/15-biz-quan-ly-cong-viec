# Kịch bản kiểm thử nghiệm thu — Quản lý Công việc

> Test case theo use case trong `03-USE-CASE.md`. Phần nền (đăng nhập, phân quyền, đặt lại dữ liệu) dùng TC-SYS-01 đến TC-SYS-10 trong `ZDOCS/03-KIEN-TRUC/USE-CASE-NEN.md` §8.

---

## 1. Cách chạy

| Mục | Nội dung |
| :--- | :--- |
| Môi trường | Chạy cả hai chế độ: dữ liệu mẫu (`mock`) và BE thật (`api`) |
| Dữ liệu | Đặt lại dữ liệu demo trước mỗi lượt test; lượt đặt lại tạo sẵn thông báo nhắc hạn của 08:00 hôm nay (BR-18) |
| Thứ tự | Chạy theo thứ tự mã TC trong một lượt; số liệu mong đợi giả định các TC trước đã chạy |
| Tài khoản | Theo cột "Vai trò": Quản lý là `quanly` (Lê Minh Quân), Thành viên là `nhanvien` (Nguyễn Thu Hà) |
| Thiết bị | Desktop 1366×768; TC-12, TC-27 chạy thêm một lần ở cửa sổ 375 px |
| Đạt | Kết quả thực tế khớp toàn bộ cột "Kết quả mong đợi" |

Dữ liệu mẫu dùng trong test:

- **Người:** Lê Minh Quân (`quanly`), Hồ Thanh Tâm (quản lý dự án MKT), Nguyễn Thu Hà (`nhanvien`), Phạm Đức Anh (`nhanvien2`), Trần Quốc Bảo, Võ Ngọc Hân.
- **Dự án `WEB`** "Website bán hàng Nội thất Gỗ Việt": quản lý Lê Minh Quân; bắt đầu hôm nay − 40, kết thúc hôm nay + 20; 60 việc, 2 Đã hủy, 36 Hoàn thành (thực tế 62%, kế hoạch 66%, Đúng tiến độ); thành viên Quân, Hà, Đức Anh, Bảo, Hân.
- **Dự án `APP`** "App đặt lịch Spa Thanh Xuân": quản lý Lê Minh Quân; bắt đầu hôm nay − 60, kết thúc hôm nay + 10; 50 việc, 29 Hoàn thành (thực tế 58%, kế hoạch 85%, Chậm tiến độ); thành viên Quân, Đức Anh, Bảo, không có Hà; có việc `APP-07`.
- **Dự án `MKT`** "Chiến dịch Tết 2027 — Mỹ phẩm Hoa Sen": quản lý Hồ Thanh Tâm, Đang thực hiện; có Hà, Hân.
- **Dự án `HR`** "Tuyển dụng quý 4": quản lý Lê Minh Quân, Tạm dừng; việc `HR-04` hạn hôm qua; không có Hà.
- **Dự án `BRD`** "Bộ nhận diện Cà phê Mộc": Hoàn thành; có Hà.
- **Việc của Hà** (đúng 5 việc mở, khối lượng tuần 28 giờ): `WEB-12` "Thiết kế trang chi tiết sản phẩm" Đang làm, hạn hôm qua, 12 giờ; `WEB-15` "Thiết kế banner trang chủ" Đang làm, hạn hôm nay + 2, 8 giờ, bật Cần duyệt, checklist 5 mục đã xong 3; `MKT-05` "Thiết kế key visual Tết" Đang làm, hạn hôm nay + 4, 8 giờ; `MKT-09` "Thiết kế storyboard TVC Tết" Đang làm, hạn hôm nay − 2, không ước lượng; `MKT-11` "Thiết kế bộ post Facebook tuần 1" Cần làm, hạn ngày mai, không ước lượng.
- **Việc của Đức Anh** (khối lượng tuần 52 giờ, Quá tải): `WEB-20` "Kết nối cổng thanh toán" Đang làm, hạn hôm nay + 3, 16 giờ; `WEB-30` "Kiểm thử giỏ hàng" Đang làm, hạn hôm qua, 12 giờ; các việc APP còn lại 24 giờ.

---

## 2. Test case

### 2.1. Dự án và thành viên

| Mã | UC | Tình huống | Vai trò | Các bước | Kết quả mong đợi |
| :--- | :--- | :--- | :--- | :--- | :--- |
| TC-01 | UC-01 | Tạo dự án | Quản lý | 1. Dự án → Tạo dự án 2. Mã `TST`, tên "Dự án kiểm thử", bắt đầu hôm nay − 10, kết thúc hôm nay + 10 3. Lưu | Dự án Đang thực hiện; Lê Minh Quân là thành viên; tổng quan dự án: thực tế 0%, kế hoạch 50%, "Chậm tiến độ" (0 nhỏ hơn 50 − 10); Kanban 4 cột trống |
| TC-02 | UC-01 | Dữ liệu dự án không hợp lệ | Quản lý | 1. Tạo dự án mã `WEB` 2. Mã `T` 3. Mã `1AB` 4. Mã `TST2`, ngày kết thúc trước ngày bắt đầu | Bước 1: "Mã dự án đã tồn tại". Bước 2, 3: "Mã dự án không đúng định dạng". Bước 4: lỗi tại ô ngày kết thúc. Không dự án nào được tạo |
| TC-03 | UC-01 | Thành viên chỉ thấy dự án tham gia | Thành viên | 1. Mở Dự án 2. Gõ URL tổng quan dự án APP 3. Gõ URL chi tiết `APP-07` | Bước 1: chỉ có WEB, MKT, BRD; không có APP, HR, TST; không có nút Tạo dự án. Bước 2, 3: "Không tìm thấy dự án hoặc bạn không phải thành viên" |
| TC-04 | UC-02 | Thêm thành viên | Quản lý, Thành viên | 1. Dự án TST → tab Thành viên → Thêm: Nguyễn Thu Hà, Phạm Đức Anh, Trần Quốc Bảo 2. Đổi sang Nhân viên, mở Dự án | Bước 1: 3 người vào danh sách, mỗi người có thông báo "Bạn được thêm vào dự án Dự án kiểm thử". Bước 2: Hà thấy TST |
| TC-05 | UC-02 | Gỡ thành viên còn việc mở | Quản lý | 1. Kanban TST, thêm nhanh "Chuẩn bị dữ liệu thử" ở cột Cần làm; mở chi tiết, giao Trần Quốc Bảo 2. Tab Thành viên, bấm Gỡ ở Bảo 3. Chọn giao lại cho Phạm Đức Anh, xác nhận | Bước 1: việc có mã `TST-1`. Bước 2: hộp liệt kê `TST-1`. Bước 3: `TST-1` của Đức Anh, lịch sử ghi đổi người làm, Đức Anh có thông báo được giao; Bảo không còn trong danh sách thành viên |
| TC-06 | UC-02 | Gỡ quản lý dự án | Quản lý | 1. Tab Thành viên TST, xem dòng Lê Minh Quân | Nút Gỡ bị vô hiệu, chú thích "Đổi quản lý dự án trước" |

### 2.2. Tạo và giao công việc

| Mã | UC | Tình huống | Vai trò | Các bước | Kết quả mong đợi |
| :--- | :--- | :--- | :--- | :--- | :--- |
| TC-07 | UC-04 | Tạo việc đầy đủ | Quản lý | 1. Kanban TST → Thêm công việc 2. Tiêu đề "Thiết kế trang đăng nhập", người làm Nguyễn Thu Hà, bắt đầu hôm nay, hạn hôm nay + 3, ưu tiên Cao, ước lượng 8 giờ, bật Cần duyệt, checklist "Wireframe", "Giao diện desktop", "Giao diện mobile", "Bàn giao file" 3. Lưu | Mã `TST-2`, đầu cột Cần làm; thẻ hiện ưu tiên Cao, hạn, checklist 0/4; Hà có thông báo "Bạn được giao TST-2 Thiết kế trang đăng nhập, hạn {dd/MM/yyyy}" |
| TC-08 | UC-04 | Dữ liệu công việc không hợp lệ | Quản lý | 1. Thêm công việc tiêu đề "AB" 2. Tiêu đề "Tài liệu bàn giao", hạn hôm qua 3. Bắt đầu hôm nay + 5, hạn hôm nay + 3 4. Bỏ ngày bắt đầu, hạn hôm nay + 15, để trống người làm, lưu | Bước 1–3: báo lỗi tại ô tương ứng, không lưu. Bước 4: cảnh báo vàng "Hạn sau ngày kết thúc dự án", vẫn lưu; mã `TST-3`, Chưa giao |
| TC-09 | UC-04 | Thành viên tạo việc | Thành viên | 1. Kanban TST, gõ "Chuẩn bị bộ icon" vào ô thêm nhanh cột Cần làm, Enter 2. Mở chi tiết `TST-4` | Bước 1: việc `TST-4`, người làm Nguyễn Thu Hà, ưu tiên Trung bình, không có hạn. Bước 2: ô người làm chỉ đọc |
| TC-10 | UC-04 | Cảnh báo sắp quá tải | Quản lý | 1. Kanban WEB → Thêm công việc "Chỉnh giao diện giỏ hàng" 2. Mở ô người làm 3. Chọn Nguyễn Thu Hà, ước lượng 8 giờ, hạn hôm nay + 3, lưu 4. Mở Tổng quan | Bước 2: Hà hiện "36/40 giờ" (28 giờ có sẵn + 8 giờ của `TST-2`). Bước 3: cảnh báo vàng "Sẽ quá tải: 44 giờ trong 7 ngày", vẫn lưu được. Bước 4: cột của Hà 44 giờ, nhãn "Quá tải" |

### 2.3. Bảng Kanban

| Mã | UC | Tình huống | Vai trò | Các bước | Kết quả mong đợi |
| :--- | :--- | :--- | :--- | :--- | :--- |
| TC-11 | UC-05 | Lọc và nhãn hạn | Thành viên | 1. Kanban WEB, bấm "Việc của tôi" 2. Thêm lọc hạn "Trễ hạn" | Bước 1: chỉ còn thẻ Hà làm; việc mở gồm `WEB-12` nhãn đỏ "Trễ 1 ngày", `WEB-15`, "Chỉnh giao diện giỏ hàng". Bước 2: chỉ còn `WEB-12` |
| TC-12 | UC-05 | Hoàn thành việc của mình | Thành viên | 1. Xem tiến độ ở tổng quan dự án WEB 2. Kéo `WEB-12` từ Đang làm sang Hoàn thành 3. Xem lại tổng quan dự án | Bước 1: 61% (36 ÷ 59 việc không hủy). Bước 2: `WEB-12` ở Hoàn thành, ngày hoàn thành hôm nay, mất nhãn trễ. Bước 3: 62% (37 ÷ 59 = 62,7 làm tròn xuống) |
| TC-13 | UC-05 | Kéo việc của người khác | Thành viên | 1. Bỏ lọc, kéo `WEB-20` (người làm Phạm Đức Anh) sang Hoàn thành | Thẻ trả về Đang làm, báo "Bạn chỉ cập nhật được việc mình làm hoặc mình tạo" |
| TC-14 | UC-05 | Việc cần duyệt thả vào Hoàn thành | Thành viên | 1. Kéo `WEB-15` (Cần duyệt, checklist 3/5) sang Hoàn thành | Thẻ vào cột Chờ duyệt, báo "Việc cần quản lý duyệt"; không hỏi checklist; Lê Minh Quân có thông báo gửi duyệt; tiến độ WEB giữ 62% |
| TC-15 | UC-05 | Hoàn thành khi checklist chưa xong | Thành viên | 1. Mở `TST-4`, thêm checklist "Icon menu", "Icon giỏ hàng", tick "Icon menu" 2. Kéo `TST-4` sang Hoàn thành 3. Chọn Hủy 4. Kéo lại, chọn "Vẫn hoàn thành" | Bước 2: hỏi "Còn 1/2 mục chưa xong. Vẫn hoàn thành?". Bước 3: thẻ về Cần làm. Bước 4: thẻ ở Hoàn thành |
| TC-16 | UC-05 | Dự án đã hoàn thành chỉ xem | Thành viên | 1. Mở Kanban dự án BRD 2. Thử kéo một thẻ; mở một công việc | Không kéo được; không có ô thêm nhanh; chi tiết công việc không có khung bình luận, mọi ô chỉ đọc |

### 2.4. Chi tiết công việc và checklist

| Mã | UC | Tình huống | Vai trò | Các bước | Kết quả mong đợi |
| :--- | :--- | :--- | :--- | :--- | :--- |
| TC-17 | UC-06 | Checklist và lịch sử | Thành viên | 1. Mở `TST-2`, tick "Wireframe", "Giao diện desktop" 2. Đổi ưu tiên Cao thành Khẩn cấp 3. Xem Lịch sử, quay lại Kanban TST | Bước 1: checklist 2/4. Bước 3: lịch sử có "Nguyễn Thu Hà đổi ưu tiên từ Cao sang Khẩn cấp"; thẻ hiện 2/4, ưu tiên Khẩn cấp |
| TC-18 | UC-06 | Xem việc của người khác | Thành viên | 1. Mở `TST-1` (người làm Phạm Đức Anh) | Mọi ô và checklist chỉ đọc; vẫn có khung bình luận |
| TC-19 | UC-06 | Đổi hạn về quá khứ | Thành viên | 1. Ở `TST-2`, sửa hạn thành hôm qua | Báo "Hạn không được trước hôm nay"; hạn giữ hôm nay + 3 |
| TC-20 | UC-06 | Hủy và khôi phục | Quản lý | 1. Mở `TST-3`, bấm Hủy công việc, để trống lý do 2. Nhập lý do "Gộp vào TST-2", xác nhận 3. TST → Danh sách, nhóm theo trạng thái, mở `TST-3` ở nhóm Đã hủy, bấm Khôi phục | Bước 1: không xác nhận được. Bước 2: `TST-3` Đã hủy, rời Kanban. Bước 3: `TST-3` về cột Cần làm |

### 2.5. Duyệt, bình luận, đính kèm

| Mã | UC | Tình huống | Vai trò | Các bước | Kết quả mong đợi |
| :--- | :--- | :--- | :--- | :--- | :--- |
| TC-21 | UC-07 | Trả lại rồi duyệt | Quản lý, Thành viên | 1. Quản lý mở thông báo gửi duyệt `WEB-15`, bấm Trả lại, để trống lý do 2. Nhập "Đổi màu nút theo bộ nhận diện", xác nhận 3. Đổi sang Nhân viên, tick 2 mục checklist còn lại, kéo `WEB-15` sang Hoàn thành 4. Đổi sang Quản lý, kéo `WEB-15` từ Chờ duyệt sang Hoàn thành | Bước 1: không xác nhận được. Bước 2: `WEB-15` về Đang làm, có bình luận chứa lý do, Hà có thông báo bị trả lại. Bước 3: thẻ vào Chờ duyệt. Bước 4: Hoàn thành, người duyệt Lê Minh Quân, không hỏi checklist (5/5); tiến độ WEB 64% (38 ÷ 59) |
| TC-22 | UC-08 | Bình luận nhắc tên kèm ảnh | Thành viên, Quản lý | 1. Mở `TST-2`, gõ "@" chọn Lê Minh Quân, nội dung "nhờ anh xem bản desktop", đính kèm ảnh png 2 MB 2. Gửi 3. Đổi sang Quản lý, bấm chuông | Bước 2: bình luận hiện ngay, ảnh có xem trước. Bước 3: có thông báo "Nguyễn Thu Hà nhắc bạn trong TST-2" |
| TC-23 | UC-08 | Tệp quá lớn, sai định dạng | Thành viên | 1. Ở `TST-2`, đính kèm tệp pdf 11 MB 2. Đính kèm tệp `.exe` | Lần lượt báo "Tệp tối đa 10 MB", "Định dạng không được hỗ trợ"; không tệp nào được tải lên |
| TC-24 | UC-08 | Sửa bình luận | Thành viên | 1. Sửa bình luận ở TC-22 thành "nhờ anh xem bản desktop và mobile" 2. Mở `WEB-15`, xem bình luận lý do trả lại của Lê Minh Quân | Bước 1: bình luận hiện "(đã sửa)". Bước 2: không có nút Sửa, Xóa |

### 2.6. Danh sách, lịch, việc của tôi

| Mã | UC | Tình huống | Vai trò | Các bước | Kết quả mong đợi |
| :--- | :--- | :--- | :--- | :--- | :--- |
| TC-25 | UC-09 | Sắp xếp dạng danh sách | Quản lý | 1. Mở `TST-1`, đặt hạn hôm nay + 3, ưu tiên Thấp 2. TST → tab Danh sách | Thứ tự: `TST-2` (hôm nay + 3, Khẩn cấp), `TST-1` (hôm nay + 3, Thấp), `TST-3` (hôm nay + 15), cuối cùng `TST-4` (không có hạn) |
| TC-26 | UC-09 | Kéo đổi hạn trên lịch | Quản lý | 1. TST → tab Lịch, kéo `TST-2` từ hôm nay + 3 sang hôm nay + 5 2. Kéo `TST-2` sang hôm qua | Bước 1: hạn mới hôm nay + 5, lịch sử ghi lại. Bước 2: thẻ về hôm nay + 5, báo "Hạn không được trước hôm nay" |
| TC-27 | UC-10 | Việc của tôi | Thành viên | 1. Mở Việc của tôi | Nhóm Trễ hạn có `MKT-09` "Trễ 2 ngày". Nhóm 7 ngày tới theo thứ tự: `MKT-11` (ngày mai), "Chỉnh giao diện giỏ hàng" (hôm nay + 3), `MKT-05` (hôm nay + 4), `TST-2` (hôm nay + 5). Không có việc đã Hoàn thành, không có việc của người khác |
| TC-28 | UC-10 | Thông báo nhắc hạn | Thành viên, Quản lý | 1. Đăng nhập nhanh vai trò Nhân viên, bấm chuông 2. Đổi sang Quản lý, bấm chuông | Bước 1: có "MKT-09 Thiết kế storyboard TVC Tết đã trễ hạn 2 ngày" và "MKT-11 Thiết kế bộ post Facebook tuần 1 đến hạn ngày mai". Bước 2: có "WEB-30 Kiểm thử giỏ hàng (Phạm Đức Anh) đã trễ hạn"; không có thông báo cho `HR-04` vì dự án HR đang Tạm dừng |

### 2.7. Tổng quan và trạng thái dự án

| Mã | UC | Tình huống | Vai trò | Các bước | Kết quả mong đợi |
| :--- | :--- | :--- | :--- | :--- | :--- |
| TC-29 | UC-11 | Tiến độ tính theo công việc | Quản lý | 1. Kanban TST, thêm nhanh 6 việc `TST-5` đến `TST-10`; mở tổng quan dự án 2. Kéo `TST-5`, `TST-6` sang Hoàn thành 3. Kéo `TST-7` sang Hoàn thành 4. Hủy `TST-8`, lý do "Trùng việc" 5. Kéo `TST-9` sang Hoàn thành | Kế hoạch luôn 50%. Bước 1: 10 việc, 1 hoàn thành (`TST-4`), 10%, Chậm tiến độ. Bước 2: 3 ÷ 10 = 30%, Chậm tiến độ. Bước 3: 4 ÷ 10 = 40%, Đúng tiến độ. Bước 4: 4 ÷ 9 = 44%, Đúng tiến độ. Bước 5: 5 ÷ 9 = 55% (55,6 làm tròn xuống), Đúng tiến độ |
| TC-30 | UC-11 | Tổng quan của quản lý | Quản lý | 1. Mở Tổng quan | Bảng tiến độ có WEB (64%, Đúng tiến độ), APP (58%, kế hoạch 85%, Chậm tiến độ), MKT, TST (55%, kế hoạch 50%, Đúng tiến độ); không có HR, BRD. Biểu đồ khối lượng: Phạm Đức Anh 52 giờ, "Quá tải". Danh sách việc trễ có `WEB-30`, `MKT-09`; không có `WEB-12`, `HR-04` |
| TC-31 | UC-11 | Tổng quan của thành viên | Thành viên | 1. Đăng nhập nhanh vai trò Nhân viên | Việc của tôi: Cần làm 3, Đang làm 2, Chờ duyệt 0; trễ hạn 1; đến hạn hôm nay 0; tiến độ dự án tham gia có WEB, MKT, TST, không có APP, BRD; không có biểu đồ khối lượng của người khác |
| TC-32 | UC-11 | Tỉ lệ đúng hạn không có mẫu số | Quản lý | 1. Tổng quan, lọc dự án TST | Thẻ tỉ lệ đúng hạn hiển thị "—" vì các việc hoàn thành của TST đều không có hạn; thẻ dự án đang thực hiện là 1 |
| TC-33 | UC-03 | Đóng dự án còn việc mở, tạm dừng | Quản lý, Thành viên | 1. Dự án TST → Trạng thái → Hoàn thành 2. Chọn Tạm dừng 3. Đổi sang Nhân viên, mở Kanban TST 4. Đổi về Quản lý, chọn Tiếp tục | Bước 1: báo còn 4 việc mở (`TST-1`, `TST-2`, `TST-3`, `TST-10`), không đổi trạng thái. Bước 2: TST Tạm dừng. Bước 3: bảng chỉ xem, không kéo được. Bước 4: TST về Đang thực hiện |

---

## 3. Biên bản chạy thử

| Ngày | Người test | Chế độ | Số TC đạt / tổng | Lỗi ghi nhận |
| :--- | :--- | :--- | :---: | :--- |
| | | | | |
