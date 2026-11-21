# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): NGUYỄN TUẤN HƯNG — 2A202603199
Người kiểm (học viên): Đặng Minh Quân — 2A202603171 — ngày 21/11/2026 — Phiên bản guideline: Road v1.0
File được kiểm (tên + `revision` trong manifest): `NguyenTuanHung-front.zip`, `NguyenTuanHung-fisheye.zip`, `NguyenTuanHung-front-extra.zip`, `NguyenTuanHung-fisheye-extra.zip` — bản trong `r1/`, manifest ghi `revision: 1`. Lưu ý: manifest revision 1 chỉ khai báo hai file lõi (front, fisheye); hai zip `-extra` nằm ngoài manifest nên tôi kiểm riêng và không cộng vào kết luận chính thức của lô.
Số ảnh kiểm: 6 (A01–A06) + 22 ảnh còn lại kiểm bằng `road_check lint`   Số nhãn đã kiểm (shape + tag): 326 (214 shape + 112 tag)

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 28 | 0 | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 16 | 2 (A06, A14) + 2 chờ lead (A05) | nặng |
| QC1-03 position | sai thuộc tính / thừa | 47 | 0 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 47 | 0 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 47 | 0 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 47 | 0 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 94 | 0 (B11 chờ phân mã) | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 37 | 0 | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 36 | 0 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 36 | 0 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 52 | 0 | chính |
| QC1-12 file | lỗi file | 4 | 0 | nhẹ / nặng |

Lô gồm 214 shape (47 lane, 42 road_curb, 32 drivable, 20 crosswalk, 37 đèn, 36 biển) + 112 tag = 326 nhãn. QC1-07 gộp drivable + crosswalk + road_curb theo cách `road_check` gán mã.

Tag: 28/28 ảnh đủ bốn tag, `camera` đúng cho cả bốn nhóm (front, fisheye_front/rear/left/right). File: cả bốn zip mở được, không có nhãn lạ.

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-02 | A06 | lane (R1) | nặng | Thiếu R1. Ảnh có vạch trắng mép phải của làn (vùng x≈640–900, y≈450–470) nên đây là bỏ sót, không phải "không thấy vạch" |
| 2 | QC1-02 | A14 | lane (R1) | nặng | Thiếu R1. Ảnh đêm, vạch mép phải vẫn đọc được nhờ đèn đường (vùng x≈690–720, y≈480–580) |
| 3 | QC1-02 | A05 | lane (L1, R1) | nặng (chờ lead) | Đường không có vạch sơn nào — cùng ca mơ hồ với lô của tôi; không kết luận thay lead |

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| A05 | Đường một chiều hẹp, hai bên xe đỗ sát lề, không có vạch sơn. Để `lane` trống và chỉ vẽ `road_curb` có đúng không? | (chờ) |
| A06 | Vạch trắng phía phải ở x≈640–900 thuộc **R1** của làn xe mình hay là vạch phân làn/vành đai bên phải? Nếu là R1 thì đây là lỗi nặng (bỏ sót) | (chờ) |
| A14 | Như A06 — vạch mép phải ban đêm là R1 hay vạch của làn bên cạnh? | (chờ) |
| B11 | Ảnh **không có shape nào** (chỉ có 4 tag) trong khi vạch kẻ và vùng lái nhìn thấy rõ. Xếp vào QC1-07 (bỏ sót vùng lái/vạch) hay QC1-02 (bỏ sót vạch làn)? Cả ảnh bị bỏ trống có tính là một lỗi nặng hay nhiều lỗi? | (chờ) |

## Quyết định
Lỗi nặng: 2 (A06 R1, A14 R1) — cộng 2 mục chờ lead (A05)   Lỗi chính: 0 / 326 nhãn = 0 %   Lỗi nhẹ: 0   Ca chờ lead: 4
Quyết định (Release / Hold / Rework): **Hold**
Lý do (theo luật của phiếu): mức nặng của A06/A14 phụ thuộc việc vạch phải có phải là R1 hay không, và B11 chưa rõ mã — đều là câu hỏi còn chờ lead, ảnh hưởng trực tiếp tới kết luận. Nếu lead xác nhận vạch phải là R1 thì hai lỗi này là lỗi nặng thật và quyết định chuyển thành **Rework** (luật: có ít nhất một lỗi nặng → Rework). Tỉ lệ lỗi chính 0 % < 5 % nên không có lý do Rework từ phía lỗi chính.

Loại lỗi: bỏ sót = thiếu nhãn phải có; thừa = gán cái không phải đối tượng; sai phạm vi = hình lệch, sai chiều, dừng sai chỗ, tràn vùng. Ba loại này theo cách chia lỗi gán nhãn của ISO/IEC 5259-4 (mục 8.4.2); "sai thuộc tính" và "lỗi file" là khóa học thêm. Cách xếp mức: [thang mức lỗi](../docs/qc_severity_road_v1.0.md).
