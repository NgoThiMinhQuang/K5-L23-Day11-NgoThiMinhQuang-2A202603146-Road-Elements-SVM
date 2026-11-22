# Ngoại lệ — Bài lab ngày 20/11/2026

## Ảnh không thấy vạch

| Ảnh | Vị trí | Xử lý |
| --- | --- | --- |
| A05 | L1 và R1 | Không thấy vạch sơn rõ; không vẽ suy đoán |
| A09 | R1 | Không thấy vạch tương ứng rõ; giữ road_curb, không thêm lane |
| A14 | R1 | Không thấy vạch tương ứng rõ trên ảnh đêm; không thêm lane |

Ghi nhận ngoại lệ theo ảnh, không chờ coach xác nhận theo phạm vi bài nộp đã thống nhất. Giữ nguyên bốn cảnh báo QC1-02 trong log lint và manifest để phản ánh đúng dữ liệu.

## Chốt CVAT và kiểm lại sau sửa

Bước chốt nhãn trên CVAT và kiểm lại sau sửa được học viên xác nhận là ngoại lệ. Không điền trạng thái completed hoặc số shape trên job khi chưa xác minh.
