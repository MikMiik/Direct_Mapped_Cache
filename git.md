# Direct-Mapped Cache Controller

## 1. Phân công và Chức năng từng file

| File | Thành viên phụ trách | Chức năng |
| ----- | ----- | ----- |
| `src/top.v` | **Thành viên 1** (Trưởng nhóm) | Module đỉnh: kết nối CPU interface, Cache Controller, Cache Memory và Main Memory. |
| `src/cache_memory.v` | **Thành viên 2** | Lưu Data Array, Tag Array, Valid Bit; xử lý đọc/ghi Cache theo Index. |
| `src/cache_controller.v` | **Thành viên 3** | Cài đặt FSM điều khiển: nhận diện Hit/Miss, điều phối đọc/ghi giữa Cache và Memory. |
| `src/main_memory.v` | **Thành viên 4** | Mô hình bộ nhớ chính (256x8 bit), phục vụ nạp khi Miss và ghi dữ liệu. |
| `tb/cache_tb.v` | **Thành viên 4** | Testbench tạo xung clock, stimulus CPU và so khớp kết quả đọc/ghi. |
| `simulation/*.png` | **Thành viên 5** | Lưu ảnh waveform các test case: Hit, Miss, Conflict Miss. |
| `docs/` & `presentation/` | **Thành viên 5** | Lưu tài liệu kiến trúc, sơ đồ FSM, file báo cáo (.pdf) và slide thuyết trình. |

## 2. Quy tắc đặt tên Commit (Bắt buộc dùng Tiếng Anh)

Cú pháp chuẩn: `<type>: <short description>`

* `feat:` Thêm chức năng hoặc logic mới (VD: `feat: implement hit detection logic`)
* `fix:` Sửa lỗi logic hoặc lỗi compile (VD: `fix: correct FSM state transition`)
* `test:` Thêm hoặc sửa testbench (VD: `test: add conflict miss test case`)
* `docs:` Cập nhật tài liệu, slide, ảnh waveform (VD: `docs: add read miss waveform`)
* `refactor:` Tối ưu, dọn dẹp code mà không đổi chức năng (VD: `refactor: clean up cache signals`)

## 3. Hướng dẫn thao tác Git cho từng thành viên

### Bước 1: Khởi tạo nhánh `develop` (Chỉ Trưởng nhóm làm 1 lần duy nhất)

Trưởng nhóm tạo nhánh `develop` từ `main` rồi đẩy lên GitHub:

```bash
git checkout -b develop
git push -u origin develop
```

### Bước 2: Lấy dự án về máy (Dành cho cả nhóm)

Mở terminal/git bash tại thư mục muốn lưu:

```bash
git clone <URL_REPOSITORY>
cd Direct_Mapped_Cache

# Chuyển sang nhánh develop để làm mốc làm việc
git checkout develop
```

### Bước 3: Tạo nhánh riêng theo nhiệm vụ (Từ nhánh `develop`)

Mỗi người tự tạo và chuyển sang nhánh riêng của mình:

* **Thành viên 1:** `git checkout -b feature/top-module`
* **Thành viên 2:** `git checkout -b feature/cache-memory`
* **Thành viên 3:** `git checkout -b feature/controller`
* **Thành viên 4:** `git checkout -b feature/memory-tb`
* **Thành viên 5:** `git checkout -b feature/docs-verification`

### Bước 4: Kiểm tra và lưu thay đổi khi làm việc

Sau khi sửa hoặc thêm code vào file của mình (áp dụng quy tắc commit ở mục 2):

```bash
# Xem các file đã thay đổi
git status

# Thêm file cần lưu (ví dụ cache_memory.v hoặc dùng "git add ." cho tất cả)
git add src/cache_memory.v

# Lưu thay đổi bằng tiếng Anh đúng cú pháp
git commit -m "feat: add tag comparison logic"
```

### Bước 5: Đẩy nhánh lên GitHub

Chỉ đẩy nhánh cá nhân, không đẩy trực tiếp vào `main` hay `develop`:

```bash
# Đổi tên nhánh tương ứng với nhánh bạn đã tạo ở Bước 3
git push -u origin <ten-nhanh-cua-ban>
```

*(Từ lần thứ hai trở đi trên cùng nhánh đó chỉ cần gõ: `git push`)*

### Bước 6: Cập nhật code mới nhất từ nhóm về máy mình

Trước khi tiếp tục code hoặc chuẩn bị nộp bài:

```bash
# 1. Chuyển sang develop và kéo code mới nhất từ GitHub về
git checkout develop
git pull origin develop

# 2. Quay lại nhánh của mình và gộp code mới vào
git checkout <ten-nhanh-cua-ban>
git merge develop
```

### Bước 7: Ghép code vào dự án chung (Pull Request)

1. Truy cập vào trang GitHub của nhóm.
2. Bấm vào nút **Compare & pull request** xuất hiện ở đầu trang.
3. Chọn nhánh nguồn (**compare**) là `<ten-nhanh-cua-ban>` và nhánh đích (**base**) là `develop`.
4. Bấm **Create pull request** để Trưởng nhóm (Thành viên 1) kiểm tra và merge.