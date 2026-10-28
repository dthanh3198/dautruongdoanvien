# ĐẤU TRƯỜNG ĐOÀN VIÊN (bản MVP trắc nghiệm realtime)

Kết nối thanh niên – Bùng nổ tiếng cười.

## Bản này có gì, chưa có gì

**Đã có (chưa được chạy thử, xem mục Kiểm thử):**
MC tạo phòng → mã PIN + QR → đoàn viên nhập biệt danh → MC bắt đầu → cùng trả lời một câu → máy chủ chấm điểm → bảng xếp hạng → trao giải. Có mời người chơi ra, vào lại phòng khi tải lại trang, tự đóng đáp án khi hết giờ, chế độ chiếu toàn màn hình, 12 câu hỏi mẫu có giải thích.

**Chưa có (làm ở các bước sau):** Thật hay thách, Đoán ý đồng đội, Vòng quay may mắn, công cụ MC thêm/sửa câu hỏi, âm thanh, pháo giấy, bộ 100 câu hỏi. Bộ 12 câu mẫu cần MC tự kiểm tra lại trước khi dùng chính thức.

**Công nghệ:** mình chọn trang web tĩnh (HTML + JavaScript, không cần build) thay vì React + Vite, để bạn không phải cài gì và cập nhật dễ hơn. Backend dùng Supabase, đăng tải bằng Vercel. Cả hai có gói miễn phí.

## Bước 1. Tạo Supabase (miễn phí)
1. Mở https://supabase.com, bấm **Start your project**, đăng ký (có thể dùng Google/GitHub).
2. Bấm **New project**. Đặt tên `dau-truong-doan-vien`, đặt mật khẩu database (tự ghi lại), chọn vùng **Southeast Asia (Singapore)**, bấm **Create**. Chờ 1–2 phút.
3. Vào **Authentication → Sign In / Providers** (tên mục có thể khác chút), bật **Allow anonymous sign-ins**, bấm **Save**.
4. Vào **SQL Editor → New query**, mở file `supabase/schema.sql`, dán toàn bộ nội dung, bấm **Run**. Thành công khi hiện "Success". (Nếu báo lỗi, chụp màn hình gửi lại cho mình. Không chạy file này 2 lần.)
5. Vào **Project Settings → API**. Chép **Project URL** và khóa **anon / publishable**.

## Bước 2. Điền cấu hình
Mở `config.js`, thay hai giá trị bằng Project URL và anon key vừa chép. Không dùng khóa `service_role` hay `secret`.

## Bước 3. Đưa lên GitHub
1. Đăng ký https://github.com, bấm **New repository**, tên `dau-truong-doan-vien`, chọn **Public**, **Create**.
2. Bấm **uploading an existing file**, kéo thả `index.html`, `config.js`, thư mục `supabase`, `README.md`, bấm **Commit changes**.

## Bước 4. Đăng lên Vercel (miễn phí)
1. Mở https://vercel.com, đăng nhập bằng GitHub.
2. Bấm **Add New → Project**, chọn repo `dau-truong-doan-vien`, bấm **Import**.
3. Để mặc định (Framework: Other, không cần build), bấm **Deploy**.
4. Xong sẽ có link dạng `https://ten-du-an.vercel.app`. Mở thử trên điện thoại.

Cập nhật sau này: sửa file trên GitHub (hoặc tải file mới đè lên), Vercel tự đăng lại sau vài chục giây.

## Chi phí và giới hạn
- Supabase và Vercel đều có gói miễn phí, nhưng điều kiện có thể thay đổi, hãy xem trang giá của họ. Dự án Supabase miễn phí có thể bị tạm dừng nếu lâu không dùng, hãy mở thử trước buổi sinh hoạt vài ngày.
- Mỗi phòng giới hạn 100 người trong mã. Giới hạn kết nối đồng thời của gói miễn phí chưa được kiểm chứng ở đây, hãy thử với số người thật trước khi dùng.

## Bảo mật (tóm tắt)
- Trình duyệt chỉ đọc dữ liệu, mọi thay đổi (tạo phòng, vào phòng, chấm điểm, điều khiển) đi qua hàm trên máy chủ.
- Đáp án đúng không đọc được từ trình duyệt cho đến khi MC kết thúc câu.
- Điểm do máy chủ tính theo giờ máy chủ. Gửi đáp án hết giờ hoặc gửi lần 2 đều bị bỏ qua.
- Chỉ người tạo phòng mới điều khiển được phòng. Không thu thập họ tên, số điện thoại.

## Kiểm thử trước buổi sinh hoạt (cần bạn làm, mình chưa chạy thử được)
1. MC tạo phòng trên máy tính, thấy PIN và QR.
2. 5 điện thoại/trình duyệt khác nhau quét QR, nhập 5 biệt danh khác nhau. Thử trùng biệt danh, thử PIN sai.
3. MC bấm Bắt đầu: cả 5 máy cùng thấy câu hỏi, đồng hồ gần như trùng.
4. Một máy bấm đáp án 2 lần liên tiếp: điểm chỉ cộng một lần.
5. Một máy tắt Wi-Fi 5 giây rồi bật lại, tải lại trang: vẫn trong phòng, đúng câu hiện tại.
6. Để hết giờ: đáp án tự khóa, hiện đáp án đúng và giải thích.
7. Chơi hết bộ câu: có màn hình chung cuộc, kiểm tra xếp hạng.
8. Bằng điểm: xếp theo số câu đúng, rồi ai vào phòng trước.
