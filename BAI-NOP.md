# Bài nộp — Ngô Thị Minh Quang

**Mã học viên:** 2A202603146 · **Ngày lab:** 20/11/2026 · **Guideline:** Road v1.0.

## Hồ sơ chấm bài

| Nội dung | File | Phạm vi |
| --- | --- | --- |
| Báo cáo cá nhân | [ngothiminhquang-report.md](submissions/quang/nop-bai-20261120/ngothiminhquang-report.md) | Kiểm project, thống kê, ca khó, phản hồi QC, minh chứng, tự đánh giá |
| Nhãn front | [ngothiminhquang-front.zip](submissions/quang/nop-bai-20261120/ngothiminhquang-front.zip) | A01–A12: 12 ảnh bắt buộc |
| Nhãn front-extra | [ngothiminhquang-front-extra.zip](submissions/quang/nop-bai-20261120/ngothiminhquang-front-extra.zip) | A13–A16: 4 ảnh thêm |
| Nhãn fisheye | [ngothiminhquang-fisheye.zip](submissions/quang/nop-bai-20261120/ngothiminhquang-fisheye.zip) | B01–B08: 8 ảnh bắt buộc |
| Nhãn fisheye-extra | [ngothiminhquang-fisheye-extra.zip](submissions/quang/nop-bai-20261120/ngothiminhquang-fisheye-extra.zip) | B09–B12: 4 ảnh thêm |
| Manifest | [ngothiminhquang-manifest.json](submissions/quang/nop-bai-20261120/ngothiminhquang-manifest.json) | Revision 2, SHA-256 và thống kê cả bốn ZIP |
| Phiếu Quang kiểm Trại | [ngothiminhquang-qc1-for-trai.md](submissions/quang/nop-bai-20261120/ngothiminhquang-qc1-for-trai.md) | 12 mã QC, mẫu 6 ảnh bắt buộc và B11 xét riêng |
| Phiếu Trại kiểm Quang | [trai-qc1-for-ngothiminhquang.md](submissions/quang/nop-bai-20261120/minh-chung/qc/trai-qc1-for-ngothiminhquang.md) | Phiếu nhận; phản hồi sửa ở mục 4 báo cáo |

## Cấu trúc thư mục

```text
submissions/quang/nop-bai-20261120/
├── ngothiminhquang-front.zip
├── ngothiminhquang-front-extra.zip
├── ngothiminhquang-fisheye.zip
├── ngothiminhquang-fisheye-extra.zip
├── ngothiminhquang-manifest.json
├── ngothiminhquang-report.md
├── ngothiminhquang-qc1-for-trai.md
└── minh-chung/
    ├── anh/          # Bốn ảnh: Labels, front A10, fisheye B02, XML
    ├── qc/           # Phiếu QC nhận từ Trại và số liệu kiểm lô Trại
    ├── xml/          # Trích đoạn XML của lane B02
    ├── kiem-tra/     # Lint, selftest, kết quả xác minh file
    └── nhat-ky/      # Nhật ký sửa và ngoại lệ
```

Các thư mục `docs`, `templates`, `lab`, `src`, `configs`, `manifests`, `tests` ở gốc repo giữ tài liệu và công cụ của đề bài. Ảnh gốc trong `data/` không được đưa lên Git. Mỗi ZIP nhãn chỉ chứa `annotations.xml`.

## Đối chiếu yêu cầu

| Hạng mục | Kết quả |
| --- | --- |
| 20 ảnh bắt buộc và 8 ảnh thêm | Đủ 28 ảnh, không trùng |
| Tag ảnh | Đủ 112 tag; camera đúng tên ảnh; A10 weather=rain |
| File nhãn | CVAT for images 1.1; ZIP/CRC/XML và checksum hợp lệ; 310 shape |
| Báo cáo | Đủ mục 1–7 và phần row-anchor tùy chọn |
| Ảnh minh chứng | Đủ bốn ảnh mới, liên kết trong báo cáo |
| QC hai chiều | Có phiếu Quang kiểm Trại, phiếu Trại kiểm Quang và phản hồi sửa |
| Công cụ | 31/31 test đạt, SELFTEST PASS trên dữ liệu tổng hợp |
| Cách đóng gói | Bốn ZIP riêng theo yêu cầu học viên; khác đặc tả gốc yêu cầu hai ZIP gộp và tổng năm file |
| Cảnh báo L1/R1 | Còn bốn cảnh báo ở A05/A09/A14; ngoại lệ theo học viên, chưa có xác nhận riêng của coach trong hồ sơ |
| Completed, export và QC lại trên CVAT | Ngoại lệ theo học viên; chưa xác minh lại |
| Bản r1 riêng | Không kèm bộ nộp sau khi dọn bản cũ theo yêu cầu; các thay đổi đã commit có trong lịch sử Git |

Đối chiếu với [yêu cầu nộp](SUBMISSION.md), [đặc tả bàn giao](docs/delivery_road_v1.0.md) và [rubric](RUBRIC.md). Các ngoại lệ được ghi tại mục 5 báo cáo; không đồng nghĩa với quyết định Release của người kiểm. Chất lượng hình học theo GT và điểm cuối cùng do giáo viên đánh giá.
