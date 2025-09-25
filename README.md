# License Plate Recognition (YOLOv11 + OCR)

Nhận dạng biển số xe từ video bằng YOLOv11 + OCR.  
Repo đã có sẵn video kết quả: **`vehicle_video_output.mp4`**.

## 🎬 Demo ngay trong README

> Trình hiển thị của GitHub hỗ trợ thẻ HTML5 video. Nếu trình duyệt/ứng dụng không hỗ trợ, hãy dùng link bên dưới.

<video src="vehicle_video_output.mp4" controls width="720">
  Trình duyệt của bạn không hỗ trợ thẻ video. Xem trực tiếp file tại:
  <a href="vehicle_video_output.mp4">vehicle_video_output.mp4</a>.
</video>

> ✅ Nếu bạn xem README trên GitHub web, nút **Play ▶️** sẽ xuất hiện.  
> 🔗 Link trực tiếp: [vehicle_video_output.mp4](vehicle_video_output.mp4)

---

## 📦 Clone & tải file lớn (LFS)

Repo dùng **Git LFS** cho tệp `.mp4`/`.pt`. Để chắc chắn tải đầy đủ video:

```bash
git lfs install
git clone https://github.com/WhiteKnight0003/LicensePlateRecognition.git
cd LicensePlateRecognition
git lfs pull
```

Nếu không thấy file `.mp4` sau khi clone, hãy chạy lại `git lfs pull`.

---

## ▶️ Chỉ mở video kết quả (không cần chạy model)

Chọn **một** trong các cách sau:

### Cách 1: Mở bằng trình phát có sẵn
```bash
# Chạy một trong các lệnh (tùy máy đã cài gì):
ffplay -autoexit vehicle_video_output.mp4     # nếu đã cài ffmpeg
mpv vehicle_video_output.mp4                  # nếu có mpv
vlc vehicle_video_output.mp4                  # nếu có VLC
```

### Cách 2: Mở bằng Python + OpenCV
```bash
python -m venv .venv
source .venv/bin/activate      # Windows: .venv\Scripts\activate
pip install opencv-python

python - << 'PY'
import cv2
cap = cv2.VideoCapture('vehicle_video_output.mp4')
if not cap.isOpened():
    raise SystemExit("Không mở được vehicle_video_output.mp4. Hãy kiểm tra git lfs pull hoặc đường dẫn.")
while True:
    ok, frame = cap.read()
    if not ok: break
    cv2.imshow('vehicle_video_output', frame)
    if cv2.waitKey(1) & 0xFF == 27: break  # ESC để thoát
cap.release(); cv2.destroyAllWindows()
PY
```

---

## ⚙️ (Tuỳ chọn) Chạy lại pipeline để tạo video

Nếu bạn muốn tái tạo đầu ra từ video đầu vào (không bắt buộc để xem demo):

```bash
python -m venv .venv
source .venv/bin/activate                      # Windows: .venv\Scripts\activate
pip install --upgrade pip
pip install ultralytics==8.* easyocr opencv-python numpy
# Với GPU: cài torch/torchvision phù hợp CUDA theo hướng dẫn PyTorch

python main.py
# Script mặc định đọc vehicle_video.mp4 và ghi vehicle_video_output.mp4 (giữ nguyên tên file/thư mục).
```

---

## 🔧 Khắc phục nhanh

- **Video không phát / không tải về** → chạy `git lfs pull`.  
- **OpenCV không mở video** → cài `ffmpeg` (Ubuntu: `sudo apt install ffmpeg`).  
- **Thiết bị GPU không nhận** → chạy bằng CPU trước (hoặc cài đúng bản `torch` theo CUDA).

---

## 📂 Cấu trúc tối thiểu

```
LicensePlateRecognition/
├─ README.md
├─ main.py            # (tuỳ chọn chạy lại pipeline)
├─ easyOCR.py         # (tuỳ chọn)
├─ vehicle_video.mp4  # (đầu vào mẫu - tuỳ chọn)
└─ vehicle_video_output.mp4  # ✅ video kết quả để xem
```

---

**Góp ý/issue**: nếu video không hiển thị trong README, hãy mở trực tiếp link file hoặc tải về máy bằng LFS như hướng dẫn ở trên.
