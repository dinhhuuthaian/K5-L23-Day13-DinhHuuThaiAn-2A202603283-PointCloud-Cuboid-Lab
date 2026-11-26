# Báo cáo Day 13 — Đinh Hữu Thái An, 2A202603283

## 1. Kết luận trước
Mã số: 2A202603283
Họ tên: Dinh Huu Thai An
Task CVAT: D13-2A202603283 · 10 frame: s01f26, s01f57, s02f27, s02f51, s03f13, s03f54, s04f13, s04f59, s05f10, s05f38
Số cuboid: 58 (s01f26 = 10, s01f57 = 6, s03f13 = 7, các frame còn lại = 5). Phiếu tự kiểm còn 9/58 cuboid có cảnh báo (cảnh báo không tính điểm), phần lớn là Car rộng hơn khoảng tham chiếu và một số hộp đáy chưa sát mặt đường.

## 2. Đọc frame (Bước 2)
Hai frame đọc kỹ. Ảnh: `t1-<frame>-3d`, `t1-<frame>-top` (ảnh nhìn từ trên xuống, có đánh dấu phía trước, +x, +y).

| Frame | Phía trước xe ở cạnh nào của ảnh nhìn từ trên xuống; +x, +y chỉ về đâu | Mặt đường (phẳng/dốc; thấp hơn LiDAR ~ m) | Vật xa nhất đọc được (~ m) | Loại vật thấy | Vật phía sau / hai bên | Cụm chưa đọc được |
|---|---|---|---|---|---|---|
| s01f26 | [[cạnh trái của ảnh]]; theo COORDINATES.md phía trước là −y, +x là bên trái, +y là phía sau | z đáy các hộp trong Bảng A dao động −1,55 đến −2,47 m (gần LiDAR khoảng −1,6 đến −1,8 m, xa 20–25 m tới −2,2 đến −2,5 m); mặt đường có vẻ không phẳng hoàn toàn. [[XÁC NHẬN bằng ảnh nhìn ngang mặt đường]] | ≈ 27 m (hộp xa nhất tôi gán nhãn: #7, 27,1 m) | 10 Car | Phía sau (y > 0): #1, #2, #6, #7, #8, #9; sát bên: #4; phía trước: #3, #5, #10 | [[không có]] |
| s01f57 | [[cạnh phải của ảnh]]; theo COORDINATES.md phía trước là −y, +x là bên trái, +y là phía sau | z đáy các hộp ≈ −1,4 đến −1,9 m, nên mặt đường thấp hơn LiDAR khoảng 1,6–1,9 m. [[XÁC NHẬN: phẳng hay dốc]] | ≈ 15,5 m (Cyclist #6, 138 điểm) | 5 Car, 1 Cyclist | Phía sau: #4; sát bên: #3; phía trước: #1, #2, #5, #6 | [[Không có]] |

3 điều **chỉ camera** cho biết: [[ĐIỀN: 1)… 2)… 3)…, lấy từ hai frame trên]]
3 điều **chỉ LiDAR** cho biết: [[ĐIỀN: 1)… 2)… 3)…]]

Tám frame lướt:

| Frame | Phía trước ở cạnh nào của ảnh nhìn từ trên xuống | Điều lạ (nếu có) |
|---|---|---|
| s05f38 | [[nhìn xiên thì phía trước nghiêng về bên phải]] | [[không có]] |
| s01f57 | [[nhìn xiên thì phía trước nghiêng về bên phải]] | [[một số điểm sáng rời rạc lơ lửng phía trên khối nhà cây]] |


## 3. Ba cuboid có hướng dẫn (Bước 3)
Ảnh: `t2-a-car`, `t2-b-bus-truck`, `t2-c-ped-cyclist`.
Các hộp dưới đây là hộp gợi ý từ Bảng A. **Nếu ảnh mẫu của bạn dùng hộp khác thì đổi frame, idx và số cho khớp ảnh.**

