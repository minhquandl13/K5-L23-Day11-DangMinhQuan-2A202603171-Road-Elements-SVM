# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): Đặng Minh Quân (2A202603171) — **tự kiểm**, lớp chưa phân công bạn kiểm
Người kiểm (học viên): Đặng Minh Quân — ngày 21/11/2026 — Phiên bản guideline: Road v1.0
File được kiểm (tên + `revision` trong manifest): `DangMinhQuan-front.zip`, `revision 1`, `contains_images = false`
Số ảnh kiểm: 6 (+ 6 ảnh thêm: A07–A12)   Số nhãn đã kiểm (shape + tag): 161 (113 shape + 48 tag)

> Ghi chú minh bạch: chưa được phân công lô của học viên khác, nên phiếu này là **tự kiểm** lô front của chính tôi bằng đúng 12 mã và đúng quy trình; phần "Ca mơ hồ" giữ nguyên để lead trả lời.

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 12 | 0 | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 12 | 2 (chờ lead) | nặng |
| QC1-03 position | sai thuộc tính / thừa | 28 | 0 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 28 | 0 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 28 | 0 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 28 | 0 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 24 | 0 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 24 | 0 | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 21 | 0 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 21 | 3 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | – | – | chính |
| QC1-12 file | lỗi file | 2 | 0 | nhẹ / nặng |

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-10 | A10 | traffic_sign #10 @(536,235) | nhẹ | Box cao < 8 px — dưới ngưỡng bắt buộc, có thể bỏ |
| 2 | QC1-10 | A10 | traffic_sign #11 @(830,226) | nhẹ | Box cao < 8 px — dưới ngưỡng bắt buộc, có thể bỏ |
| 3 | QC1-10 | A10 | traffic_sign #15 @(441,233) | nhẹ | Box cao < 8 px — dưới ngưỡng bắt buộc, có thể bỏ |

Đã sửa trong lô này trước khi lập phiếu: 6 cặp polyline cùng `position` (vạch đứt bị tách — QC1-05) ở A03, A04, A08, A09, A10, A11 đã gộp thành một nét; 5 polyline vẽ ngược chiều (QC1-04) ở A03, A07, A09, A11, A12 đã đảo lại thành gần → xa. Sau khi sửa, `lint` báo **0 lỗi chính**.

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| A05 | Đường một chiều hẹp, hai bên xe đỗ sát lề, **không có vạch sơn nào**. Để `lane` trống và chỉ vẽ `road_curb` cho hai lề vật lý — có đúng không, hay phải coi mép đường là L1/R1? | (chờ) |

## Quyết định
Lỗi nặng: 0 (2 mục QC1-02 chuyển sang ca chờ lead)   Lỗi chính: 0 / 161 nhãn = 0 %   Lỗi nhẹ: 3   Ca chờ lead: 1
Quyết định (Release / Hold / Rework): **Release** (có 1 ca chờ lead, không chặn)
Lý do (theo luật của phiếu): không có lỗi mức nặng nào còn lại sau khi loại ca mơ hồ; tỉ lệ lỗi chính 0 % < 5 % nên không Rework; ba lỗi nhẹ dưới ngưỡng 8 px không bắt buộc.

Loại lỗi: bỏ sót = thiếu nhãn phải có; thừa = gán cái không phải đối tượng; sai phạm vi = hình lệch, sai chiều, dừng sai chỗ, tràn vùng. Ba loại này theo cách chia lỗi gán nhãn của ISO/IEC 5259-4 (mục 8.4.2); "sai thuộc tính" và "lỗi file" là khóa học thêm. Cách xếp mức: [thang mức lỗi](../docs/qc_severity_road_v1.0.md).
