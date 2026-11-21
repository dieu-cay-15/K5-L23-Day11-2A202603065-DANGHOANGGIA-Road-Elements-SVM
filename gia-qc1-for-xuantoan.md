# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): xuantoan        Người kiểm (học viên): gia (Đặng Hoàng Gia)  
Ngày: 2026-11-21                         Phiên bản guideline: Road v1.0  
File được kiểm (tên + `revision` trong manifest): `xuantoan-front.zip` (`sha256: 2e69c7f6...`), `xuantoan-fisheye.zip` (`sha256: 1fea7c95...`) — `revision: 1` (`xuantoan-manifest.json`)  
Số ảnh kiểm: 6 (`A01`, `A03`, `A04`, `B01`, `B02`, `B06`; trong đó **`B01` không có lỗi**) (+ 0 ảnh thêm)   Số nhãn đã kiểm (shape + tag): 57 (33 shape + 24 tag)  

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 24 | 0 | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 6 | 1 | nặng |
| QC1-03 position | sai thuộc tính / thừa | 14 | 10 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 14 | 1 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 14 | 1 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 14 | 4 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 13 | 6 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 4 | 4 (2 nặng, 2 chính) | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 6 | 1 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 2 | 1 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 12 | 2 | chính |
| QC1-12 file | lỗi file | 57 | 0 | nhẹ / nặng |

*(Ghi chú kiểm file toàn lô: cả 2 file zip mở lại được, `contains_images = false`, đủ tên label và thuộc tính Road v1.0. Ngoài 6 ảnh mẫu, `road_check lint` còn ghi nhận 2 lỗi nhẹ `QC1-12` điểm lặp liền nhau ở `A02` và `A11`, bạn nên xóa luôn khi Rework.)*

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-02 | A04 | `lane` (`R1`) | nặng | Thiếu vạch `R1` (vạch trắng đứt bên phải làn đang đi `#1` bị để mặc định `position=L1`). |
| 2 | QC1-03 | A01 | `lane#0@(110,717)` | nặng | Vạch trắng đứt sát trái làn đang đi là `L1`, nhưng gán nhầm `position = R1`. |
| 3 | QC1-03 | A01 | `lane#1@(0,599)` | nặng | Vạch trắng đôi mép ngoài cùng bên trái là `L2`, nhưng gán nhầm `position = L1`. |
| 4 | QC1-03 | A01 | `lane#2@(711,720)` | nặng | Vạch trắng đứt sát phải làn đang đi là `R1`, nhưng gán nhầm `position = L2`. |
| 5 | QC1-03 | A04 | `lane#1@(720,535)` | nặng | Vạch trắng đứt sát phải làn đang đi là `R1`, nhưng để mặc định `position = L1`. |
| 6 | QC1-03 | A04 | `lane#2@(1280,537)` | nặng | Vạch trắng liền ngoài cùng làn phải là `R2`, nhưng để mặc định `position = L1`. |
| 7 | QC1-03 | A04 | `lane#3@(1279,515)` | nặng | Vạch mép ngoài dải đệm làn xe đạp nhưng để mặc định `position = L1` (đúng là `other` hoặc không gán). |
| 8 | QC1-03 | A04 | `lane#7@(23,550)` | nặng | Tách nét trái của vạch vàng đôi `L1` thành một vạch `L2` thừa (quy tắc: vạch đôi chỉ vẽ 1 polyline `L1`, `kind = double` ở giữa hai nét). |
| 9 | QC1-03 | B06 | `lane#2@(207,293)` | nặng | Camera hông trái (`fisheye_left`): gán `position = L1`, quy tắc bắt buộc `position = other`. |
| 10 | QC1-03 | B06 | `lane#3@(193,259)` | nặng | Camera hông trái (`fisheye_left`): gán `position = L1`, quy tắc bắt buộc `position = other`. |
| 11 | QC1-03 | B06 | `lane#4@(926,495)` | nặng | Camera hông trái (`fisheye_left`): gán `position = L1`, quy tắc bắt buộc `position = other`. |
| 12 | QC1-04 | A03 | `lane#2@(594,379)` | chính | Vẽ ngược chiều từ xa về gần (`(594,379) → (701,466)`), phải vẽ từ gần xe ra xa. |
| 13 | QC1-05 | A03 | `lane#2@(594,379)` | chính | Vạch `R1` nối qua đoạn bị che/chữ `SCHOOL` nhưng không bật cờ `occluded` (`occluded=0`). |
| 14 | QC1-06 | A01 | `lane#1@(0,599)` | chính | Vạch trắng đôi mép trái nhưng để `kind = single`, đúng là `double`. |
| 15 | QC1-06 | A01 | `lane#2@(711,720)` | chính | Vạch trắng đứt nhưng gán `style = solid, color = yellow`, đúng là `dashed, white`. |
| 16 | QC1-06 | A04 | `lane#1@(720,535)` | chính | Vạch trắng đứt nhưng để mặc định `style = solid`, đúng là `dashed`. |
| 17 | QC1-06 | B06 | `lane#4@(926,495)` | chính | Vạch trắng đứt sát dải phân cách tàu điện nhưng để mặc định `style = solid`, đúng là `dashed`. |
| 18 | QC1-07 | A01 | `drivable#5@(4,603)` | chính | Làn cùng chiều bên trái gán `area_type = direct` (mặc định), đúng là `alternative`. |
| 19 | QC1-07 | A01 | `drivable#7@(732,718)` | chính | Làn cùng chiều bên phải gán `area_type = direct` (mặc định), đúng là `alternative`. |
| 20 | QC1-07 | A03 | `drivable#3@(239,700)` | chính | Gộp cả làn đang đi và làn bên phải vào một vùng `direct` duy nhất thay vì tách `direct` và `alternative`. |
| 21 | QC1-07 | A04 | `drivable#0@(1279,540)` | chính | Làn cùng chiều bên phải gán `area_type = direct` (mặc định), đúng là `alternative`. |
| 22 | QC1-07 | B02 | `drivable#3@(136,673)` | chính | Vùng `drivable` tràn sang làn bên trái cắt qua đảo phân cách giữa đường. |
| 23 | QC1-07 | B06 | `drivable` (bỏ sót) | chính | Thiếu hoàn toàn polygon `drivable` trên ảnh `B06` (trọng tâm ảnh yêu cầu `drivable` + `lane`). |
| 24 | QC1-08 | A04 | `traffic_light#4@(551,268)` | nặng | Đèn hướng về xe (`facing = front`) đang sáng **màu xanh (`green`)** nhưng gán nhầm `color = red` (mặc định CVAT). |
| 25 | QC1-08 | A04 | `traffic_light#5@(600,273)` | nặng | Đèn hướng về xe (`facing = front`) đang sáng **màu xanh (`green`)** nhưng gán nhầm `color = red` (mặc định CVAT). |
| 26 | QC1-08 | A03 | `traffic_light` (bỏ sót) | chính | Bỏ sót các cụm đèn xanh hướng về xe rõ trên trục đường (tọa độ khoảng `(628,297)`, `(706,307)`, cao ≥ 8 px). |
| 27 | QC1-08 | B02 | `traffic_light` (bỏ sót) | chính | Bỏ sót cụm đèn đỏ đang sáng rõ hướng về xe ở cột bên phải (`(876,282)–(889,322)`). |
| 28 | QC1-09 | A03 | `traffic_sign#0@(220,172)` | chính | Tấm biển quay mặt sau nhưng gán `facing = front, group = prohibitory` (đúng là `facing = back`). |
| 29 | QC1-10 | A03 | `traffic_sign` (bỏ sót) | chính | Bỏ sót 2 biển cảnh báo rõ bên lề phải (biển công trường hình thoi cam `(794,310)` và biển trường học vàng `(1000,275)`). |
| 30 | QC1-11 | B02 | `traffic_light#0@(118,114)` | chính | Tâm hộp nằm ngoài 80 % bán kính ảnh fisheye (`> 512 px` từ tâm), cần bật `edge_zone = true` (đang để `false`). |
| 31 | QC1-11 | B02 | `traffic_light#4@(1069,74)` | chính | Tâm hộp nằm ngoài 80 % bán kính ảnh fisheye (`> 512 px` từ tâm), cần bật `edge_zone = true` (đang để `false`). |

