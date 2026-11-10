# Báo cáo cá nhân — Ngày 2 Object Detection

Đổi tên file theo `MSSV_HoTen.md`, ví dụ `20241234_NguyenVanAn.md`. Điền kết quả thật, xóa dòng hướng dẫn khi nộp. Xem [quy định nộp](../../SUBMISSION.md).

## 1. Thông tin học viên

- Họ tên: NGUYỄN VĂN NHẤT
- MSSV:2A202603278
- Email:nhatnvedelz@gmail.com
- Lớp:L2B
- Link repo bài làm:https://github.com/Edelzz/K5-L2-Day02-NguyenVanNhat-2A202603278-ObjectDetection.git
- Link Colab đã chạy:https://colab.research.google.com/drive/1bUZLwRaWsx8TrGwCbdqaRVNaPXmguJ4H?usp=sharing

## 2. Schema và mini guideline

Dẫn tới [GUIDELINE_MINI.md](../../GUIDELINE_MINI.md). Tóm tắt ba ca mơ hồ đã quyết định, cách áp dụng schema và phần cần giảng viên làm rõ.

## 3. Annotation và self-QC

- Số file nhãn train: 50
- Kết quả checker và lỗi đã xử lý: 50
- Danh sách ít nhất 10 ảnh đã rà bằng mắt: driver_001 đến driver_050
- Lỗi bỏ sót/box/class phát hiện khi rà và cách sửa: drive_003, drive_009, drive_024
- Commit khóa nhãn ban đầu:

## 4. Gold QC và rework

| Chỉ số | Trước sửa | Sau sửa nếu có |
|---|---:|---:|
| TP |424 | |
| FP |341 | |
| FN |229 | |
| Precision | 0.5542| |
| Recall |0.6493 | |
| F1 |0.5980 | |
| mean_iou_of_matches |0.7642 | |
| passed |false | |

Dẫn tới `outputs/annotation_evaluation.json` trong repo. Nếu rework, ghi ảnh, lỗi đã kiểm, quyết định sửa/giữ và lý do. Không suy nguyên nhân chỉ từ FP/FN. Không có rework thì ghi rõ.

## 5. Kết quả YOLO

- Runtime, GPU/CPU, phiên bản Ultralytics và Torch: cpu, Ultralytics YOLO Detection 1.0
- Các tham số thay đổi so với notebook nếu có và lý do:
- Đường dẫn best checkpoint trong phiên chạy:"/content/Day2-Lab/outputs/yolo26_runs/vehicle_annotation/weights/best.pt"

| Chỉ số trên 10 ảnh eval | Giá trị |
|---|---:|
| Precision |0.46652254072571203 |
| Recall |0.23643109791845476 |
| mAP50 |0.27956654462639946 |
| mAP50–95 | 0.20491882437741812|

Đặt cả 2 folder `assets/eval_predictions/` và `assets/yolo26_runs/` (giải nén từ `day2_colab_outputs.zip`) cạnh báo cáo và dẫn link tương đối. Không chỉ ghi số; chỉ ra ít nhất một ảnh và vật thể cụ thể.

Trả lời bốn câu hỏi cuối notebook:

1. Lớp nào recall thấp nhất? Ảnh nào minh họa? 
# Lớp bus có recall thấp nhất
2. Nếu mAP50 cao nhưng mAP50–95 thấp, cần kiểm điều gì trên box?
# Cần kiểm tra độ khít và vị trí bounding box: box có quá rộng/quá hẹp không, có lệch khỏi thân xe không, có bao gồm nền hoặc vật thể bên cạnh không, và các cạnh box có bám đúng biên vật thể không. mAP50 chỉ yêu cầu mức IoU thấp hơn; mAP50–95 đánh giá ở nhiều ngưỡng IoU nghiêm ngặt hơn nên nhạy hơn với sai lệch tọa độ.
3. Lỗi class nào có thể liên quan guideline? Dữ kiện nào hỗ trợ nhận xét? 
# Nhầm lẫn car–`van` là một vấn đề cần rà soát. Ví dụ cụ thể drive_051.jpg có một xe con màu đỏ ở tiền cảnh được dự đoán van 0.95, trong khi hình dáng quan sát được nghiêng về car.
4. Vì sao không dùng 10 ảnh eval để train? Vai trò validation của chúng trong notebook là gì?
# Không dùng eval để train để giữ dữ liệu đánh giá tách khỏi quá trình cập nhật trọng số, tránh rò rỉ dữ liệu và giữ phép đánh giá có ý nghĩa.Theo luồng notebook của bài, 10 ảnh eval được dùng làm validation để theo dõi/so sánh kết quả và lựa chọn checkpoint phù hợp; vì vậy không nên dùng chính các ảnh này làm dữ liệu huấn luyện.

## 6. Khó khăn và cách xử lý

| Bước/thời điểm | Lỗi quan sát | Cách đã thử | Kết quả/còn thiếu |
|---|---|---|---|
| Gold QC |	F1 = 0.5980 thấp hơn ngưỡng 0.80; Precision = 0.5542; Recall = 0.6493 |Đọc thống kê evaluator và xác định các ảnh cần ưu tiên mở kiểm tra |Mean IoU = 0.7642 đạt ngưỡng; cần rà ảnh, xác định nguyên nhân từng mismatch và chạy evaluator lại sau rework |

## 7. Tự đánh giá theo rubric

Đối chiếu [RUBRIC.md](../../RUBRIC.md): phần nào đã có kết quả, phần nào còn thiếu hoặc chưa kiểm được. Không tự nhận hoàn thành bước chưa chạy.
Chưa đạt ngưỡng F1 theo JSON (0.5980 < 0.80); mean IoU đạt ngưỡng (0.7642 ≥ 0.70).

## 8. Công cụ AI và tài liệu tham khảo

ChatGPT: hỗ trợ giải thích schema car/truck/bus/van, diễn đạt quy tắc trong GUIDELINE_MINI.md, giải thích cách ghi “lý do theo schema” và hỗ trợ tạo bản nhãn dự thảo cho ảnh drive_001 và hướng dẫn trả lời kết quả notebook
