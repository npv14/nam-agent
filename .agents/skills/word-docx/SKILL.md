---
name: Word / DOCX
slug: word-docx
version: 1.0.2
homepage: https://clawic.com/skills/word-docx
description: "Create, inspect, and edit Microsoft Word documents and DOCX files with reliable styles, numbering, tracked changes, tables, sections, and compatibility checks. Use when (1) the task is about Word or `.docx`; (2) the file includes tracked changes, comments, fields, tables, templates, or page layout constraints; (3) the document must survive round-trip editing without formatting drift."
changelog: Tightened the skill around fragile review workflows, reference stability, and layout drift after a stricter external audit.
metadata: {"clawdbot":{"emoji":"📘","os":["linux","darwin","win32"]}}
---
## Khi Nào Sử Dụng

Sử dụng khi đầu ra chính là tài liệu Microsoft Word hoặc file `.docx`, đặc biệt khi có theo dõi thay đổi, bình luận, tiêu đề, đánh số, trường, bảng, mẫu, hoặc yêu cầu tương thích.

## Quy Tắc Cốt Lõi

### 1. Xử lý DOCX như OOXML, không phải văn bản thuần

- File `.docx` là một ZIP gồm các phần XML, vì vậy cấu trúc quan trọng không kém văn bản hiển thị.
- Các phần quan trọng thường là `word/document.xml`, `styles.xml`, `numbering.xml`, tiêu đề, chân trang, và các file quan hệ.
- Văn bản có thể bị chia thành nhiều run; không bao giờ giả định một từ hay câu nằm trong một node XML duy nhất.
- Sử dụng các quy trình khác nhau có chủ đích: trích xuất có cấu trúc để đọc nhanh, tạo theo kiểu style cho file mới, và chỉnh sửa OOXML-aware cho tài liệu hiện có dễ hỏng.
- Nếu công việc chủ yếu là đọc, trích xuất, hoặc xem xét, ưu tiên đường dẫn đọc bảo toàn cấu trúc trước khi chạm vào OOXML.
- Với các chỉnh sửa sâu, kiểm tra bố cục gói thay vì chỉ dựa vào đầu ra được hiển thị.
- Đọc, tạo, và bảo toàn tài liệu đã xem xét là các công việc khác nhau dù định dạng giống nhau.
- Đầu vào `.doc` cũ thường cần chuyển đổi trước khi tin tưởng các giả định `.docx` hiện đại.

### 2. Bảo toàn style và định dạng trực tiếp có chủ đích

- Ưu tiên style được đặt tên hơn định dạng trực tiếp để tài liệu dễ chỉnh sửa.
- Style phân lớp: style đoạn văn, style ký tự, và định dạng trực tiếp không hoạt động giống nhau.
- Xóa định dạng trực tiếp thường an toàn hơn là chồng thêm định dạng nội tuyến.
- Khi chỉnh sửa file hiện có, mở rộng hệ thống style hiện tại thay vì tạo hệ thống song song mới.
- Sao chép nội dung giữa các tài liệu có thể âm thầm nhập các style, cài đặt theme, và định nghĩa đánh số lạ.

### 3. Danh sách và đánh số là hệ thống riêng

- Dấu đầu dòng và đánh số thuộc về định nghĩa đánh số của Word, không phải ký tự Unicode được dán vào.
- `abstractNum`, `num`, và thuộc tính đánh số đoạn văn đều quan trọng, vì vậy hành vi khởi động lại hiếm khi chỉ là "hình thức".
- Thụt lề và đánh số có liên quan nhưng không giống nhau; một danh sách có thể có đánh số bị hỏng dù thụt lề trông đúng.
- Một danh sách trông đúng trong một trình soạn thảo có thể tự khởi động lại, làm phẳng, hoặc đánh số lại sau nếu trạng thái đánh số cơ bản sai.

### 4. Bố cục trang nằm trong các phần

- Lề, hướng, tiêu đề, chân trang, và đánh số trang là hành vi cấp phần.
- Tiêu đề trang đầu và tiêu đề trang lẻ/chẵn có thể khác nhau trong cùng một tài liệu, nên sửa một tiêu đề có thể không sửa được toàn bộ.
- Đặt kích thước trang rõ ràng vì mặc định A4 và US Letter thay đổi phân trang và chiều rộng bảng.
- Sử dụng ngắt phần cho thay đổi bố cục; khoảng cách thủ công và ngắt trang lạc chỗ thường tạo ra độ lệch.
- Media tiêu đề và chân trang dùng quan hệ riêng cho từng phần, nên sao chép ID thường làm hỏng ảnh hoặc liên kết.
- Bảng, ngắt trang, và tiêu đề thường lệch cùng nhau, nên coi các sửa bố cục là toàn tài liệu, không phải chỉnh sửa cục bộ.
- Hình học bảng phụ thuộc vào chiều rộng trang, lề, và chiều rộng cố định, nên chỉnh sửa bảng "gần đúng" thường bị hỏng sau trong Google Docs hoặc LibreOffice.

### 5. Theo dõi thay đổi, bình luận, và trường cần chỉnh sửa chính xác