*(Ảnh **`B01`** trong 6 ảnh mẫu được kiểm tra đạt **không lỗi**: đủ 4 tag đúng chuẩn `fisheye_front/day/clear/real`, polygon `crosswalk` và `drivable direct` gọn, không tràn lề và dừng sạch ngay mép cản trước xe mình.)*

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| A03 | Ảnh quay lúc trời sẫm ánh đèn phố: chọn `timeofday = dusk` hay `day` đều chấp nhận hay chuẩn hoá một giá trị? | *(Không ảnh hưởng quyết định Rework do lô đã có nhiều lỗi nặng rõ ràng)* |

## Quyết định
Lỗi nặng: 13   Lỗi chính: 18 / 57 nhãn = 31,6 %   Lỗi nhẹ: 0   Ca chờ lead: 0 (1 ghi chú không ảnh hưởng kết luận)  
Quyết định (Release / Hold / Rework): **Rework**  
Lý do (theo luật của phiếu): Lô còn **13 lỗi nặng** (≥ 1 lỗi nặng là bắt buộc Rework — chủ yếu do quên sửa thuộc tính mặc định CVAT của `lane.position`, nhầm `L1/R1/L2`, gán sai `position` ở camera fisheye hai bên và gán đèn xanh `facing=front` thành `red` ở `A04`) đồng thời tỉ lệ lỗi chính đạt **31,6 % > 5 %** số nhãn đã kiểm (18 / 57 nhãn).  

Loại lỗi: bỏ sót = thiếu nhãn phải có; thừa = gán cái không phải đối tượng; sai phạm vi = hình lệch, sai chiều, dừng sai chỗ, tràn vùng. Ba loại này theo cách chia lỗi gán nhãn của ISO/IEC 5259-4 (mục 8.4.2); "sai thuộc tính" và "lỗi file" là khóa học thêm. Cách xếp mức: [thang mức lỗi](docs/qc_severity_road_v1.0.md).
