# Báo cáo Bài 2: Quản lý nhánh và giải quyết xung đột (Merge Conflict)


## Các bước thực hiện
1. `git init`, tạo nhánh `main`, commit đầu tiên với `README.md` (dòng `Mo ta: ...`).
2. `git checkout -b feature-update`: tạo nhánh phụ, sửa dòng `Mo ta`, commit.
3. `git checkout main`: quay lại nhánh chính, sửa **cùng dòng** `Mo ta` theo nội dung khác, commit.
4. `git merge feature-update --no-ff`: Git báo `CONFLICT (content): Merge conflict in README.md`, quá trình gộp dừng lại.
5. `git status` cho thấy `README.md` ở trạng thái *both modified*.

## Giải quyết xung đột thủ công
1. Mở `README.md`, thấy các ký hiệu đánh dấu:
   - `<<<<<<< HEAD` … nội dung của nhánh `main`
   - `=======` ngăn cách hai phiên bản
   - `>>>>>>> feature-update` … nội dung của nhánh `feature-update`
2. Quyết định giữ cả hai ý: viết lại thành một dòng duy nhất “hỗ trợ đồng bộ nhiều thiết bị và có thêm tính năng nhắc việc”.
3. **Xóa toàn bộ** các dòng `<<<<<<<`, `=======`, `>>>>>>>`.
4. `git add README.md` để đánh dấu đã giải quyết.
5. `git commit` để tạo merge commit.

## Cơ chế 3-Way Merge
Git so sánh 3 vùng: *base* (tổ tiên chung – commit đầu), *ours* (main) và *theirs* (feature-update). Nếu chỉ một bên thay đổi một dòng thì Git tự gộp; khi cả hai bên cùng sửa một dòng khác nhau thì Git không biết chọn bên nào nên đánh dấu xung đột để người dùng quyết định.

## Kết quả
Lệnh `git log --graph --oneline` (xem `git_log.txt` và ảnh chụp đính kèm) cho thấy `feature-update` tách ra từ `main` rồi gộp lại bằng một merge commit có 2 commit cha.
