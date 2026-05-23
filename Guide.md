# Hướng dẫn dọn dẹp (Clean Up Guide) cho OmniVoice Studio

Khi dự án này khởi chạy lần đầu, nó tải về một lượng lớn dữ liệu (khoảng vài GB) để thiết lập môi trường AI hoàn toàn chạy cục bộ trên máy của bạn. Nếu sau này bạn muốn xóa dự án và dọn sạch "rác" khỏi ổ cứng, hãy làm theo các bước sau để thu hồi dung lượng:

## 1. Dọn dẹp cục bộ (Bên trong thư mục dự án)
Nếu bạn chỉ xóa thư mục `D:\OmniVoice`, bạn sẽ dọn được:
- **`node_modules/`**: Chứa các thư viện Node.js do `bun install` tải về (~200MB).
- **`.venv/`**: Môi trường Python ảo do `uv` tạo ra, chứa toàn bộ thư viện Python hạng nặng như PyTorch, torchaudio, transformers, v.v. (~4-5GB).

*Lệnh dọn nhanh:* Bạn chỉ cần Shift + Delete toàn bộ thư mục `D:\OmniVoice`.

## 2. Dọn dẹp Global Cache (Bên ngoài thư mục dự án)
Ngay cả khi bạn xóa thư mục dự án, một số công cụ AI vẫn lưu cache ở các thư mục hệ thống của người dùng để dùng chung cho các dự án khác. Nếu muốn dọn sạch 100%, hãy xóa các thư mục sau:

### A. Hugging Face Models Cache
Đa số các mô hình AI (như WhisperX, mô hình tách giọng, mô hình ngôn ngữ) được tải qua Hugging Face Hub sẽ lưu cache tại đây.
- **Đường dẫn:** `C:\Users\<Tên_User_Của_Bạn>\.cache\huggingface\hub`
- **Cách xóa:** Xóa toàn bộ thư mục `hub` bên trong `huggingface`. (Sẽ giải phóng vài GB).

### B. PyTorch / Torch Hub Cache
Một số file trọng số (weights) của PyTorch có thể được lưu ở đây.
- **Đường dẫn:** `C:\Users\<Tên_User_Của_Bạn>\.cache\torch`

### C. Bộ đệm (Cache) của trình quản lý gói `uv`
Công cụ `uv` mà mình vừa cài đặt cho bạn lưu trữ các bản phân phối Python (như CPython 3.11.15) và cache các gói pip.
- **Đường dẫn:** `C:\Users\<Tên_User_Của_Bạn>\AppData\Local\uv\cache` (hoặc `AppData\Roaming\uv`)
- **Cách xóa an toàn:** Mở PowerShell và gõ lệnh:
  ```powershell
  uv cache clean
  ```

## Tổng kết
Khi muốn gỡ bỏ hoàn toàn:
1. Xóa thư mục `D:\OmniVoice`.
2. Xóa `~/.cache/huggingface`.
3. Xóa `~/.cache/torch`.
4. Chạy `uv cache clean` (nếu bạn không dùng `uv` cho việc nào khác nữa thì có thể gỡ cài đặt `uv` bằng `pip uninstall uv`).
