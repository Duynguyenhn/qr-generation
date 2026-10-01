# Tạo QR Hàng Loạt

Công cụ tạo hàng loạt mã QR từ danh sách Excel hoặc CSV. Chỉ cần nạp file, chọn cột, bấm một nút là tải về file ZIP chứa toàn bộ ảnh QR, mỗi ảnh đặt tên theo cột bạn chọn.

**Dùng ngay:** https://duynguyenhn.github.io/qr-generation/

- Không cần cài đặt, không cần tài khoản. Mở bằng Chrome, Edge hoặc Firefox là dùng được.
- Dữ liệu không rời khỏi máy bạn. File Excel được đọc và mã QR được tạo ngay trong trình duyệt, không gửi lên máy chủ nào.
- Mỗi mã được quét lại sau khi tạo để kiểm tra đọc đúng nội dung.

---

## Cách dùng

### Bước 1: Nạp danh sách

Kéo thả file vào ô **"Kéo thả file vào đây"**, hoặc bấm vào ô để chọn file.

- Nhận các định dạng: `.xlsx`, `.xls`, `.csv`
- Dòng đầu tiên nên là tiêu đề cột. Nếu file không có tiêu đề, bỏ tick ô **"Dòng đầu tiên là tiêu đề cột"**.
- File Excel có nhiều sheet thì chọn đúng sheet ở ô **Sheet**.

Khi mới mở, trang hiển thị sẵn **dữ liệu mẫu** (nhãn vàng "Dữ liệu mẫu"). Dữ liệu này chỉ để xem thử, không phải dữ liệu thật.

Ví dụ một file đúng chuẩn:

| STT | Mã sản phẩm | Link QR |
|---|---|---|
| 1 | SP-000001 | https://example.com/sp/a1B2c3D4 |
| 2 | SP-000002 | https://example.com/sp/e5F6g7H8 |

### Bước 2: Chọn cột

| Ô | Ý nghĩa | Ví dụ |
|---|---|---|
| **Cột tên file** | Giá trị trong cột này thành tên ảnh | `SP-000001` → `SP-000001.png` |
| **Cột nội dung QR** | Nội dung được mã hoá vào QR | Link, văn bản, số điện thoại… |

Công cụ tự đoán cột: cột chứa link được chọn làm nội dung, cột kiểu mã/serial được chọn làm tên file. Bạn kiểm tra lại và đổi nếu đoán sai.

Bấm vào một dòng trong bảng để xem trước mã QR của dòng đó ở khung **Bản xem trước** bên phải.

### Bước 3: Thông số QR

Thông số mặc định là chuẩn đang dùng cho tem in. Nếu không có yêu cầu khác, giữ nguyên.

| Thông số | Mặc định | Giải thích |
|---|---|---|
| Vùng QR | 850 px | Kích thước phần mã QR (không tính viền) |
| Viền trắng mỗi cạnh | 75 px | Khoảng trắng bao quanh mã |
| Mức sửa lỗi | M (15%) | Mã chịu được bao nhiêu phần trăm bị bẩn, mờ, che. Chọn **H** nếu định đặt logo vào giữa mã |
| Màu QR / Màu nền | Đen / Trắng | Nên giữ mã tối trên nền sáng. Mã màu nhạt hoặc nền tối nhiều app không quét được |
| PPI ghi vào PNG | 300 | Quyết định kích thước khi đặt ảnh vào phần mềm dàn trang. 1000 px ở 300 PPI ≈ 84,7 mm |

Với thông số mặc định, mỗi ảnh xuất ra là **PNG 1000 × 1000 px**.

### Bước 4: Tạo và tải về

1. Kiểm tra **Tên folder / file ZIP**. Công cụ tự đặt theo mã đầu và mã cuối, ví dụ `QR_SP_000001-000500`. Bạn sửa lại được.
2. Nên để tick **"Quét lại từng mã sau khi tạo để kiểm tra"**.
3. Bấm **Tạo và tải ZIP** và chờ thanh tiến trình chạy hết. Đừng đóng tab trong lúc chạy. Muốn dừng giữa chừng thì bấm **Dừng**.
4. File ZIP tự tải về thư mục Downloads.

