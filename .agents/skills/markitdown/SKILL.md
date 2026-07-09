---
name: markitdown
description: "Convert any document (PDF, Word, Excel, etc.) to a well-formatted Markdown file using markitdown, and then manually refine the markdown to visually match the original document's structure."
---

# markitdown Skill

## Khi nào nên sử dụng?
Sử dụng skill này khi người dùng yêu cầu chuyển đổi một tệp tài liệu (PDF, DOCX, XLSX, v.v.) sang Markdown và nhấn mạnh việc **giữ nguyên định dạng, bố cục giống nhất có thể** so với file gốc.

## Điều kiện tiên quyết
- Máy tính phải được cài đặt thư viện `markitdown`. Nếu lệnh lỗi, hãy tự động cài đặt bằng `pip install markitdown[all]`.

## Quy trình thực hiện (Workflow)

### 1. Chuyển đổi thô bằng MarkItDown
Sử dụng công cụ `run_command` để chạy lệnh:
```bash
markitdown "path/to/input.ext" -o "path/to/output.md"
```
*Lưu ý: Nếu file đang bị khóa (ví dụ: đang mở trong Excel/Word), hãy tạo một bản sao (copy) của file đó và chạy lệnh trên bản sao.*

### 2. Phân tích nội dung thô
Sử dụng `view_file` để đọc nội dung file `output.md` vừa được tạo ra. 
*Lưu ý: `markitdown` thiên về trích xuất text (raw text extraction), nên kết quả thường thiếu các thẻ Heading, danh sách bullet bị biến thành ký tự lạ (như ``, `◘`), và thiếu in đậm/in nghiêng.*

### 3. Tinh chỉnh và Làm đẹp (Beautify) - BẮT BUỘC
Dựa vào ngữ cảnh và nội dung đọc được, hãy sử dụng trí thông minh của bạn để viết lại (rewrite) toàn bộ nội dung Markdown sao cho sát với cấu trúc file gốc nhất:
- **Slide PPTX:** Gom thông tin lặp (footer/header) lên đầu, chuyển mỗi slide thành một Section (dùng `---`), thêm Heading `#` cho từng slide.
- **Excel / Bảng tính:** Xóa bỏ hoàn toàn các cột/hàng chứa `NaN`, `Unnamed: X`. Chuyển đổi các vùng dữ liệu dạng Form/Control Panel thành danh sách `Key: Value` gọn gàng. Chỉ giữ lại dạng Markdown Table cho những vùng thực sự là bảng dữ liệu (Data Table), và có thể ẩn bớt các hàng lịch sử quá dài nếu không cần thiết.
- **Heading:** Thêm các thẻ `#`, `##`, `###` cho các tiêu đề chính/phụ.
- **Lists:** Chuyển đổi các ký tự lạ thành danh sách gạch đầu dòng chuẩn (`-` hoặc `*`).
- **Typography:** **In đậm** các từ khóa, con số quan trọng, nhãn dán (labels).
- **Structure:** Dùng thước kẻ ngang (`---`) để phân chia các phần (sections) rõ ràng.

**⚠️ QUAN TRỌNG KHI XỬ LÝ HÀNG LOẠT (BATCH PROCESSING):**
Nếu người dùng yêu cầu xử lý một thư mục (nhiều file), bạn **PHẢI** duyệt qua từng file một để thực hiện bước Làm đẹp (Beautify) này. Tuyệt đối không được bỏ qua bước này và không được hỏi lại người dùng xem có muốn làm đẹp không. Hãy âm thầm làm đẹp tất cả các file rồi mới báo cáo kết quả tổng thể.

### 4. Ghi đè file hoàn chỉnh
Sử dụng công cụ `write_to_file` để ghi đè (overwrite) nội dung Markdown đã được bạn tinh chỉnh đẹp đẽ vào chính file `output.md` đó.

### 5. Báo cáo người dùng (Overview)
Sau khi hoàn tất (đặc biệt khi xử lý nhiều file), hãy tạo một Overview Artifact CHỈ CHỨA danh sách link các file Markdown đầu ra (dưới dạng gạch đầu dòng). Không thêm bất kỳ văn bản mô tả, giải thích, hay thông tin thừa nào khác để người dùng có một không gian làm việc gọn gàng.