| Vật | Frame, idx | Class | Mũi tên yaw đúng hướng? | Đáy chạm đường? | Đã kiểm Top/Side/Front + ảnh? | Kích thước trong bảng 4.3? |
|---|---|---|---|---|---|---|
| (a) xe con gần | s01f57, #3 (3,4 m, 3104 điểm) | Car | yaw 268,0° (cùng chiều xe thu dữ liệu). [[XÁC NHẬN mũi tên chỉ đầu xe trên ảnh camera]] | khoảng hở với mặt đường 0,20 m, z đáy −1,600 m. [[XÁC NHẬN ở Side/Front]] | [[XÁC NHẬN]] | 4,675 × 1,835 × 1,399 m: hợp sedan (3,8–5,0 × 1,70–1,90 × 1,40–1,60); cao 1,399 m, sát cận dưới 1,40 |
| (b) xe buýt hoặc xe tải | s03f13, #4 (16,2 m, 624 điểm) | Truck | yaw 271,2° (cùng chiều). [[XÁC NHẬN]] | khoảng hở 0,03 m, z đáy −2,087 m. [[XÁC NHẬN]] | [[XÁC NHẬN]] | 5,646 × 1,867 × 2,135 m: dài, rộng trong khoảng bán tải (5,2–6,2 × 1,85–2,10); cao 2,135 m vượt khoảng 1,80–2,00, hơi cao hơn tham chiếu |
| (c) người đi bộ hoặc xe hai bánh | s01f57, #6 (15,5 m, 138 điểm) | Cyclist | yaw 272,1° (cùng chiều). [[XÁC NHẬN]] | khoảng hở −0,10 m, z đáy −1,439 m. [[XÁC NHẬN]] | [[XÁC NHẬN]] | 1,733 × 0,644 × 1,816 m: nằm trong khoảng xe đạp có người (1,6–1,9 × 0,50–0,70 × 1,60–1,90) |

Vòng hiệu chuẩn: [[ĐIỀN: cuboid của bạn lệch so với các bạn ở điểm nào, cả lớp chốt cách hiểu guideline nào. Nếu bạn không làm vòng này thì ghi rõ "không tham gia" và lý do.]]

Vật bỏ qua vì không đủ cơ sở: [[ĐIỀN: frame, vị trí, mô tả, loại nghi vấn như UNCERTAIN_CLASS hoặc LOW_VISIBILITY; hoặc ghi "không có"]]

## 4. Bốn hiện tượng chất lượng (Bước 4)
Nguyên nhân ghi là **giả thuyết**. Frame mượn thì ghi rõ nguồn: task chung, hoặc MSSV của bạn cho mượn.

| Hiện tượng | Frame / tên ảnh / nguồn | Nguyên nhân (giả thuyết) | Thấy gì trên point cloud | Hệ quả khi gán (theo guideline) |
|---|---|---|---|---|
| 1. Bóng che | [[frame 6, `t4-1-bong-che`]] | [[xe bus bị che bởi rào]] | [[thấy được nóc xe]] | [[bật occluded, cuboid bao phần suy luận được]] |
| 2. Thưa ở xa | [[frame 8, `t4-2-thua-o-xa`]] | [[car ở xa]] | [[thấy được đuôi xe tự vẽ phần đầu xe]] | [[ thấy khoảng 15–20% thể tích xe]] |
| 3. Phản xạ thấp / ít điểm bất thường | [[frame 2, `t4-3-phan-xa-thap`]] | [[chỉ thấy phần đuôi xe nên thấy ít điểm ]] | [[chỉ thấy được điểm ở đuôi xe]] | [[ thấy khoảng 15–20% thể tích xe]] |
| 4. Điểm lạ | [[frame 2, `t4-4-diem-la`]] | [[nghi ngờ có cycle]] | [[thấy được phần thân người trở lên và 1 phần của xe đạp]] | [[ gán thành cycle]] |

## 5. Số từ cuboid của tôi (Bước 5)
Lấy từ `submission/D13-2A202603283-bangA.csv`; số điểm lấy từ cột `points_in` của `-tukiem.csv`. Mặt đường khoảng −1,7 m: z đáy lệch hơn 0,3 m là lơ lửng hoặc chìm.

| Cuboid (frame, idx, class) | z | h | z đáy = z − h/2 | dist_m | r = √(x²+y²+z²) | yaw_deg | Nhận xét (lơ lửng / chìm / chạm đường) |
|---|---|---|---|---|---|---|---|
| s01f57, #1, Car | −1,006 | 1,678 | −1,845 | 9,63 | 9,68 | 269,7 | chạm đường: lệch 0,15 m so với −1,7 m; khoảng hở −0,05 m |
| s01f57, #4, Car | −0,984 | 1,605 | −1,786 | 6,60 | 6,67 | 274,3 | chạm đường: lệch 0,09 m; khoảng hở 0,01 m |
| s02f51, #3, Car | −1,008 | 1,697 | −1,856 | 22,87 | 22,89 | 266,8 | chạm đường: lệch 0,16 m; khoảng hở 0,11 m |

(a) Cuboid **gần nhất**: s01f57 #3 Car, tâm (2,934; 1,723; −0,901): `dist_m` = 3,40 m, r = 3,52 m. Cuboid **xa nhất**: s05f38 #1 Bus, tâm (2,758; −43,156; 0,078): `dist_m` = 43,24 m, r = 43,24 m (z gần 0 nên r gần bằng dist_m).