---

## File ZIP tải về gồm gì

```
QR_SP_000001-000500.zip
└─ QR_SP_000001-000500/
   ├─ SP-000001.png
   ├─ SP-000002.png
   ├─ …
   ├─ SP-000500.png
   └─ _danh_sach.csv
```

File **`_danh_sach.csv`** liệt kê từng ảnh với dòng gốc trong Excel, nội dung QR, version và kết quả quét. Mở bằng Excel để đối chiếu.

| Cột `kiem_tra` | Ý nghĩa |
|---|---|
| `OK` | Mã quét lại đọc đúng nội dung |
| `CHƯA ĐỌC ĐƯỢC` | Bộ quét trong trình duyệt chưa đọc được. Mở ảnh đó và quét thử bằng điện thoại |
| `không quét` | Bạn đã tắt bước quét lại |
| `LỖI: nội dung quá dài` | Nội dung vượt sức chứa của QR, không có ảnh. Rút gọn nội dung hoặc hạ mức sửa lỗi |

---

## Kiểm tra dữ liệu

Khung **Kiểm tra dữ liệu** bên phải báo các vấn đề trước khi bạn bấm tạo:

| Cảnh báo | Công cụ xử lý thế nào | Bạn nên làm gì |
|---|---|---|
| **Tên trùng** | Tự thêm hậu tố `_2`, `_3` để không ghi đè ảnh | Kiểm tra lại file gốc, tên trùng thường là lỗi dữ liệu |
| **Nội dung trùng** | Vẫn tạo bình thường | Hai tem cùng link là đáng ngờ, nên hỏi lại nguồn dữ liệu |
| **Ô nội dung trống** | Bỏ qua dòng đó | Bổ sung nội dung nếu dòng đó cần có mã |
| **Tên đổi ký tự** | Thay các ký tự Windows cấm (`\ / : * ? " < > \|`) bằng `_` | Không cần làm gì |

---

## Lưu ý

- **Cần có mạng khi mở trang** để tải thư viện xử lý. Sau khi trang đã mở, việc tạo mã chạy hoàn toàn trên máy.
- **Thời gian chạy:** vài trăm mã mất vài giây, vài nghìn mã mất vài phút tuỳ cấu hình máy. Tắt bước quét lại sẽ nhanh hơn nhưng không nên.
- **Mã QR là mã tĩnh:** nội dung được mã hoá thẳng vào ảnh, không qua dịch vụ trung gian, không hết hạn. Muốn đổi nội dung thì phải tạo và in lại mã.
- **In thử trước khi in số lượng lớn:** in vài tem ở đúng kích thước thật, quét bằng cả iPhone và Android. Nếu link trong mã là link kích hoạt hoặc chỉ dùng một lần, quét thử có thể làm link đó đổi trạng thái, nên dùng tem in thử rồi huỷ.
- **Kích thước in tối thiểu:** mã càng nhiều nội dung càng dày. Link ngắn in từ khoảng 15 mm vẫn quét tốt; nội dung dài (vCard, văn bản) nên in lớn hơn.

---

## Câu hỏi thường gặp

**Tải về bị chặn hoặc không thấy file?**
Kiểm tra thư mục Downloads và thanh tải xuống của trình duyệt. Một số trình duyệt hỏi xác nhận khi trang tải file lớn, hãy chọn **Giữ lại / Keep**.

**File CSV mở ra bị lỗi font tiếng Việt?**
Lưu CSV từ Excel bằng **CSV UTF-8 (Comma delimited)**. Công cụ cũng đọc được file `.xlsx` trực tiếp, nên dùng `.xlsx` cho chắc.

**Serial có số 0 ở đầu bị mất (`000123` thành `123`)?**
Công cụ đọc giá trị đúng như Excel hiển thị. Nếu trong Excel đã mất số 0 thì định dạng cột đó là **Text** trước khi nhập dữ liệu.

**Mã có đọc được bằng mọi app quét QR không?**
Có. Mã theo chuẩn QR Code thông thường, mức sửa lỗi M, đọc được bằng camera điện thoại và các app quét phổ biến.
