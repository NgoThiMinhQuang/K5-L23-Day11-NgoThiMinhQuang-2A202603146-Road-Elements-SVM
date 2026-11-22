# Phiếu QC 1 — Road v1.0

**Lô được kiểm:** Bùi Kim Trại (`trai`)  
**Người kiểm:** Ngô Thị Minh Quang (`ngothiminhquang`)  
**Ngày kiểm:** 20/11/2026 · **Guideline:** Road v1.0  
**Revision của lô:** chưa có manifest.

## Nhận diện file được kiểm

| File | Số ảnh | Đủ 4 tag | Kèm ảnh | SHA-256 |
| --- | ---: | ---: | --- | --- |
| trai-front.zip | 12 | 12/12 | Không | `ed644a478a411668299f63e7be972f5487f0ebc61d631eef849a686c5fc11fad` |
| trai-front-extra.zip | 4 | 4/4 | Không | `a4ff77ae1a4308fdb1775768978718067bf8f3b15992e68e8025fb2d5ebf754f` |
| trai-fisheye.zip | 8 | 8/8 | Không | `0eef79e83fe2abb4cfa2101a193bd965df501cf6426d6553821fa82762a13276` |
| trai-fisheye-extra.zip | 4 | 4/4 | Không | `9e7e3cae8c150d3d4832304b84c2d1508a2f8fa76800bce0e9a2635efd2d97fb` |

Bốn ZIP CRC hợp lệ, mỗi ZIP chứa `annotations.xml`, không kèm ảnh. Đủ 28 ảnh không trùng, tên/kích thước khớp ảnh gốc. Tổng cộng 319 shape và 112 tag.

## Phạm vi và số nhãn kiểm

**Mẫu kiểm:** A02, A08, A10, B02, B06, B08 — 6 ảnh bắt buộc, 118 nhãn. Kiểm thêm B11 và thống kê riêng. Chưa đối chiếu GT.

| Ảnh | Shape | Tag | Tổng nhãn | Kết quả chính |
| --- | ---: | ---: | ---: | --- |
| A02 | 7 | 4 | 11 | Chưa phát hiện lỗi chắc chắn trong phạm vi kiểm; dùng làm ảnh đối chứng |
| A08 | 38 | 4 | 42 | F01: vạch ngang được gán lane |
| A10 | 17 | 4 | 21 | F02–F04: ba polygon khoét theo xe; F05: sai nhóm biển cấm |
| B02 | 10 | 4 | 14 | F06: polyline R1 đi ra rồi quay ngược theo hai mép |
| B06 | 16 | 4 | 20 | Còn câu hỏi về vạch cạnh đảo/ray và mép thân xe; chưa cộng lỗi chưa chắc chắn |
| B08 | 6 | 4 | 10 | Cần kiểm sát mép thân xe; chưa cộng lỗi chưa chắc chắn |
| **Tổng bắt buộc** | **94** | **24** | **118** | Dùng mẫu số 118 cho tỉ lệ lỗi chính |
| B11 — thêm | 7 | 4 | 11 | E01–E06: lane thuộc vạch ô đỗ/vùng gạch chéo; thống kê riêng |

## Tổng hợp theo mã

| Mã | Loại lỗi | Số mục kiểm | Số lỗi xác nhận | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 24 tag | 0 | nặng / nhẹ |
| QC1-02 đủ L1, R1 | bỏ sót | 8 vị trí trên A02/A08/A10/B02 | 0 | nặng |
| QC1-03 position / đối tượng lane | sai thuộc tính / thừa | 28 lane | 1 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 28 lane | 1 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 28 lane | 0 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 28 lane | 0 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 35: 29 polygon + 6 curb | 3 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 14 đèn | 0 | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 31: 14 đèn + 17 biển | 1 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 17 biển | 0 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 32 shape fisheye | 0 | chính |
| QC1-12 file | lỗi file | 118 nhãn mẫu + 4 ZIP | 0 | nhẹ / nặng |

## Danh sách lỗi

Định vị đối tượng bằng thứ tự shape trong XML (`#`, từ 0) và tọa độ điểm đầu.

| # | Mã | Ảnh | Nhãn, vị trí | Mức | Mô tả và cách sửa |
| --- | --- | --- | --- | --- | --- |
| F01 | QC1-03 | A08 | lane#32, đầu (364.3,367.6) | nặng | Polyline đến (2.8,361.0) bám vạch ngang bên trái giao lộ, được gán `lane`, position=other. Đây không phải vạch phân chia làn theo hướng chạy. Xóa nhãn lane thừa; không chỉ đổi position để hết cảnh báo |
| F02 | QC1-07 | A10 | drivable#14, direct | chính | Biên polygon đi vòng theo phần thân xe đen phía trước, qua vùng (540.55,392.60) → (547.03,457.10) → (763.26,456.25) → (768.81,407.24). Cách vẽ đang loại phần đường dưới xe. Sửa theo vùng đi được nếu đường trống, không khoét quanh xe khác |
| F03 | QC1-07 | A10 | drivable#16, alternative, đầu (1199.49,661.92) | chính | Biên lõm quanh xe bên phải, rõ ở (834.23,402.23)–(1015.32,390.67) và (1045.37,426.12)–(1142.47,499.33). Xác định vùng đường dưới xe, không bám đường bao thân xe |
| F04 | QC1-07 | A10 | drivable#0, alternative, đầu (70.53,650.23) | chính | Biên bám theo chân xe đỗ tím và xe xa bên trái, qua (401.40,351.22), (404.50,356.77), (475.75,351.95). Không khoét theo xe. Đồng thời rà phạm vi dải đỗ xe và làn alternative; chưa cộng riêng lỗi phạm vi khi chưa xác nhận |
| F05 | QC1-09 | A10 | traffic_sign#9, box (45.75,47.08)–(94.43,172.32) | chính | Cụm biển NO PARKING / NO STANDING đang mang group=information. Nội dung là cấm dừng/đỗ, cần group=prohibitory. Cần rà tách từng tấm biển vật lý; chưa cộng thêm lỗi gộp box |
| F06 | QC1-04 | B02 | lane#3, R1, kind=double | chính | Đường đi từ (998.43,433.57) xuống (1255.29,570.52), qua (1245.92,587.41) rồi quay về (963.56,429.90), bám hai mép và tạo vòng hẹp. Vẽ lại polyline hở trên tâm vạch, từ gần xe ra xa. `kind=double` không phải lý do vẽ đường bao đi-về |

