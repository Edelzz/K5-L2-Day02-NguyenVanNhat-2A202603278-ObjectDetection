# Mini guideline — bài làm cá nhân

> Điền nội dung này trước khi bắt đầu gán nhãn. Giữ lại các quyết định sau khi self-QC.

## Định nghĩa lớp

| Lớp | Định nghĩa của bạn | Ví dụ/điểm phân biệt |
| --- | --- | --- |
| `car` |Thiết kế chủ yếu để chở người.Thân xe thấp hoặc có dáng SUV cao vừa phải.
Khoang hành khách và khoang hành lý kiểu xe con.|Xe con, sedan, SUV, taxi |
| `truck` |Thiết kế chủ yếu để vận chuyển hàng hóa.Có cabin và thùng chở hàng riêng biệt. Có thể có thùng kín, thùng mui bạt hoặc thùng hở.	 | Xe tải, xe đầu kéo, xe bán tải|
| `bus` |Thiết kế chủ yếu để chở nhiều hành khách. Có nhiều cửa sổ lớn dọc thân xe. Có nhiều hàng ghế và cửa lên xuống dành cho hành khách. |Xe buýt, minibus chở khách |
| `van` |Thân xe dạng hộp, tương đối cao. Khoang cabin và khoang phía sau thường liền thành một thân xe. |Xe van, minivan |

## Quy tắc chung

- Box bám sát vật thể nghĩa là: Box phải ôm sát phần thân xe nhìn thấy được, không lấy thừa phần mặt đường, bầu trời hoặc xe bên cạnh.

- Vật thể bị che khuất: Vẫn gán nhãn nếu có thể nhận diện được loại xe. Bounding box chỉ bao quanh phần xe nhìn thấy được.

- Vật thể bị cắt bởi rìa ảnh: Vẫn gán nhãn nếu nhận diện được loại xe. Box kéo đến đúng rìa ảnh, không tự đoán hoặc vẽ thêm phần xe nằm ngoài khung hình.

- Vật thể rất nhỏ/mơ hồ: Nếu xe quá nhỏ hoặc chỉ còn một phần rất nhỏ khiến không thể xác định chắc chắn class (car, truck, bus, van), không tự đoán nhãn. Ghi lại tên ảnh và trường hợp đó để hỏi giảng viên.
## Ghi lại quyết định cho ít nhất ba ca mơ hồ

| Ảnh | Tình huống | Quyết định cuối | Lý do theo schema |
| --- | --- | --- | --- |
| `drive_175` |xe bị che còn phần thân sau xe | Là car |Hình dáng và đặc điểm cửa sổ phù hợp với xe car. |
| `drive_199` | xe bị che hầu hết chỉ còn phần thân sau xe  | là car | hình dáng phù hợp với xe car |
| `drive_568` |xe nhỏ, mơ hồ, bị che chỉ còn phần thân sau xe | là car |hình dáng phù hợp với xe car |
