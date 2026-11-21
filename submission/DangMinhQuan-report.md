# Báo cáo cá nhân — Ngày 11
Họ tên: Đặng Minh Quân          Mã học viên: 2A202603171
Phiên bản CVAT (Help → About): 2.74.1
Guideline: Road v1.0    Lần nộp (`revision` trong manifest): 1
Thời điểm export (ngày giờ trên CVAT): 21/11/2026 00:32 (UTC+7)    Số lần nộp lại sau Rework: 0

## 1. Kiểm project
| Mục | Đúng như guideline Road v1.0? | Ghi chú |
| --- | --- | --- |
| 6 label, đúng kiểu | Có | lane, road_curb = polyline; crosswalk, drivable = polygon; traffic_light, traffic_sign = rectangle |
| Thuộc tính và giá trị | Có | lane: position/style/color/kind; drivable: area_type; light: color/type/facing/edge_zone; sign: group/facing/edge_zone |
| 4 tag ảnh | Có | camera, timeofday, weather, source — 12/12 ảnh front, 8/8 ảnh fisheye đủ bốn tag |
Cách kết thúc polyline trên bản CVAT này: bấm đúp chuột trái tại điểm cuối.
Cách đặt tag ảnh trên bản CVAT này: chọn label tag rồi bấm một lần vào ảnh, sau đó chọn `value` trong Details.

## 2. Số lượng đã gán
| Task | Ảnh | lane | road_curb | crosswalk | drivable | traffic_light | traffic_sign |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| front | 12 | 28 | 9 | 7 | 24 | 24 | 21 |
| front-extra (đã làm 0 / 4) | 4 | 0 | 0 | 0 | 0 | 0 | 0 |
| fisheye | 8 | 7 | 8 | 11 | 5 | 6 | 8 |
| fisheye-extra (đã làm 0 / 4) | 4 | 0 | 0 | 0 | 0 | 0 | 0 |

Tổng: 20 ảnh đã gán (12 front + 8 fisheye), 158 shape (113 front + 45 fisheye), 80 tag (48 + 32).

## 3. Bảng ca khó
| Ảnh | Nhãn | Phân vân giữa | Đã chọn | Lý do |
| --- | --- | --- | --- | --- |
| A05 — **CHỜ LEAD XÁC NHẬN** | lane | mép đường vật lý: để `lane` trống hay coi mép là L1/R1 | Để trống, chỉ gán `road_curb` | Đường một chiều hẹp, hai bên xe đỗ sát, không có vạch sơn nào. Tôi không tự đặt luật: giữ nguyên trạng và chờ lead trả lời |
| A03 — **CHỜ LEAD XÁC NHẬN** | lane | vạch vàng đôi **một liền một đứt** (QCVN 1.4) | `kind = double`, `style = solid` | Road v1.0 không có giá trị cho vạch 1.4 hỗn hợp, nên một nửa thông tin (nửa đứt) bị mất khi chuyển sang thuộc tính. Đây là **hạn chế của schema**, không phải lỗi vẽ: đã ghi lại và chờ lead cách chuẩn hoá |
| B03 | crosswalk | cụm vạch trắng ở rìa trái có phải vạch ngựa vằn | Không vẽ | Đã phóng 3× vùng rìa: đó là vạch mép đường chạy dọc + làn xe đạp sơn đỏ, không phải vạch ngựa vằn ngang. Ảnh bị cắt nhưng đối tượng không thuộc `crosswalk`, nên bỏ là đúng chứ không phải vì "gần rìa" |
| A06, A08 | drivable | làn sơn xanh có tính vào vùng lái | Không | Làn xe đạp không phải phần đường xe chạy |
| B05–B08 | lane | có dùng L1/R1 ở camera hai bên | position = other | Quy tắc 4 bắt buộc `other` |

## 4. Phiếu QC 1 nhận được
Bạn kiểm lô của tôi: NGUYỄN TUẤN HƯNG — 2A202603199   Quyết định nhận được: chưa có (chưa nhận phiếu cho lô của tôi)
| Mã lỗi | Số lỗi | Đồng ý? | Đã sửa? |
| --- | ---: | --- | --- |
| – | 0 | – | – |

Chiều ngược lại đã làm được: tôi kiểm lô của Hưng (bản `r1/`, 28 ảnh, 326 nhãn) và ghi phiếu `DangMinhQuan-qc1-for-NguyenTuanHung.md`. Kết quả **Hold**: 2 lỗi nặng tiềm tàng (A06 và A14 thiếu R1 — chờ lead xác nhận vạch mép phải có phải R1), A05 không có vạch sơn nên không kết luận thay lead, và B11 không có shape nào (chờ lead phân mã). Lỗi chính 0/326 = 0 %.