### Định vị lỗi để đối chiếu

Các lỗi được định vị bằng mã ảnh, thứ tự shape trong XML và tọa độ tại bảng Danh sách lỗi. Các ảnh đối chiếu cũ đã được xóa theo yêu cầu học viên; số liệu và mô tả lỗi trong phiếu được giữ nguyên.

## Ảnh thêm — ghi riêng

**B11:** 7 shape + 4 tag = 11 nhãn. Sáu lane dưới đây thuộc ranh giới ô đỗ/vùng gạch chéo, không phải vạch phân làn chạy xe. Cần xóa các nhãn lane gán nhầm.

| # | Mã | Ảnh | Nhãn và điểm đầu | Mức | Yêu cầu |
| --- | --- | --- | --- | --- | --- |
| E01 | QC1-03 | B11 | lane#0@(1098.60,573.84) | nặng | Xóa lane gán nhầm vạch ô đỗ/gạch chéo |
| E02 | QC1-03 | B11 | lane#1@(992.04,583.48) | nặng | Như trên |
| E03 | QC1-03 | B11 | lane#3@(1164.26,549.21) | nặng | Như trên |
| E04 | QC1-03 | B11 | lane#4@(1109.85,570.63) | nặng | Như trên |
| E05 | QC1-03 | B11 | lane#5@(449.08,431.41) | nặng | Như trên |
| E06 | QC1-03 | B11 | lane#6@(347.34,397.14) | nặng | Như trên |

Sáu lỗi và 11 nhãn B11 được thống kê riêng, không tính vào tỉ lệ mẫu bắt buộc.

## Ca mơ hồ và cảnh báo lint

| Ảnh / nội dung | Câu hỏi / việc cần làm | Phản hồi lead |
| --- | --- | --- |
| A05 | Thiếu L1 và R1 theo lint; không thấy vạch rõ. Chờ xác nhận ngoại lệ. Ngoài mẫu kiểm sâu | Chưa có |
| A09 | Thiếu R1 theo lint; cần phân biệt vạch sơn với mép đường. Ngoài mẫu kiểm sâu | Chưa có |
| A14 — thêm | Lint báo thiếu R1 trên ảnh đêm. Cần kiểm bằng ảnh gốc và xác nhận ngoại lệ nếu không thấy vạch | Chưa có |
| A06 | Lint nghi đảo chiều ở đường gần ngang; cần phân biệt vạch dừng với lane. Chưa xác nhận lỗi. Ngoài mẫu kiểm sâu | Chưa có |
| A10 — weather | Tag `clear` nhưng đường ướt và có dấu nước trên kính; rà lại `rain` và xác nhận mức lỗi | Chưa có |
| A10 — các box biển nhỏ | Rà chức năng các biển group=other và việc tách từng tấm biển; chưa cộng lỗi ngoài F05 | Chưa có |
| B06/B08 — vùng lái | Rà mép thân xe, bóng và đảo phân luồng; chưa xác nhận lỗi phạm vi polygon | Chưa có |
| B06 — lane cạnh đảo/ray | Phân biệt vệt sơn với mép đảo hoặc ray; chưa xác nhận lỗi phân loại | Chưa có |
| Kế hoạch label từng slot | Cần bản kế hoạch cuối cùng để kiểm việc thiếu nhóm label | Chưa có |

**Lint toàn lô:** 28 ảnh, 5 cảnh báo: 4 nặng QC1-02 ở A05/A09/A14 và 1 chính QC1-04 ở A06. Các cảnh báo này chưa tính vào số lỗi xác nhận của mẫu QC.

## Quyết định

**Mẫu bắt buộc:** 1 lỗi nặng, 5 lỗi chính, 0 lỗi nhẹ đã xác nhận.  
**Tỉ lệ lỗi chính:** 5 / 118 × 100 = **4,24%**.  
**Quyết định của người kiểm Ngô Thị Minh Quang: REWORK — yêu cầu sửa và gửi lại.**

Tôi quyết định Rework vì F01 là lỗi nặng QC1-03: gán vạch ngang thành lane phân chia làn. Theo thang mức của lab, một lỗi nặng là đủ yêu cầu sửa lại. Tỉ lệ lỗi chính là 4,24%, không vượt 5%. Trại cần sửa F01–F06 và gửi lại để kiểm; xử lý E01–E06 nếu nộp B11.

Sau sửa: export lại các task liên quan, gửi manifest và phản hồi các ca mơ hồ. Kiểm lại F01, F02, F06 và ảnh đối chứng A02.

## Tài liệu và số liệu kiểm

- [Guideline Road v1.0](minh-chung/docs/guideline_road_v1.0.md).
- [Thang mức lỗi QC](minh-chung/docs/qc_severity_road_v1.0.md).
- [Mẫu phiếu của repo](minh-chung/templates/qc1_form.md).
- [Dữ liệu đếm nhãn, SHA-256 và cảnh báo](minh-chung/out/qc-trai/inspection.json).

**Người kiểm: Ngô Thị Minh Quang.**
