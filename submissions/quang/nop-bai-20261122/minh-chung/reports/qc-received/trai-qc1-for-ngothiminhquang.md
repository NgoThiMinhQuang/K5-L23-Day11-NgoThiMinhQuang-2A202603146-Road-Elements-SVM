# Phiếu QC 1 — Road v1.0

Lô được kiểm: **ngothiminhquang**  
Người kiểm: **BuiKimTrai**  
Ngày: **20/11/2026**  
Phiên bản guideline: **Road v1.0**  
Revision: không có manifest kèm các file nhận được.

## File và phạm vi kiểm

| File | Ảnh | Số ảnh |
| --- | --- | ---: |
| ngothiminhquang-front.zip | A01–A12 | 12 |
| ngothiminhquang-fisheye.zip | B01–B08 | 8 |
| ngothiminhquang-front-extra.zip | A13–A16 | 4 |
| ngothiminhquang-fisheye-extra.zip | B09–B12 | 4 |

Cả bốn file đều mở được, đủ 28 ảnh, mỗi ảnh có bốn tag và không kèm ảnh gốc. Đã chạy lint trên cả bốn file, sau đó đối chiếu nhãn với ảnh gốc để kiểm hình vẽ và thuộc tính.

Mẫu kiểm chi tiết gồm **A02, A08, A10, B02, B06, B08**. Kiểm thêm **B11** và ghi kết quả riêng.

| Ảnh | Shape | Tag | Tổng nhãn | Nhận xét |
| --- | ---: | ---: | ---: | --- |
| A02 | 7 | 4 | 11 | Chưa phát hiện lỗi trong phần đã kiểm. |
| A08 | 38 | 4 | 42 | Một nét sơn ngang tại giao lộ bị gán thành lane. |
| A10 | 17 | 4 | 21 | Ba polygon drivable khoét theo xe; một biển cấm bị gán sai group. |
| B02 | 10 | 4 | 14 | Polyline R1 đi ra rồi quay ngược theo mép còn lại. |
| B06 | 16 | 4 | 20 | Chưa kết luận thêm lỗi; có điểm cần lưu ý ở mép thân xe và cạnh đảo phân luồng. |
| B08 | 6 | 4 | 10 | Chưa kết luận thêm lỗi; cần lưu ý mép polygon sát thân xe. |
| **Tổng mẫu bắt buộc** | **94** | **24** | **118** | |
| B11 — ảnh thêm | 7 | 4 | 11 | Sáu đường thuộc ô đỗ/vùng gạch chéo bị gán thành lane. |

Số nhãn dùng tính tỉ lệ lỗi là **118**, gồm shape và tag của sáu ảnh bắt buộc. B11 được xét riêng, không cộng vào mẫu số này.

## Tổng hợp theo mã

| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 24 | 0 | nặng / nhẹ |
| QC1-02 đủ L1, R1 | bỏ sót | 8 | 0 | nặng |
| QC1-03 position | sai thuộc tính / thừa | 28 | 1 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 28 | 1 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 28 | 0 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 28 | 0 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 35 | 3 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 14 | 0 | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 31 | 1 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 17 | 0 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 32 | 0 | chính |
| QC1-12 file | lỗi file | 122 | 0 | nhẹ / nặng |

Một nhãn có thể được kiểm ở nhiều mã. Cột “Số mục kiểm” không dùng để cộng thành mẫu số tính tỉ lệ lỗi. Riêng QC1-12 gồm 118 nhãn và bốn file ZIP. Các điểm chưa đủ căn cứ được ghi ở mục Ca mơ hồ, không cộng vào bảng lỗi.

## Danh sách lỗi

| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả và cách sửa |
| --- | --- | --- | --- | --- | --- |
| F01 | QC1-03 | A08 | lane#32@(364,368) | nặng | Đường từ (364,368) đến (3,361) nằm trên nét sơn ngang tại giao lộ, không phải vạch phân làn dọc nhưng được gán lane, position=other. Cần bỏ nhãn lane này. |
| F02 | QC1-07 | A10 | drivable#3@(452,603), direct | chính | Biên polygon đi vòng theo thân xe đen phía trước, làm phần mặt đường dưới xe bị loại khỏi vùng direct. Cần sửa vùng lái theo mặt đường khi không có xe, không khoét theo thân xe. |
| F03 | QC1-07 | A10 | drivable#5@(1199,662), alternative | chính | Polygon bên phải lõm theo các xe ở khoảng (834,402)–(1015,391) và (1045,426)–(1142,499). Cần sửa lại biên vùng đường, không lấy thân xe làm ranh giới. |
| F04 | QC1-07 | A10 | drivable#6@(71,650), alternative | chính | Polygon bên trái khoét quanh xe màu tím và các xe phía xa, ở đoạn khoảng (404,357)–(511,320). Cần bỏ phần khoét theo xe và kiểm lại phạm vi làn alternative. |
| F05 | QC1-09 | A10 | traffic_sign#15@(46,47) | chính | Biển có nội dung NO PARKING / NO STANDING nhưng group=information. Theo Road v1.0, biển cấm dừng/đỗ thuộc group=prohibitory. Cần đổi lại group. |
| F06 | QC1-04 | B02 | lane#7@(998,434), R1 | chính | Polyline đi từ (998,434) tới phía gần (1255,571), rồi quay lại (964,430), tạo thành một vòng hẹp. Cần vẽ lại thành một đường tâm từ gần ra xa; vạch đôi cũng không vẽ vòng theo cả hai mép. |

