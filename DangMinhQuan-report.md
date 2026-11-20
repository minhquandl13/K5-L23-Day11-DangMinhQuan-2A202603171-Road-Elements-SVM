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

## 3. Bảng ca khó
| Ảnh | Nhãn | Phân vân giữa | Đã chọn | Lý do |
| --- | --- | --- | --- | --- |
| A05 | lane | vẽ mép đường thành L1/R1 hay để trống | Để trống | Đường không có vạch sơn nào, chỉ có lề vật lý nên gán road_curb; chờ lead xác nhận |
| B03 | crosswalk | vẽ cụm vạch nhỏ ở rìa hay bỏ | Bỏ | Cụm vạch gần như ra ngoài vùng ảnh |
| A03 | lane | vạch vàng đôi một liền một đứt | kind = double, style = solid | Road v1.0 không có giá trị riêng cho 1.4 |
| A06, A08 | drivable | làn sơn xanh có tính vào vùng lái | Không | Làn xe đạp không phải phần đường xe chạy |
| B05–B08 | lane | có dùng L1/R1 ở camera hai bên | position = other | Quy tắc 4 bắt buộc `other` |

## 4. Phiếu QC 1 nhận được
Bạn kiểm lô của tôi: chưa được phân công   Quyết định nhận được: chưa có
| Mã lỗi | Số lỗi | Đồng ý? | Đã sửa? |
| --- | ---: | --- | --- |
| – | 0 | – | – |

## 5. Kiểm file export
| File | Mở lại được? | Số shape ảnh 1 (job / file) | Số shape ảnh 2 (job / file) | Tag camera có trong XML? |
| --- | --- | --- | --- | --- |
| DangMinhQuan-front.zip | Có | A01: 9 / 9 | A02: 7 / 7 | Có |
| DangMinhQuan-fisheye.zip | Có | B01: 6 / 6 | B02: 8 / 8 | Có |

`lint`: 20 ảnh, 5 cảnh báo — 2 nặng (A05 L1/R1, ca khó), 0 chính, 3 nhẹ (A10 box < 8 px).

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
Lỗi nhiều nhất hôm nay: QC1-05 (vạch đứt bị tách thành 2–3 polyline) và QC1-04 (vẽ từ xa về gần). Cách tránh ở Ngày 20: chạy `road_check lint` trước khi Finish job; vạch đứt vẽ một nét liên tục băng qua khe, luôn bắt đầu từ mép dưới đi lên xa.

Nhãn đi vào model ở đâu: polyline `lane` được lấy mẫu theo hàng để tạo cặp (y, x) làm đích row-anchor. Vạch bị tách đôi khiến model học "không có làn" ở khoảng khe — LKA mất làn đúng tại chỗ đường đứt nét.

## 8. (Tùy chọn, buffer) Từ polyline đến đích row-anchor
Không làm — cần bài của bạn được kiểm cùng ảnh, chưa được phân công.