- Văn bản hiển thị không phải toàn bộ tài liệu khi theo dõi thay đổi được bật.
- Chèn, xóa, và bình luận mang metadata có thể tồn tại sau các chỉnh sửa bất cẩn.
- Văn bản đã xóa có thể vẫn tồn tại trong XML dù không còn xuất hiện trên màn hình.
- Điểm neo bình luận và phạm vi xem xét có thể bị hỏng nếu chỉnh sửa di chuyển văn bản mà không bảo toàn cấu trúc xung quanh.
- Đánh dấu bình luận và wrapper xem xét không hoạt động như định dạng nội tuyến, nên di chuyển văn bản bất cẩn có thể làm mồ côi hoặc đặt sai vị trí chúng.
- Bình luận, chú thích cuối trang, dấu trang, và media liên kết có thể nằm trong các phần riêng, không chỉ trong phần thân tài liệu chính.
- Mục lục, số trang, ngày tháng, tham chiếu chéo, và trình giữ chỗ mail merge là các trường.
- Chỉnh sửa nguồn trường cẩn thận và dự kiến giá trị hiển thị được cache sẽ trễ cho đến khi làm mới.
- Siêu liên kết, dấu trang, và tham chiếu có thể bị hỏng nếu ID hoặc quan hệ không còn khớp.
- Dấu trang, chú thích cuối trang, phạm vi bình luận, và tham chiếu chéo phụ thuộc vào điểm neo ổn định dù văn bản hiển thị có vẻ không bị ảnh hưởng.
- Tài liệu có thể trông đúng trong khi vẫn chứa đầu ra trường cũ sẽ làm mới thành thứ khác sau này.
- Với quy trình xem xét, thực hiện thay thế tối thiểu thay vì viết lại toàn bộ đoạn văn.
- Trong quy trình theo dõi thay đổi, chỉ khoảng thay đổi mới trông có vẻ thay đổi; viết lại rộng tạo ra xem xét ồn ào và có thể phá hủy ngữ cảnh định dạng gốc.
- Với tài liệu xem xét pháp lý, học thuật, hoặc kinh doanh, mặc định dùng chỉnh sửa kiểu xem xét hơn là viết lại đoạn văn toàn bộ trừ khi người dùng yêu cầu rõ ràng.

### 6. Xác minh tính tương thích vòng lặp trước khi giao

- Tài liệu phức tạp có thể thay đổi giữa Word, LibreOffice, Google Docs, và công cụ chuyển đổi.
- Bảng, tiêu đề, font nhúng, và style được sao chép là nguồn phổ biến gây độ lệch bố cục.
- Coi `.docm` là macro-bearing và rủi ro cao hơn; coi `.doc` là đầu vào cũ có thể cần chuyển đổi trước.
- Khi bố cục quan trọng, chiều rộng bảng rõ ràng an toàn hơn hành vi auto-fit hoặc kiểu phần trăm mà các trình soạn thảo khác diễn giải khác.
- Tài liệu vượt qua kiểm tra văn bản có thể vẫn thất bại về phân trang, chiều rộng bảng, hoặc làm mới tham chiếu sau khi người nhận mở.

## Bẫy Phổ Biến

- Sao chép-dán có thể nhập các style và định nghĩa đánh số không mong muốn.
- Ảnh tiêu đề hoặc chân trang dùng quan hệ riêng cho từng phần, nên tái sử dụng ID mù quáng sẽ làm hỏng chúng.
- Đoạn văn trống dùng làm khoảng cách làm cho mẫu dễ vỡ; khoảng cách thuộc về cài đặt đoạn văn.
- Xuất trông sạch vẫn có thể ẩn các sửa đổi chưa giải quyết, bình luận, hoặc giá trị trường cũ.
- Khởi động lại danh sách "bằng mắt" thường thất bại vì trạng thái đánh số nằm bên ngoài văn bản đoạn văn.
- Một cụm từ hiển thị có thể bị chia thành nhiều run, dấu trang, thẻ sửa đổi, hoặc ranh giới trường.
- Thay thế toàn bộ đoạn văn để thay đổi một mệnh đề thường phá hủy chất lượng xem xét, dấu trang, bình luận, hoặc định dạng nội tuyến lân cận.
- Xóa tất cả văn bản hiển thị khỏi một đoạn văn hoặc mục danh sách vẫn có thể để lại dấu đoạn văn trống, dấu đầu dòng trống, hoặc đánh số không ổn định.
- Hành vi chiều rộng bảng auto-fit và kiểu phần trăm có thể trông chấp nhận được trong Word nhưng vẫn lệch trong Google Docs hoặc LibreOffice.
- LibreOffice và Google Docs có thể dịch chuyển các bảng phức tạp, hành vi phần, và font nhúng dù Word trông hoàn hảo.
- Chế độ tương thích có thể âm thầm giới hạn các tính năng mới hơn hoặc thay đổi hành vi phân trang.
- Một thay đổi duy nhất trong kích thước trang hoặc mặc định lề có thể lan rộng qua bảng, tiêu đề, TOC, và tham chiếu chéo.
- Quy trình sửa đổi có thể trông được chấp nhận trên màn hình trong khi metadata còn sót lại, bình luận, hoặc cache trường vẫn làm file không ổn định sau này.
- Mục TOC, chú thích cuối trang, và tham chiếu chéo có thể trông đúng cho đến khi người nhận cập nhật các trường và lộ ra các điểm neo bị hỏng.
