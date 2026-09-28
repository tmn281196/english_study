# Học tiếng Anh

Ba trang học tiếng Anh. Toàn bộ là file tĩnh (HTML, CSS, JS, JSON), không có backend, không có bước dựng;
đăng trên GitHub Pages: https://tmn281196.github.io/english_study/

| Trang | Nội dung |
|---|---|
| `en-svo` | Đồ thị khung câu tiếng Anh: mẫu động từ, nhóm theo ngữ nghĩa, bảng tra nhãn |
| `en-chunks` | ~1270 khối (cụm từ) tiếng Anh thông dụng, mỗi câu ví dụ tách thành khối |
| `en-matrix` | ~2900 câu luyện nói từ bộ Speaking Matrix, ngắt khối kèm nghĩa tiếng Việt |

## Cấu trúc

```
src/            cả site, đăng nguyên thư mục này
  index.html            trang mục lục
  en-svo/, en-chunks/   đồ thị câu, khối từ (en-chunks đọc chunks.json)
  en-matrix/            luyện nói Speaking Matrix: data.json (dựng từ epub), vi.json (nghĩa tiếng Việt)
tools/
  speaking-matrix.py    dựng src/en-matrix/data.json từ năm cuốn epub Speaking Matrix (Python 3)
```

## Xem thử

Trang đọc dữ liệu bằng `fetch`, nên phải mở qua http chứ không mở file trực tiếp:

```bash
python -m http.server -d src
```

rồi vào http://localhost:8000.

## Đăng lên GitHub Pages

Đẩy lên nhánh `main` là xong: `.github/workflows/pages.yml` đăng nguyên `src/`.

## Sửa nội dung

- Khối tiếng Anh: `src/en-chunks/chunks.json`.
- Speaking Matrix: epub không nằm trong repo. Dựng lại `data.json`:

  ```bash
  python tools/speaking-matrix.py <thư mục epub>
  ```

  Sách viết cho người Hàn, nhưng trang và `data.json` không giữ chữ Hàn nào. Nghĩa câu, nghĩa từng khối nằm ở
  `src/en-matrix/vi.json` (khóa là câu tiếng Anh), nên dựng lại `data.json` không mất bản dịch. Tên bài, tên mục,
  ghi chú từ vựng được thay bằng tiếng Việt lúc dựng, tra từ `vi-titles.json` đặt cạnh các file epub; chưa dịch
  thì để trống. Cần bản gốc tiếng Hàn để dịch phần mới thì thêm `--ko` (ghi `src/en-matrix/ko.json`, không đăng).
