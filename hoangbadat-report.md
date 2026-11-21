# Báo cáo cá nhân — Ngày 11
Họ tên: Hoàng Bá Đạt               Mã học viên: 2A202603100  
Phiên bản CVAT (Help → About): v2.82.0  
Guideline: Road v1.0               Lần nộp (`revision` trong manifest): 1  
Thời điểm export (ngày giờ trên CVAT): 2026-11-21    Số lần nộp lại sau Rework: 0  

## 1. Kiểm project
| Mục | Đúng như guideline Road v1.0? | Ghi chú |
| --- | --- | --- |
| 6 label, đúng kiểu | ĐÚNG | lane (polyline), road_curb (polyline), crosswalk (polygon), drivable (polygon), traffic_light (rectangle), traffic_sign (rectangle) |
| Thuộc tính và giá trị | ĐÚNG | Đầy đủ select attributes và checkbox edge_zone đúng taxonomy Road v1.0 |
| 4 tag ảnh | ĐÚNG | camera, timeofday, weather, source (mỗi tag có select attribute value) |
Cách kết thúc polyline trên bản CVAT này: Nhấn phím N trên bàn phím.  
Cách đặt tag ảnh trên bản CVAT này: Bấm công cụ Setup tag ở thanh bên trái, chọn từng tag rồi bấm +, sau đó mở Details ở bảng Objects bên phải để chọn giá trị value.  

## 2. Số lượng đã gán
| Task | Ảnh | lane | road_curb | crosswalk | drivable | traffic_light | traffic_sign |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| front | 12 | 28 | 2 | 4 | 19 | 18 | 20 |
| front-extra (đã làm __ / 4) | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| fisheye | 8 | 3 | 3 | 7 | 8 | 2 | 3 |
| fisheye-extra (đã làm __ / 4) | 0 | 0 | 0 | 0 | 0 | 0 | 0 |

## 3. Bảng ca khó
| Ảnh | Nhãn | Phân vân giữa | Đã chọn | Lý do |
| --- | --- | --- | --- | --- |
| A05 | lane | Vẽ hay không vẽ L1/R1 | Không vẽ L1/R1, vẽ road_curb | Đường trong phố hẹp hai bên xe đỗ, không có vạch sơn kẻ đường |
| A06 | lane | Thiếu R1 bên phải | Không vẽ R1 | Mép phải đường là bó vỉa hè dưới chân dầm cầu, không có vạch sơn |
| B06 | lane | position L1/R1 hay other | other | Camera sườn xe (MVL) không có làn xe tiến tới, quy tắc bắt buộc position = other |
| B01, B04, B05, B08 | crosswalk | lane hay crosswalk | crosswalk | Vạch ngựa vằn qua đường vẽ bằng 1 polygon bao trùm, không kẻ từng vạch bằng lane |

## 4. Phiếu QC 1 nhận được
Bạn kiểm lô của tôi: Đào Duy Hiếu  Quyết định nhận được: Release  
| Mã lỗi | Số lỗi | Đồng ý? | Đã sửa? |
| --- | ---: | --- | --- |
| Không có lỗi nặng | 0 | Đồng ý | Đã hoàn thiện |

## 5. Kiểm file export
| File | Mở lại được? | Số shape ảnh 1 (job / file) | Số shape ảnh 2 (job / file) | Tag camera có trong XML? |
| --- | --- | --- | --- | --- |
| hoangbadat-front.zip | CÓ | 8 / 8 | 5 / 5 | CÓ (front) |
| hoangbadat-fisheye.zip | CÓ | 3 / 3 | 4 / 4 | CÓ (fisheye_front, fisheye_rear, fisheye_left, fisheye_right) |

## 6. Ảnh chụp màn hình
1. Tab Labels của project: Có đủ 6 label và 4 tag.
2. Một ảnh camera trước đã gán đủ (làn, vùng lái, đèn/biển): Ảnh A01 (đủ 4 vạch lane, vùng lái direct/alternative, biển báo xanh).
3. Một ảnh fisheye đã gán, phóng to đoạn polyline cong: Ảnh B08 (vùng lái né thân xe, vạch người đi bộ crosswalk).
4. Một đoạn XML có `<polyline label="lane">`: `annotations.xml` trong file `hoangbadat-front.zip`.

## 7. Tự đánh giá
Lỗi bạn mắc nhiều nhất hôm nay (theo mã QC1-xx), và cách tránh ở Ngày 20:  
- Chiều vẽ polyline vạch làn: ban đầu vẽ từ trên xuống dưới (ngược chiều quy tắc gần ra xa). Cách tránh: luôn chấm điểm đầu tiên ở mép dưới ảnh (gần xe nhất) rồi mới đi dần ra xa.
- Tag camera ảnh fisheye: cần luôn đối chiếu hậu tố tên file (`_FV`, `_RV`, `_MVL`, `_MVR`) trước khi bắt đầu gán.
Nhãn của bạn đi vào model ở đâu? Chọn một lỗi đã sửa và nói nó làm model học sai thế nào:  
- Nếu gán nhầm vạch sườn xe thành L1/R1 trên camera fisheye sườn, model phát hiện làn xe (Lane Keeping Assist) sẽ hiểu nhầm xe đang chạy ngang và đưa ra góc lái sai lệch gây nguy hiểm.
