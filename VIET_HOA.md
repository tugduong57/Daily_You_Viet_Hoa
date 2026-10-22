# Kế hoạch Việt hoá Daily You

Mục tiêu: toàn bộ giao diện và thông báo hiển thị bằng tiếng Việt, thuật ngữ thống nhất, không gây lỗi hiển thị hay vận hành.

## Checklist

### 1. Rà soát tệp ngôn ngữ, giao diện và thông báo hệ thống
- [x] Tệp ngôn ngữ gốc `lib/l10n/intl_en.arb`: 297 chuỗi (cấu hình trong `l10n.yaml`).
- [x] Tệp tiếng Việt `lib/l10n/intl_vi.arb`: trước đây chỉ dịch 30/297 chuỗi, phần còn lại hiển thị tiếng Anh.
- [x] Chuỗi viết cứng trong mã Dart (`Text(...)`, `title:`, `label:`…): không còn chuỗi giao diện tiếng Anh; các chuỗi còn lại là log nội bộ (`_logger`), tên thương hiệu hoặc tên định dạng tệp.
- [x] Thông báo hệ thống: nội dung lấy từ bản dịch và lưu vào SharedPreferences khi mở app (`lib/pages/launch_page.dart`); các chuỗi dự phòng tiếng Anh nằm trong `lib/main.dart`, `lib/notification_manager.dart`, `lib/utils/backup_restore_utils.dart`.
- [x] Native: Android/iOS chỉ chứa tên ứng dụng "Daily You" (giữ nguyên thương hiệu).

### 2. Dịch và thay thế nội dung
- [x] Dịch đủ 297/297 chuỗi trong `intl_vi.arb`, giữ nguyên mọi placeholder (`{count}`, `{tag}`, `{percent}`…) và cú pháp số nhiều ICU (tiếng Việt chỉ dùng dạng `other`).
- [x] Chuỗi dự phòng của thông báo (“Ngày này năm xưa”, “Ghi nhật ký hôm nay!”, “Sao lưu thất bại”) chuyển sang tiếng Việt.
- [x] Tiếng Việt là ngôn ngữ mặc định cho lượt cài đặt mới (`Settings.overrideLanguage` trong `lib/config_provider.dart`); khi không xác định được ngôn ngữ, ứng dụng dùng tiếng Việt thay vì tiếng Anh (`lib/main.dart`). Người dùng vẫn có thể chọn “Theo hệ thống” hoặc ngôn ngữ khác trong Cài đặt → Ngôn ngữ.
- [x] Sinh lại mã bằng `flutter gen-l10n` (`lib/l10n/generated/app_localizations_vi.dart`).

### 3. Kiểm tra chức năng
- [x] `flutter analyze`: không có lỗi.
- [x] `flutter test`: 506/506 test đạt.
- [x] Kiểm tra định dạng runtime của các chuỗi có số nhiều/placeholder với locale `vi` (ví dụ: `5 tuần trước`, `Đang tạo bản sao lưu… 42%`, `Xóa "Gym"? Thẻ này đang được dùng trong 5 nhật ký.`).
- [ ] Kiểm tra thủ công trên thiết bị thật: độ dài chuỗi trên nút/thanh điều hướng, thông báo nhắc hằng ngày, thông báo sao lưu tự động.

## Bảng thuật ngữ

| Tiếng Anh | Tiếng Việt |
|---|---|
| Log | Nhật ký |
| Flashbacks | Hồi tưởng |
| On This Day | Ngày này năm xưa |
| Gallery | Thư viện |
| Tag / Label / Tracker | Thẻ / Nhãn / Theo dõi |
| Category | Danh mục |
| Mood | Tâm trạng |
| Template | Mẫu |
| Streak | Chuỗi |
| Backup / Restore | Sao lưu / Khôi phục |
| Sync / External location | Đồng bộ / Vị trí bên ngoài |
| Import / Export | Nhập / Xuất |
| Attachment | Tệp đính kèm |
| Accent color | Màu nhấn |
| Biometric unlock | Mở khóa bằng sinh trắc học |

Giữ nguyên: tên ứng dụng “Daily You”, AMOLED, Markdown, GPL-3.0 và tên định dạng của ứng dụng khác (Daylio, Diaro…).

## Lưu ý khi cập nhật từ upstream
Khi `intl_en.arb` thêm chuỗi mới, bổ sung bản dịch vào `intl_vi.arb` rồi chạy `flutter gen-l10n`. Chuỗi chưa dịch sẽ tự hiển thị bằng tiếng Anh.
