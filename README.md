# 語彙帳 — Web app học biểu đạt business tiếng Nhật

App tĩnh (HTML/JS thuần). Lưu tiến độ bằng `localStorage`. Cài được lên màn hình chính điện thoại (PWA), chạy offline.

## Files
- `index.html` — app (logic + giao diện)
- `data.js` — **KHO DỮ LIỆU**: sửa file này để thêm từ vựng dần
- `manifest.json`, `sw.js`, `icon-*.png` — cấu hình PWA (cài app + offline)

## Cách host (chọn 1)

### A. Cloudflare Pages / Netlify (miễn phí, public URL, ~2 phút)
1. Vào dash.cloudflare.com → Workers & Pages → Create → Pages → Upload assets (hoặc kéo-thả vào app.netlify.com/drop).
2. Kéo cả thư mục này vào → nhận URL `https://...pages.dev`.
3. Mở URL trên điện thoại → Safari/Chrome → "Thêm vào màn hình chính".

### B. Server nhà + Tailscale (riêng tư)
```bash
# đặt thư mục này lên server, rồi:
python3 -m http.server 8080      # hoặc cấu hình nginx trỏ vào thư mục
```
Mở `http://<tên-máy-tailscale>:8080` trên điện thoại (đã cài Tailscale).
> Lưu ý: PWA/Service Worker cần HTTPS hoặc localhost. Trên Tailscale, dùng Tailscale Serve (cấp HTTPS) để bật được offline & cài app.

## Thêm từ vựng dần — 2 cách

1. **Trên điện thoại (nhanh):** nút **＋ Thêm** → nhập thẻ → lưu vào máy ngay. Nút **⤓ Backup** xuất các thẻ tự thêm ra file `.json`.
2. **Vào nguồn (chuẩn):** mở `data.js`, thêm 1 dòng vào mảng `window.VOCAB_DATA`:
   ```js
   {c:"jargon", l:"中級", jp:"腹を割って話す", y:"はらをわってはなす", vi:"Nói thẳng thật lòng", ex:"一度、腹を割って話しましょう。"},
   ```
   `c` phải là 1 key có trong `window.VOCAB_CATS`. Muốn thêm nhóm mới thì thêm key vào `VOCAB_CATS`.
   Sau khi sửa `data.js`, **đổi `CACHE = "jpbiz-v1"` → `"jpbiz-v2"`** trong `sw.js` rồi redeploy để bản mới hiện ra.