## 5. Kiểm file export
| File | Mở lại được? | Số shape ảnh 1 (job / file) | Số shape ảnh 2 (job / file) | Tag camera có trong XML? |
| --- | --- | --- | --- | --- |
| DangMinhQuan-front.zip | Có | A01: 9 / 9 | A02: 7 / 7 | Có |
| DangMinhQuan-fisheye.zip | Có | B01: 6 / 6 | B02: 8 / 8 | Có |

`lint` báo **20 ảnh, 5 cảnh báo** (0 lỗi mức "chính"). Danh sách đầy đủ, có mã:

| # | Mã | Mức | Ảnh | Nhãn | Nội dung |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-02 | nặng | A05 | lane | thiếu L1 — ca mơ hồ, **chờ lead** (không thấy vạch sơn) |
| 2 | QC1-02 | nặng | A05 | lane | thiếu R1 — cùng ca mơ hồ, **chờ lead** |
| 3 | QC1-10 | nhẹ | A10 | traffic_sign #10 @(536,235) | box cao < 8 px, dưới ngưỡng bắt buộc |
| 4 | QC1-10 | nhẹ | A10 | traffic_sign #11 @(830,226) | box cao < 8 px |
| 5 | QC1-10 | nhẹ | A10 | traffic_sign #15 @(441,233) | box cao < 8 px |

Cả hai cảnh báo mức nặng đều thuộc **A05** (L1 và R1 của cùng một ảnh) — không có ảnh nào khác bị nặng.

## 6. Ảnh chụp màn hình
1. Tab Labels của project: `screenshots/labels.png`
2. Ảnh camera trước đã gán đủ: `screenshots/front-a04.png`
3. Ảnh fisheye, phóng to đoạn polyline cong: `screenshots/fisheye-b04.png`
4. Đoạn XML có `<polyline label="lane">`:
```xml
<polyline label="lane" source="manual" occluded="0"
  points="114.05,720.00;182.95,657.12;285.68,570.25;321.00,540.65;340.80,522.64"
  z_order="0">
  <attribute name="position">L1</attribute>
  <attribute name="style">dashed</attribute>
  <attribute name="color">white</attribute>
  <attribute name="kind">single</attribute>
</polyline>
```

## 7. Tự đánh giá
**Nguồn gốc hai lỗi QC1-04 và QC1-05 nêu dưới đây:** do **tôi tự phát hiện** khi chạy `python -m road_lab.road_check lint` trên chính file export của mình, rồi tự sửa — **không phải** kết quả của một phiếu QC chính thức (mục 4 ghi rõ chưa nhận được phiếu nào). Cụ thể lint báo 6 cặp polyline cùng `position` (A03, A04, A08, A09, A10, A11) và 5 polyline vẽ ngược chiều (A03, A07, A09, A11, A12); tôi đã gộp các cặp thành một nét và đảo chiều các đường còn lại, sau đó lint còn 0 lỗi mức chính.

Hai lỗi này là loại tôi mắc nhiều nhất hôm nay. Cách tránh ở Ngày 20: luôn chạy `road_check lint` trước khi Finish job; vạch đứt vẽ **một nét liền** băng qua khe (không tách đoạn), và luôn bắt đầu từ mép dưới (gần xe) đi lên xa.

**Nhãn đi vào model ở đâu:** polyline `lane` bị lấy mẫu theo hàng để tạo cặp (y, x) làm đích row-anchor. Nếu guideline yêu cầu một nét liên tục cho vạch đứt mà tôi tách thành nhiều polyline, dữ liệu trở thành không nhất quán: ở những hàng thuộc khoảng khe không có điểm annotation, bước chuyển polyline → row-anchor có thể hiểu là "không có làn", nên model mất khả năng dự đoán vị trí làn đúng tại chỗ đường đứt nét và LKA mất bám làn ở đó. Mức ảnh hưởng thực tế còn tuỳ pipeline chuyển đổi xử lý khoảng khe thế nào (nội suy hay bỏ trống) — đây là điểm tôi muốn kiểm chứng thêm.

## 8. (Tùy chọn, buffer) Từ polyline đến đích row-anchor
Không làm — cần bài của bạn được kiểm cùng ảnh, chưa nhận được file của bạn Hưng.
