---
name: Word Beautifier / Làm đẹp tài liệu Word
slug: word-beautifier
version: 1.0.0
description: Tự động thiết kế lại và làm đẹp các tài liệu Microsoft Word (.docx) sang định dạng báo cáo hiện đại, chuyên nghiệp với font Segoe UI, màu nhận diện UWA Blue & Gold, bảng biểu tinh gọn, thẻ KPI chỉ số và Header/Footer tự động.
metadata: {"clawdbot":{"emoji":"🎨","os":["win32","linux","darwin"]}}
---

## Khi Nào Sử Dụng

Sử dụng kỹ năng này khi người dùng yêu cầu làm đẹp, thiết kế lại hoặc cải thiện thẩm mỹ cho tài liệu Microsoft Word (`.docx`), biến các định dạng mặc định hoặc thô sơ thành tài liệu có thiết kế hiện đại, cao cấp và chuẩn chỉnh.

## Quy Tắc Cốt Lõi (Core Rules)

### 1. Kích Thước Trang & Lề (Geometry)
- Luôn đặt kích thước khổ giấy là **A4** (8.27 x 11.69 inches).
- Thiết lập lề trang đều **1.0 inch** (2.54 cm) ở cả 4 phía (Top, Bottom, Left, Right).

### 2. Hệ Thống Màu Sắc & Typography
- **Hệ màu chủ đạo (UWA Theme)**:
  - **Màu chính (Primary Blue)**: `#003087` (Xanh dương đậm) cho tiêu đề lớn, tiêu đề bảng, liên kết.
  - **Màu điểm nhấn (Accent Gold)**: `#E1B924` (Vàng kim) cho thanh dọc trang trí lề trái của tiêu đề.
  - **Màu chữ chính (Charcoal)**: `#2B2B2B` (Xám đen) giúp văn bản trang nhã hơn màu đen thuần.
  - **Màu nền nhạt (Soft Shading)**: `#F4F7FB` (Xám-xanh rất nhẹ) làm nền hàng lẻ trong bảng và nền các thẻ chỉ số.
- **Typography (Segoe UI)**:
  - **Title (Tiêu đề tài liệu)**: 24pt, In đậm, Xanh UWA, kèm thanh viền trái dày 4.5pt (36 dxa, space 10).
  - **Heading 1**: 18pt, In đậm, Xanh UWA, kèm thanh viền trái màu vàng dày 4.0pt (32 dxa, space 10). Giãn trước 18pt, sau 6pt, `keep_with_next = True`.
  - **Heading 2**: 13pt, In đậm, Xanh UWA. Giãn trước 14pt, sau 4pt.
  - **Heading 3**: 11.5pt, In đậm, Xám tối `#2B2B2B`. Giãn trước 10pt, sau 2pt.
  - **Body (Văn bản thường)**: 11pt, Regular, Xám tối, giãn dòng 1.15, giãn sau đoạn 6pt.

### 3. Tái Thiết Kế Bảng Biểu (Tables)
- **Header hàng đầu**: Nền xanh UWA `#003087`, chữ màu trắng in đậm 10pt. Thiết lập `cantSplit` và `tblHeader` để tự động lặp lại khi sang trang.
- **Hàng dữ liệu**:
  - Đổ màu xen kẽ: Hàng lẻ màu nhạt `#F4F7FB`, hàng chẵn màu trắng `#FFFFFF`.
  - Font chữ trong bảng: 9.5pt Segoe UI, màu `#2B2B2B`.
- **Đường viền**: Xóa toàn bộ viền dọc. Chỉ dùng viền ngang mảnh màu xám `#E0E0E0` để phân tách hàng.
- **Căn đệm (Padding)**: Thiết lập margins cho ô: Top/Bottom = 110 dxa (~5.5pt), Left/Right = 150 dxa (~7.5pt).
- **Căn lề cột**: Căn phải cột số liệu/tiền tệ, căn trái cột văn bản thường.

### 4. Dàn Hàng Thẻ Thống Kê & Icons (Dashboard Cards)
- **Metric Cards**: Gom nhóm các danh sách chỉ số đứng dọc thành **1 hàng nhiều cột** (sử dụng bảng ẩn viền dọc). Mỗi ô có nền màu nhạt `#F4F7FB`, viền trái màu vàng `#E1B924` dày 3pt, chữ số chính cỡ 22pt đậm xanh UWA, mô tả phía dưới cỡ 9pt xám.
- **Icon Cards**: Gom nhóm các icon emoji đứng dọc thành **1 hàng nhiều cột**. Mỗi ô có viền xám mỏng `#E0E0E0` bao quanh, nền màu nhạt `#F4F7FB`. Emoji căn giữa cỡ 20pt, nhãn căn giữa cỡ 9.5pt in đậm bên dưới.

### 5. Mục Lục Tương Tác & Chân Trang Động
- **Mục lục**: Tạo danh sách mục lục thủ công. Đính kèm Bookmark nội bộ tại các Heading 1, thiết lập liên kết mục lục trỏ đến bookmark này bằng thuộc tính XML `w:anchor` giúp click nhảy trang trực tiếp.
- **Header**: Hiển thị tên tài liệu in nghiêng 8.5pt màu xám lề phải, có đường kẻ dưới xanh dương mảnh.
- **Footer**: Chèn dynamic XML field `PAGE` và `NUMPAGES` tạo định dạng số trang dạng `Trang X / Y` tự động.

---

## Các Đoạn Mã XML Mẫu (Helper Code Snippets)

Dưới đây là các hàm Python tương thích với `python-docx` để thao tác trực tiếp với XML (OOXML) giúp tránh lỗi namespace:

### 1. Đổ màu nền ô bảng (Cell Background)
```python
def set_cell_background(cell, hex_color):
    shd_elms = [child for child in cell._tc.get_or_add_tcPr() if child.tag.endswith('shd')]
    for shd in shd_elms:
        cell._tc.tcPr.remove(shd)
    shading = OxmlElement('w:shd')
    shading.set(qn('w:val'), 'clear')
    shading.set(qn('w:color'), 'auto')
    shading.set(qn('w:fill'), hex_color)
    cell._tc.get_or_add_tcPr().append(shading)
```

### 2. Thiết lập khoảng đệm ô bảng (Cell Padding)
```python
def set_cell_margins(cell, top=100, bottom=100, left=150, right=150):
    tcPr = cell._tc.get_or_add_tcPr()
    tcMar_elms = [child for child in tcPr if child.tag.endswith('tcMar')]
    for tm in tcMar_elms:
        tcPr.remove(tm)
    tcMar = OxmlElement('w:tcMar')
    for margin, val in [('top', top), ('bottom', bottom), ('left', left), ('right', right)]:
        node = OxmlElement(f'w:{margin}')
        node.set(qn('w:w'), str(val))
        node.set(qn('w:type'), 'dxa')
        tcMar.append(node)
    tcPr.append(tcMar)
```

### 3. Tạo viền trái cho đoạn văn (Paragraph Left Border)
```python
def set_paragraph_left_border(paragraph, color_hex="E1B924", size=36, space=8):
    pPr = paragraph._element.get_or_add_pPr()
    pBdr_elms = [child for child in pPr if child.tag.endswith('pBdr')]
    if pBdr_elms:
        pBdr = pBdr_elms[0]
    else:
        pBdr = OxmlElement('w:pBdr')
        pPr.append(pBdr)
    
    left_elms = [child for child in pBdr if child.tag.endswith('left')]
    for left in left_elms:
        pBdr.remove(left)
        
    left = OxmlElement('w:left')
    left.set(qn('w:val'), 'single')
    left.set(qn('w:sz'), str(size))
    left.set(qn('w:space'), str(space))
    left.set(qn('w:color'), color_hex)
    pBdr.append(left)
```

### 4. Đánh số trang tự động ở Footer (Trang X / Y)
```python
def add_page_number_fields(paragraph):
    paragraph.alignment = docx.enum.text.WD_ALIGN_PARAGRAPH.CENTER
    p = paragraph._element
    rPr = OxmlElement('w:rPr')
    rFonts = OxmlElement('w:rFonts')
    rFonts.set(qn('w:ascii'), 'Segoe UI')
    rFonts.set(qn('w:hAnsi'), 'Segoe UI')
    rPr.append(rFonts)
    sz = OxmlElement('w:sz')
    sz.set(qn('w:val'), '18') # 9pt
    rPr.append(sz)
    
    # Text "Trang "
    r_trang = OxmlElement('w:r')
    r_trang.append(rPr)
    t1 = OxmlElement('w:t')
    t1.text = "Trang "
    t1.set(qn('xml:space'), 'preserve')
    r_trang.append(t1)
    p.append(r_trang)
    
    # PAGE Field
    fldSimple1 = OxmlElement('w:fldSimple')
    fldSimple1.set(qn('w:instr'), 'PAGE')
    p.append(fldSimple1)
    
    # Slash " / "
    r_slash = OxmlElement('w:r')
    r_slash.append(rPr)
    t2 = OxmlElement('w:t')
    t2.text = " / "
    t2.set(qn('xml:space'), 'preserve')
    r_slash.append(t2)
    p.append(r_slash)
    
    # NUMPAGES Field
    fldSimple2 = OxmlElement('w:fldSimple')
    fldSimple2.set(qn('w:instr'), 'NUMPAGES')
    p.append(fldSimple2)
```

---

## Hướng Dẫn Từng Bước Cho Agent (Step-by-Step)

1. **Phân tích Tài liệu Gốc**:
   - Sử dụng kịch bản quét văn bản để đọc hết các đoạn văn và bảng biểu gốc.
   - Nhận diện các liên kết ngoài, các danh sách có cấu trúc đặc biệt (số liệu dọc, emoji dọc) để chuẩn bị các phương án gộp.
2. **Khởi tạo Tài liệu Đích**:
   - Tạo tài liệu Word mới sử dụng khổ giấy A4, lề trang 1.0 inch.
   - Thiết lập Header và Footer chứa số trang động.
3. **Dựng Khung Tiêu Đề & Mục lục**:
   - Thiết kế Tiêu đề tài liệu và Mục lục thủ công dạng gạch đầu dòng, liên kết đến bookmark của các Heading 1 bằng thuộc tính `w:anchor`.
4. **Quét và Tái Tạo Nội dung**:
   - Quét qua từng phần tử của tài liệu gốc.
   - Nếu gặp Heading 1, gán bookmark và vẽ viền vàng lề trái.
   - Nếu gặp danh sách thống kê dọc, gom gộp thành hàng thẻ chỉ số Metric Cards.
   - Nếu gặp biểu tượng emoji và nhãn ngành đứng dọc, gom gộp thành hàng thẻ Icon Cards.
   - Nếu gặp bảng biểu, sao chép nội dung và áp dụng hàm `style_table` (thiết lập chiều rộng, màu nền header xanh UWA, đổ màu xen kẽ, căn chỉnh cột số, loại bỏ viền dọc).
   - Nếu gặp văn bản thường hoặc danh sách, sao chép các runs và bảo toàn các liên kết ngoài.
5. **Lưu và Kiểm Tra**:
   - Lưu tài liệu mới và kiểm tra cấu trúc XML để chắc chắn không lỗi thẻ hoặc thiếu dữ liệu.