(b) Kích thước. Bảng A của tôi không có Pedestrian nên dùng xe hai bánh: s01f57 #6 Cyclist 1,733 × 0,644 × 1,816 m nằm trong khoảng xe đạp có người của bảng 4,3 (1,6–1,9 × 0,50–0,70 × 1,60–1,90); s03f54 #4 Cyclist 1,788 × 0,798 × 1,417 m thì rộng hơn xe đạp (0,70 m) và hơi ngắn hơn xe máy (1,8–2,3 m), nên tôi coi là trường hợp chưa chắc. Xe con: s01f57 #2 Car 4,742 × 1,849 × 1,666 m hợp khoảng SUV (4,4–5,3 × 1,80–2,10 × 1,65–2,10); chiều cao 1,666 m vượt khoảng sedan (1,40–1,60).

(c) Yaw. Xe cùng chiều phía trước: s01f57 #1 có `yaw_deg` 269,7°, gần 270°. Xe ngược chiều: s02f51 #2 (y = −10,8 m) có 91,5°, gần 90°.

Mật độ theo khoảng cách (4 cuboid ở các `dist_m` khác nhau):

| Cuboid (frame, idx, class) | dist_m | Số điểm (`points_in`) |
|---|---|---|
| s01f57, #3, Car | 3,4 | 3104 |
| s02f51, #2, Car | 11,9 | 1208 |
| s02f27, #3, Car | 21,8 | 352 |
| s04f59, #5, Car | 31,7 | 140 |

Quy luật: xa gấp khoảng 1,8 lần (từ 11,9 m lên 21,8 m) thì số điểm còn khoảng 29%, tức giảm 3,4 lần, sát với tỷ lệ nghịch bình phương khoảng cách (1,83² ≈ 3,4). So với đường cong ở slide (xe con: khoảng 1968 điểm ở 0–10 m, 718 ở 10–20 m, 214 ở 20–30 m, 72 ở 30–40 m), số điểm của tôi cao hơn khoảng 1,6–1,9 lần ở mọi dải. Giả thuyết: hộp của tôi hơi dư nên ôm cả điểm lân cận (nhiều Car của tôi rộng 2,2–2,4 m, hơn khoảng 2,10 m của bảng 4,3), hoặc frame của tôi đặc hơn trung vị; tôi chưa kiểm chứng.

Tự kiểm: hai cuboid tôi **đã sửa** sau `preview` / `selfcheck`: [[ĐIỀN: frame, idx, sửa gì]]. Cảnh báo còn lại sau lần `sync` cuối: s01f26 #5 (đáy cao hơn mặt đường 0,47 m), s01f26 #10 (height 1,12 m), s02f27 #2, s02f51 #5, s04f13 #4, s04f13 #5, s05f38 #4, s05f38 #5 (Car rộng hơn 2,3 m), s03f54 #1 (Bus rộng 3,36 m). Lý do giữ nguyên từng cảnh báo: [[ĐIỀN: lý do thật của bạn cho từng cái, hoặc ghi cái nào bạn đã sửa]]


## 6. Ý nghĩa của nhãn, cách dùng AI và điều còn chưa chắc
(a) Nhãn 3D đo bằng mét vì model dùng nó để biết khoảng cách và kích thước thật của vật quanh xe, không phụ thuộc camera hay độ phân giải ảnh như pixel. Vật thưa điểm cần quy tắc riêng vì số điểm giảm theo bình phương khoảng cách, nên nếu mỗi người tự đoán thì nhãn không nhất quán và model sẽ học từ nhãn nhiễu; do đó guideline đặt ngưỡng thấy 15–20% thể tích mới vẽ. [[Viết lại bằng lời của bạn nếu cần]]

(b) Dùng AI: có.
- Công cụ: Claude (claude.ai).
- Câu hỏi chính: hướng dẫn từng bước làm lab, đọc kết quả `sync` và `check_submission`, giải thích quy tắc class, tính các số ở mục 5 từ Bảng A của tôi, và dựng khung báo cáo.
- Cách dùng kết quả: [[ĐIỀN cho đúng thực tế: ví dụ tôi tự vẽ và sửa cuboid, tự đối chiếu số với Bảng A, và tự viết các phần quan sát ở mục 2, 3, 4]]

(c) Điều còn chưa chắc: người đi xe đạp và xe hai bánh (s03f54 #4 rộng 0,798 m, không rõ xe đạp hay xe máy); Bus s03f54 #1 rộng 3,36 m, hơn khoảng 2,5–2,6 m của bảng 4,3 nên hộp có thể dư; nhiều Car rộng 2,2–2,4 m, hơn mức 2,10 m của bảng 4,3; nhiều hộp cùng frame có yaw giống nhau đến 4 chữ số (ví dụ s03f13), nên tôi chưa chắc mình đã căn lại hướng từng hộp; s05f38 #2 có đáy cao hơn mặt đường 0,38 m nhưng không bị cờ. [[Xem lại từng ý trong CVAT, bỏ ý nào bạn đã kiểm tra và thấy không đúng, thêm ý của bạn]]
