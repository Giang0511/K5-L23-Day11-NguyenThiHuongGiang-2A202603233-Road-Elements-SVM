# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): Nguyễn Tấn Dũng        Người kiểm (học viên): Nguyễn Thị Hương Giang (2A202603233)  
Ngày: 21/11/2026                          Phiên bản guideline: Road v1.0  
File được kiểm (tên + `revision` trong manifest): `nguyentandung-front.zip` (CVAT for images 1.1, 16 ảnh A01–A16 trong một job), revision: [CẦN ĐIỀN — chưa nhận manifest của bạn Dũng]  
Số ảnh kiểm: 6 (+ 0 ảnh thêm, ghi riêng)   Số nhãn đã kiểm (shape + tag): 74  
Ảnh được kiểm: A01, A03, A04, A07, A09, A12. Chưa nhận file `nguyentandung-fisheye.zip` nên không kiểm QC1-11 và phần fisheye của QC1-12.  
Cách kiểm: không có GT, tôi đối chiếu nhãn với ảnh gốc (vẽ chồng nhãn lên ảnh, phóng to chỗ nghi ngờ) và chạy `road_check lint`. Độ lệch 5 px không đo được bằng mắt nên QC1-04 chỉ kiểm chiều vẽ và điểm dừng.

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 24 | 3 | nặng (tag camera đúng ở 6/6 ảnh; 3 lỗi là thiếu tag khác, mức nhẹ) |
| QC1-02 đủ L1, R1 | bỏ sót | 12 | 0 | nặng (A07 thiếu L1, A09 thiếu R1: chờ lead, xem Ca mơ hồ) |
| QC1-03 position | sai thuộc tính / thừa | 21 | 2 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 21 | 0 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 21 | 4 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 21 | 0 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 20 | 1 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 4 | 1 | nặng |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 12 | 0 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 8 | 2 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 0 | 0 | chính (không kiểm: chưa có file fisheye) |
| QC1-12 file | lỗi file | 1 | 0 | nhẹ / nặng (zip front mở lại được; chưa nhận zip fisheye) |

Cách đếm số mục kiểm: QC1-01 = 4 tag × 6 ảnh; QC1-02 = (L1 + R1) × 6 ảnh; QC1-03, 04, 05, 06 = 21 polyline `lane`; QC1-07 = 13 drivable + 1 crosswalk + 6 road_curb; QC1-08 = 4 đèn; QC1-09 = 4 đèn + 8 biển; QC1-10 = 8 biển.

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-08 | A12 | traffic_light, box (723,52) 52×73 | nặng | Đèn xe hướng về xe (`facing = front`) đang sáng xanh nhưng gán `color = red` |
| 2 | QC1-03 | A04 | lane, polyline bắt đầu (1278,537) | nặng | Vạch bên phải xe, bên phải R1, gán `L2`; đúng ra là `R2` |
| 3 | QC1-03 | A04 | lane, polyline bắt đầu (1277,515) | nặng | Cùng vạch đôi trắng bên phải, gán `L2`; đúng ra là `R2` |
| 4 | QC1-05 | A04 | lane, hai polyline L1 (bắt đầu (69,554) và (18,554)) | chính | Vạch đôi vàng bên trái vẽ thành hai polyline; guideline: một vạch đôi là một polyline ở giữa |
| 5 | QC1-05 | A04 | lane, hai polyline L2 (bắt đầu (1278,537) và (1277,515)) | chính | Vạch đôi trắng bên phải vẽ thành hai polyline thay vì một |
| 6 | QC1-05 | A07 | lane, hai polyline R2 ((1196,451)→(727,271) và (1280,486)→(1194,450)) | chính | Một vạch bị tách làm hai đoạn, nên nối thành một polyline |
| 7 | QC1-05 | A09 | lane, hai polyline L2 (bắt đầu (421,657) và (475,663)) | chính | Vạch đôi trắng vẽ thành hai polyline thay vì một |
| 8 | QC1-07 | A12 | drivable | chính | Vùng lái chỉ phủ đoạn sau vạch ngựa vằn; mặt đường phía trước xe (từ y ≈ 470 đến mui xe) không có vùng lái |
| 9 | QC1-10 | A07 | traffic_sign (thiếu) quanh (548,205) | chính | Biển cảnh báo hình thoi dưới cầu vượt (nhìn từ phía sau, `facing = back`) chưa gán |
| 10 | QC1-10 | A07 | traffic_sign (thiếu) quanh (595,222) | chính | Biển hình thoi thứ hai cạnh biển trên chưa gán |
| 11 | QC1-01 | A04 | tag timeofday | nhẹ | Thiếu tag `timeofday` |
| 12 | QC1-01 | A04 | tag weather | nhẹ | Thiếu tag `weather` |
| 13 | QC1-01 | A04 | tag source | nhẹ | Thiếu tag `source` |

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| A04 | Hai polyline vạch đôi trắng bên phải đang gán L2. Ego đang ở làn có R1 là vạch đứt bên phải, nên mình xếp chúng là R2 (lỗi nặng QC1-03). Lead xác nhận được không? | |
| A07 | Bên trái xe là dải bê tông, mình không thấy vạch sơn nào ở bên trái. Có cần L1 không (lint báo thiếu L1)? | |
| A07 | Polyline R2 chạy dọc rìa làn xe tải bên phải: đó là vạch sơn hay chỉ là mép đường (nếu là mép thì phải là road_curb)? | |
| A09 | Lint báo thiếu R1. Bên phải xe là lề/vỉa hè, mình không thấy vạch; có cần R1 không? | |
| A12 | Đèn người đi bộ (box (965,282), `facing = front`) đang gán `color = off` nhưng hình người đi bộ đang sáng trắng. Nên là off hay green? Nếu sai thì là lỗi nặng. | |
| A01 | Biển xanh nhỏ ở khoảng (440,472) chưa gán. Biển này cao từ 8 px và đọc được không, có thiếu biển không? | |

## Quyết định
Lỗi nặng: 3   Lỗi chính: 7 / 74 nhãn = 9,5 %   Lỗi nhẹ: 3   Ca chờ lead: 6  
Quyết định (Release / Hold / Rework): **Rework**  
Lý do (theo luật của phiếu): Có ít nhất một lỗi nặng thì Rework, và ở đây có 3 lỗi nặng: đèn xe sai màu ở A12 (chắc chắn, ảnh phóng to cho thấy đèn xanh) và hai polyline sai `position` ở A04. Ngoài ra lỗi chính 7 / 74 nhãn = 9,5 %, vượt ngưỡng 5 %, nên dù không tính lỗi nặng thì vẫn Rework. Các ca mơ hồ ở trên chưa có lời đáp, nhưng không đổi kết luận vì lỗi nặng ở A12 không phụ thuộc vào chúng, nên không chuyển sang Hold.

Loại lỗi: bỏ sót = thiếu nhãn phải có; thừa = gán cái không phải đối tượng; sai phạm vi = hình lệch, sai chiều, dừng sai chỗ, tràn vùng. Ba loại này theo cách chia lỗi gán nhãn của ISO/IEC 5259-4 (mục 8.4.2); "sai thuộc tính" và "lỗi file" là khóa học thêm. Cách xếp mức: [thang mức lỗi](../docs/qc_severity_road_v1.0.md).
