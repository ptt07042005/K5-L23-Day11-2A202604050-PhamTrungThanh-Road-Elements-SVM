# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): Đỗ Anh Hoàng (`DoAnhHoang`)        Người kiểm (học viên): Phạm Trung Thành (`2A202604050`)  
Ngày: 2026-11-21                          Phiên bản guideline: Road v1.0  
File được kiểm (tên + `revision` trong manifest): `DoAnhHoang-front.zip`, `DoAnhHoang-fisheye.zip` (`revision: 1` trong `DoAnhHoang-manifest.json`)  
Số ảnh kiểm: 6 ảnh bắt buộc (`A01, A03, A04, A08, B01, B03`) + 3 ảnh thêm (`A14, A16, B12`, ghi riêng)   Số nhãn đã kiểm (shape + tag): **102 nhãn** trên 6 ảnh bắt buộc (`24 tag + 78 shape`) + **44 nhãn** trên 3 ảnh thêm (`12 tag + 32 shape`) = **146 nhãn**  

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 36 tag (9 ảnh × 4 tag) | 0 | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 9 ảnh (kiểm L1/R1) | 2 | nặng |
| QC1-03 position | sai thuộc tính / thừa | 24 `lane` | 1 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 36 polyline (`24 lane + 12 road_curb`) | 0 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 24 `lane` | 3 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 24 `lane` | 0 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 32 polygon (`24 drivable + 8 crosswalk`) | 4 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 20 `traffic_light` | 0 | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 42 box (`20 traffic_light + 22 traffic_sign`) | 1 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 22 `traffic_sign` | 0 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 3 ảnh fisheye (`B01, B03, B12`, 23 shape) | 1 | chính |
| QC1-12 file | lỗi file | 2 file zip + 1 manifest (`contains_images: false`) | 0 | nhẹ / nặng |

## Danh sách lỗi (mỗi lỗi một dòng)
*(Ảnh kiểm **không có lỗi**: **`A03`** — đủ 4 tag, đủ `L1/R1` kèm `occluded`, tách `direct/alternative` gọn không tràn xe đỗ, đủ 2 đèn và 3 biển đúng thuộc tính.)*

| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | `QC1-07` | `A01` | `drivable#7@(1277,701)` | chính | Vùng `alternative` vẽ tràn ra ngoài vạch vàng liền `R2` lên phần lề đường sát lan can bên phải |
| 2 | `QC1-05` | `A04` | `lane#5@(56,556)`, `lane#10@(36,548)` | chính | Có 2 polyline cùng `position=L1` cho cùng một vạch vàng đôi (đúng chỉ vẽ 1 polyline có `kind=double`) |
| 3 | `QC1-07` | `A04` | `drivable#12@(3,558)` | chính | Vẽ thêm vùng `alternative` sang làn xe đi ngược chiều bên trái vạch vàng đôi |
| 4 | `QC1-05` | `A08` | `lane#4@(39,359)`, `lane#25@(416,294)` | chính | Có 2 polyline cùng `position=L2` trên cùng phía trái |
| 5 | `QC1-07` | `A08` | `drivable#8@(55,498)`, `drivable#14@(34,357)`, `drivable#15@(1,320)` | chính | Gán nhiều polygon `area_type=direct` tràn sang các làn xe đi ngược chiều bên trái |
| 6 | `QC1-07` | `B01` | `crosswalk#1@(163,674)` | chính | Đỉnh dưới của polygon `crosswalk` nhô nhẹ xuống phần phản chiếu trên cản trước thân xe |
| 7 | `QC1-09` | `B03` | `traffic_sign#10@(841,241)` | chính | Biển chỉ dẫn hình chữ nhật màu xanh dương bên phải bị gán sai `group=prohibitory` (đúng là `information`) |
| 8 | `QC1-02` | `A14` *(ảnh thêm)* | `lane` (`R1`) | nặng | Thiếu vạch `R1` màu trắng liền ở mép phải làn xe đang đi |
| 9 | `QC1-05` | `A14` *(ảnh thêm)* | `lane#6@(294,606)`, `lane#7@(331,606)` | chính | Tách vạch vàng đôi thành 2 polyline riêng cùng mang `position=L1` |
| 10 | `QC1-02` | `A16` *(ảnh thêm)* | `lane` (`R1`) | nặng | Thiếu vạch `R1` bên phải làn xe đang đi (do vạch phải bị gán nhầm sang `L1`) |
| 11 | `QC1-03` | `A16` *(ảnh thêm)* | `lane#12@(927,514)` | nặng | Vạch nằm bên phải làn xe (sát taxi vàng) nhưng gán sai `position=L1` (đúng phải là `R1`) |
| 12 | `QC1-11` | `B12` *(ảnh thêm)* | `lane#4@(1089,270)` | chính | Polyline trên ảnh fisheye chỉ có 3 điểm, chưa đặt đủ dày điểm bám theo cung cong |

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| `A05, A06, A07, A09` | `road_check lint` báo 5 cảnh báo `QC1-02` thiếu `L1/R1` ở các phía đường không có vạch sơn kẻ đường (chỉ có bó vỉa/xe đỗ) — đã xác nhận không tính lỗi | Miễn trừ theo Guideline Road v1.0 & `CHECKPOINTS.md` (không vẽ vạch giả khi ảnh không thấy vạch sơn) |

## Quyết định
Lỗi nặng: **3** *(trên ảnh thêm `A14, A16`; trên 6 ảnh bắt buộc: 0)*   Lỗi chính: **9 / 146 nhãn = 6.16 %** *(trên 6 ảnh bắt buộc: 6 / 102 nhãn = 5.88 %)*   Lỗi nhẹ: **0**   Ca chờ lead: **0**  
Quyết định (Release / Hold / Rework): **Rework**  
Lý do (theo luật của phiếu): Có **3 lỗi nặng** (`QC1-02` thiếu `R1` ở `A14, A16` và `QC1-03` gán nhầm `position=L1` cho vạch phải ở `A16`) **và** tỉ lệ lỗi chính đạt **6.16 %** trên tổng 146 nhãn kiểm (**5.88 %** trên 102 nhãn của 6 ảnh bắt buộc), vượt ngưỡng tối đa **5 %** theo thang mức lỗi Road v1.0 → cần trả về **Rework** để sửa các lỗi trùng `position`, bỏ vùng `drivable` tràn làn ngược chiều/lề phải, và sửa `R1` ở `A14, A16`.  

Loại lỗi: bỏ sót = thiếu nhãn phải có; thừa = gán cái không phải đối tượng; sai phạm vi = hình lệch, sai chiều, dừng sai chỗ, tràn vùng. Ba loại này theo cách chia lỗi gán nhãn của ISO/IEC 5259-4 (mục 8.4.2); "sai thuộc tính" và "lỗi file" là khóa học thêm. Cách xếp mức: [thang mức lỗi](docs/qc_severity_road_v1.0.md).
