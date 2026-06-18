## DỰ ĐOÁN GIÁ NHÀ

Đây là repo mình làm để thực hành các bước cơ bản nhất khi tiếp cận một bài toán Machine Learning. Dữ liệu dược sử dụng là giá nhà ở Mỹ: [nguồn](https://huggingface.co/datasets/GihanPramod99/House_Price/tree/main)

## Thành phần của Repo
* `USA_Housing_Dataset.csv`: File dữ liệu gốc.
* `Housing_Price_Prediction.ipynb`: File code Jupyter Notebook.
* `README.md`: Note

## Quá trình làm
Mục tiêu là chạy thử mô hình Ridge Regression với tập dữ liệu mình lấy trên Internet. Đây là những gì mình đã làm

1. **Dọn rác dữ liệu:** Xóa những căn nhà bị lỗi nhập giá bằng $0, lọc các dữ liệu có số âm. Do không có dữ liệu nào là `null` nên không dọn hay xử lý các trường hợp thiếu dữ liệu `null`
2. **Định dạng lại feature:** Cột `yr_renovated` là năm trùng tu lại của căn nhà có dạng là 0 nếu như chưa tùng được sửa sang lại, là năm nếu như nó đã được tu sửa. Nếu để không thì mình nhận thấy sẽ có căn "sửa vào năm 0" và có căn sửa vào 2000s, thứ mà trông khá là vô lý. Mình đã đặt là 1 nếu đã từng được sửa và 0 nếu chưa từng.
3. **Huấn luyện:** Ép standard scale dữ liệu cho đều nhau rồi đẩy vào mô hình Ridge Regression.

## Kết quả
Mô hình hiện tại có điểm R2 là khoảng **53%**, trung bình mỗi căn đoán lệch cỡ **$150k**. Sai số to có thể là do:

* **Dữ liệu nhiễu (Outliers):** Có những căn nhà giá rất cao so với trung bình giá nhà của cả tập dữ liệu. Ridge Regression rất nhạy cảm với các giá trị ngoại lai này.
* **Feature chưa đủ:** Tất cả các feature được dùng để train đều là dưới dạng số, chưa quan tâm tới các yếu tố như vị trí, tính chất, .... Kiểu như nhà mặt đường và nhà trong ngõ ấy, nhà thành phố và nhà nông thôn, ... Việc chỉ chọn các đặc trưng số hiện tại làm cho mô hình chỉ dựa vào số chứ không dựa vào tình hình thực tế

## Hướng đi có thể thử
- Thử mô hình khác
- Mã hóa cả các Feature không có dạng số
- Loại bỏ đi các phần tử ngoại lai