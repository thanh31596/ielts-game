# IELTS Flashcards

Game học 10.000 từ vựng IELTS: 100 cụm × 100 từ.

- **Flashcards**: vuốt phải = đã thuộc, vuốt trái = chưa thuộc, chạm 2 lần = lật thẻ (máy tính: ← → Space).
- **Đấu với thời gian**: đọc nghĩa, gõ đúng từ trong 15 giây.
- **Đấu với người (cùng máy)**: bấm chuông (phím A / L), ai trả lời đúng trước được điểm.
- **Đấu online (2 máy)**: tạo phòng, gửi mã/link, ai gõ đúng trước được điểm.

Không có backend, không lưu dữ liệu. Toàn bộ là file tĩnh.

## Deploy lên GitHub Pages

1. Tạo repo mới (ví dụ `ielts-game`), đưa 4 file `index.html`, `peerjs.min.js`, `.nojekyll`, `README.md` vào nhánh `main`.
2. Settings → Pages → Source: *Deploy from a branch* → Branch `main`, thư mục `/ (root)` → Save.
3. Sau 1–2 phút, game chạy tại `https://<username>.github.io/ielts-game/`.

## Kỹ thuật chế độ online

- Kết nối trực tiếp giữa 2 trình duyệt bằng WebRTC qua thư viện [PeerJS](https://peerjs.com) (MIT, bản 1.5.5 đi kèm trong repo).
- Máy tạo phòng là trọng tài: giữ câu hỏi, chấm đáp án, xác định ai đúng trước, rồi gửi trạng thái cho máy kia.
- Việc bắt tay ban đầu dùng máy chủ signaling công cộng miễn phí của PeerJS (`0.peerjs.com`). Máy chủ này không cam kết uptime.
- Một số mạng chặn kết nối trực tiếp (4G có NAT chặt, wifi công ty/trường). Khi đó cần TURN server:
  1. Đăng ký miễn phí tại https://www.metered.ca/tools/openrelay/ (20 GB/tháng).
  2. Tạo app, lấy link *TURN credentials* dạng `https://<ten-app>.metered.live/api/v1/turn/credentials?apiKey=<API_KEY>`.
  3. Mở `index.html`, tìm dòng `const TURN_CREDENTIALS_URL="";` và dán link vào giữa hai dấu ngoặc kép, rồi commit.

## Nguồn dữ liệu

- Nghĩa tiếng Việt: từ điển Anh–Việt trong [catusf/tudien](https://github.com/catusf/tudien) (CC0).
- IPA: [open-dict-data/ipa-dict](https://github.com/open-dict-data/ipa-dict) (MIT).
- Nghĩa tiếng Anh: WordNet 3.0 (Princeton WordNet License).
- Danh sách từ theo tần suất: [wordfreq](https://github.com/rspeer/wordfreq).