Số sau dấu `#` là thứ tự shape trong XML, bắt đầu từ 0. Tọa độ đi kèm giúp tìm đối tượng nếu ID trên CVAT thay đổi sau khi nhập lại.

## Ảnh thêm: B11

| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả và cách sửa |
| --- | --- | --- | --- | --- | --- |
| E01 | QC1-03 | B11 | lane#0@(1099,574) | nặng | Đường thuộc ô đỗ hoặc vùng gạch chéo cạnh ô đỗ người khuyết tật, không phải vạch phân làn. Cần bỏ nhãn lane; đổi position thành other vẫn chưa đúng loại đối tượng. |
| E02 | QC1-03 | B11 | lane#1@(992,583) | nặng | Đường thuộc ô đỗ hoặc vùng gạch chéo cạnh ô đỗ người khuyết tật, không phải vạch phân làn. Cần bỏ nhãn lane; đổi position thành other vẫn chưa đúng loại đối tượng. |
| E03 | QC1-03 | B11 | lane#3@(1164,549) | nặng | Đường thuộc ô đỗ hoặc vùng gạch chéo cạnh ô đỗ người khuyết tật, không phải vạch phân làn. Cần bỏ nhãn lane; đổi position thành other vẫn chưa đúng loại đối tượng. |
| E04 | QC1-03 | B11 | lane#4@(1110,571) | nặng | Đường thuộc ô đỗ hoặc vùng gạch chéo cạnh ô đỗ người khuyết tật, không phải vạch phân làn. Cần bỏ nhãn lane; đổi position thành other vẫn chưa đúng loại đối tượng. |
| E05 | QC1-03 | B11 | lane#5@(449,431) | nặng | Đường thuộc ô đỗ hoặc vùng gạch chéo cạnh ô đỗ người khuyết tật, không phải vạch phân làn. Cần bỏ nhãn lane; đổi position thành other vẫn chưa đúng loại đối tượng. |
| E06 | QC1-03 | B11 | lane#6@(347,397) | nặng | Đường thuộc ô đỗ hoặc vùng gạch chéo cạnh ô đỗ người khuyết tật, không phải vạch phân làn. Cần bỏ nhãn lane; đổi position thành other vẫn chưa đúng loại đối tượng. |

B11 có **6 lỗi nặng**, ghi riêng cho phần ảnh thêm. Nếu nộp ảnh này để xét thưởng, cần sửa sáu nhãn trên rồi kiểm lại.

## Ca mơ hồ

| Ảnh | Nội dung cần làm rõ | Xử lý trong phiếu |
| --- | --- | --- |
| A05, A09, A14 | Lint báo thiếu L1/R1. Cần phân biệt trường hợp bỏ sót vạch với trường hợp ảnh không thấy vạch sơn. | Không tính thành lỗi chỉ từ cảnh báo lint và không yêu cầu vẽ vạch suy đoán. Các ảnh này không nằm trong mẫu sáu ảnh dùng tính tỉ lệ. |
| B06, B08 | Mép polygon nằm sát thân xe; khó phân biệt mặt đường, bóng và mép xe ở vòng ngoài. | Chưa đủ căn cứ để ghi thêm lỗi tràn thân xe. |
| B06 | Một số đường nằm gần cạnh đảo phân luồng/đường ray. | Chưa kết luận thêm lỗi phân loại khi chưa xác định rõ từng đường. |
| A10, traffic_sign#15 | Cần kiểm tra mép từng tấm biển trong box để quyết định có phải tách riêng không. | Chỉ ghi lỗi group ở F05, không cộng thêm lỗi gộp box. |

Các điểm trên đã được trao đổi với coach; coach đồng ý chốt phiếu theo kết quả hiện tại. Chưa tính thêm lỗi ngoài những lỗi đã ghi rõ trong danh sách.

## Quyết định

Lỗi nặng: **1**  
Lỗi chính: **5 / 118 nhãn = 4,24%**  
Lỗi nhẹ: **0**  
Ca chờ lead ảnh hưởng đến quyết định: **0**

**Quyết định: Rework.**

Lô còn lỗi nặng F01 nên cần trả lại để sửa. Tỉ lệ lỗi chính là 4,24%, chưa vượt 5%, nhưng vẫn không đủ điều kiện Release vì còn lỗi nặng.

Quang cần sửa F01–F06; nếu nộp B11 để xét thưởng thì sửa thêm E01–E06. Sau đó lưu nhãn, export lại và gửi bản mới để kiểm lại các lỗi đã ghi. Giữ bản cũ và cập nhật revision trong manifest khi nộp lại.

Ba lỗi có thể dùng để đối chiếu lại phiếu: F01 ở A08, F02 ở A10 và F06 ở B02. Ảnh A02 chưa phát hiện lỗi trong phần đã kiểm.

Người kiểm: **BuiKimTrai**  
Ngày chốt: **20/11/2026**
