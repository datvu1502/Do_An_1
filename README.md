# MÔ HÌNH HỒI QUY TUYẾN TÍNH VÀ ỨNG DỤNG TRONG DỰ BÁO
Hồi quy tuyến tính là phương pháp đơn giản nhưng hiệu quả để dự đoán và giải thích
sự biến động của biến đầu ra dựa trên các biến đầu vào. Với tính linh hoạt và khả năng
mô hình hóa các mối quan hệ tuyến tính giữa các biến, phương pháp này đã được sử dụng
rộng rãi trong nhiều lĩnh vực, từ kinh tế, tài chính đến y tế, khoa học xã hội và kỹ thuật.
Việc áp dụng hồi quy tuyến tính cần phải được thực hiện một cách cẩn thận và chính
xác để tránh các sai sót và kết quả không chính xác. Điều này đặc biệt quan trọng trong
các lĩnh vực như y tế và kỹ thuật, khi sự chính xác và độ tin cậy của mô hình có thể ảnh
hưởng đến việc ra quyết định và kết quả của nghiên cứu.

Ở trong nội dung bài báo cáo này chúng ta sẽ đi tìm hiểu các nội dung như tổng quan
về mô hình hồi quy tuyến tính, mô hình hồi quy tuyến tính đơn, đa biến, kiểm tra sự phù
hợp của mô hình hồi quy tuyến tính đa biến và áp dụng mô hình vào việc ứng dụng, giải
quyết bài toán dự báo thực tế.

## THỬ NGHIỆM SỐ
Bộ dữ liệu được sử dụng gồm có các đặc trưng sau:

• Brand: Tên thương hiệu của xe.

• Year: Năm sản xuất xe.

• Kilometers: Tổng số Km mà xe đã đi.

• Fuel: Loại nhiên liệu xe sử dụng.

• Transmission: Loại hộp số xe.

• Ower: Thứ tự chủ sở hữu cũ của xe.

• Mileage: Mức tiêu thụ nhiên liệu.

• Engine: Thể tích xylanh của động cơ.

• Power: Công suất tối đa.

• Seat: Số ghế ngồi của xe.

• Price: Giá bán của xe.

Thực hiện đổi biến năm sản xuất Year thành biến tuổi của xe Ageofcar. Bộ dữ liệu
được sử dụng về giá của các loại xe cũ phổ thông, không dự báo về giá của các loại xe cổ.

# Bước 1: Tiền xử lý dữ liệu
## • Tổng quan về bộ dữ liệu:
![data2](https://github.com/datvu1502/Do_An_1/assets/118582440/edd15f7c-e941-4751-b5d8-efbee87a44b0)


Từ bảng mô tả dữ liệu ở trên ta có thể thấy được:

–	Số lượng hàng có giá trị của các cột khác nhau do xuất hiện các giá trị NULL nên ta cần xử lý mất mát của bộ dữ liệu này.

–	Các cột Brand,Fuel,Owner là các cột có dự liệu không phải dạng số nên ta cần đặt biến giả cho các giá trị trong các cột này.

–	Các cột dữ liệu còn lại là các dữ liệu dạng số.
## •	Xử lý giá trị NULL:
–	Từ thống kê về các giá trị NULL ta thấy các giá trị mất mát không vượt quá 5% của các cột dữ liệu nên ta có thể loại bỏ các giá trị này.
![sumnullnull](https://github.com/datvu1502/Do_An_1/assets/118582440/0409b00a-edc3-47c2-ae38-305fd84da292)


–	Bộ dữ liệu sau khi loại bỏ các giá trị NULL:
![datanull](https://github.com/datvu1502/Do_An_1/assets/118582440/84cd5726-b7e1-4fa6-8920-17e5aa1065cd)



## •	Các điểm ngoại lệ:
Ta sử dụng trực quan các điểm ngoại lệ thông qua biểu đồ boxlpot để xem xét các điểm ngoại lệ ảnh hưởng đến hiệu suất của mô hình.

Dựa trên đồ thị boxplot, ta xác định các giá trị nằm ngoài hai đường thẳng từ hộp đến giá trị cao nhất và thấp nhất trong khoảng biến thiên. Các giá trị này được coi là outlier.
 ![boxplot](https://github.com/datvu1502/Do_An_1/assets/118582440/dc519e0b-df0c-45fb-84bb-d88780235cb2)



Từ đồ thị trên ta thấy các biến Kilometers,Engine,Power,Price,Ageofcar xuất hiện nhiều các điểm ngoại lại, để tránh giảm hiệu suất mô hình dự đoán ta cần loại bỏ các điểm ngoại lệ.
Sau khi loại bỏ outlier bộ dữ liệu còn 3918 hàng.
![dataoutlier](https://github.com/datvu1502/Do_An_1/assets/118582440/c2442121-4d5b-41f3-9b57-ab24b050f6d7)

 

## •	Tạo biến giả:
–	Với mỗi cột có m giá trị, ta cần tạo m-1 biến giả. Giá trị không được tạo biến giả sẽ làm cơ sở.

∗ Cột Brand: giá trị ’Audi’ làm cơ sở, còn lại là biến giả.

∗ Cột Fuel: giá trị ’Diesel’ làm cơ cở.

∗ Cột Transmission: giá trị ’Automatic’ làm cơ sở.

∗ Cột Owner: giá trị ’First’ làm cơ sở.

–	Kết quả:
![biegia](https://github.com/datvu1502/Do_An_1/assets/118582440/5b7a913c-6d36-49ce-8992-e04262fd28aa)


## •	Kiểm tra hiện tượng đa cộng tuyến:

–	Sử dụng ma trận tương quan kiểm tra hiện tượng đa cộng tuyến.

–	Giữa 2 biến độc lập có hệ số tương quan |r| > 0.75 ta sẽ loại bỏ 1 trong 2 biến để tránh hiện tượng đa cộng tuyến. Biến chúng ta đang cần dự đoán là biến Price nên ta sẽ loại bỏ biến độc lập có hệ số tương quan với Price thấp hơn.

–	Ma trận tương quan:
![matrantq](https://github.com/datvu1502/Do_An_1/assets/118582440/62820459-4ba8-4a45-b0e7-256ec4c16526)

–	Ta thấy có 2 cặp biến Power - Engine và Fuel_Diesel - Fuel_Petrol có hệ số tương quan |r| > 0.75. Ta cần loại bỏ 1 trong 2 biến để tránh hiện tượng đa cộng tuyến:

∗ Loại bỏ biến Engine vì biến Engine có hệ số tương quan với biến dự đoán Price thấp hơn so với biến Power.

∗ Tương tự loại biến Fuel_Diesel ra khỏi mô hình.

# Bước 2: Xây dựng mô hình
## •	Xem xét sự phụ thuộc của biến dự báo Price với các biến qua đồ thị phân tán:
 ![ppnew1](https://github.com/datvu1502/Do_An_1/assets/118582440/6834ae5d-d1ce-49cc-a94a-eb6ca48df58d)


=> Ta thấy dữ liệu trong các đồ thị có xu hướng tạo thành một đường cong nên để đảm bảo tính tuyến tính ta sẽ tính giá trị log(Price) để đưa các đồ thị về dạng đường thẳng.

–	Kết quả:
![ppnew2](https://github.com/datvu1502/Do_An_1/assets/118582440/db38ff90-9064-41dd-beb8-2077b1052fa6)

## •	Xây dựng mô hình hồi quy tuyến tính bằng phương pháp bình phương cực tiểu.

–	Ta chia bộ dữ liệu thành 2 phần tập train và test một cách ngẫu nhiên, với tỷ lệ 80% cho tập train và 20% cho tập test.
![train](https://github.com/datvu1502/Do_An_1/assets/118582440/1d018be2-11e9-40a3-a1e7-f865b368d7d2)

–	Xây dựng mô hình bằng phương pháp bình phương cực tiểu-OLS có sẵn trong thư viện statsmodels.api với:
∗ X: ’Kilometers’, ’Mileage’, ’Power’, ’Seats’,’Ageofcar’, ’Brand_BMW’, ’Brand_Ford’, ’Brand_Honda’, ’Brand_Hyundai’, ’Brand_Mahindra’,
’Brand_Maruti’, ’Brand_Mercedes-Benz’, ’Brand_Toyota’, ’Brand_Volkswagen’,

 
’Fuel_LPG’, ’Fuel_Petrol’, ’Transmission_Manual’, ’Owner_Fourth&Above’, ’Owner_Second’, ’Owner_Third’.
∗ Y: ’Price_log’.
 ![OLS1](https://github.com/datvu1502/Do_An_1/assets/118582440/7cae1e5a-5fd9-4398-9d3a-67936d613fb7)


=> Ta thấy giá trị R2 = 0.834 và R2 - hiệu chỉnh = 0.833 nên mô hình của chúng ta khá phù hợp với bộ dữ liệu.
∗ Các hệ số β tương ứng với các biến ước lượng được. Biến phụ thuộc là
log(Price).
 ![heso](https://github.com/datvu1502/Do_An_1/assets/118582440/26e352af-c555-4024-ac70-c9c7f52c0db3)


## •	Kiểm tra sai số của mô hình:
–	Từ mô hình với hệ số β vừa tính được và sử dụng bộ dữ liệu train, ta sẽ đi dự đoán giá của xe. Từ đó ta tính các phần dư theo công thức: 

e = y_train − y_train_predict

–	Trong đó:

∗ y_train: Giá thực tế của bộ dữ liệu train.

∗ y_train_predict: Giá dự đoán của bộ dữ liệu train.

–	Đồ thị phân phối của phần dư:
 
![ppdu](https://github.com/datvu1502/Do_An_1/assets/118582440/29b27637-9c7e-48e2-86b8-f57a9489310b)

=> Ta thấy đồ thị phân phối của e có xấp xỉ với dạng đồ thị phân phối chuẩn.

–	Giá trị kỳ vọng của phần dư:
 ![kyvonge](https://github.com/datvu1502/Do_An_1/assets/118582440/5f166e42-257b-47bd-8473-791fc21231b7)

=> Thỏa mãn giả thiết kỳ vọng sai số = 0

–	Kiểm định White kiểm tra phương sai sai số thay đổi:
 ![white1](https://github.com/datvu1502/Do_An_1/assets/118582440/2acf84d1-e6f9-4511-b76f-faf52343fb72)

=> Ta có: p-value > 0.05 nên thỏa mãn giả thiết phương sai sai số thay đổi.

–	Phương pháp Durbin-Watson kiểm tra hiện tượng tự tương quan:
 ![dw](https://github.com/datvu1502/Do_An_1/assets/118582440/2e61bd2f-6335-47ee-9930-39db37816ee9)

=> Giá trị DW ≈ 2, suy ra mô hình không có sự tự tương quan giữa các phần dư.

Như vậy, mô hình thỏa mãn các giả định cần thiết của phương pháp ước lượng bình phương cực tiểu.

# Bước 3: Đánh giá mô hình
•	Ta sử dụng bộ dữ liệu test để đánh giá mô hình.
•	Từ mô hình với các giá trị β vừa tính được ta sẽ tính giá trị dự báo của bộ dữ liệu test và biểu diễn trên đồ thị:
 ![sosanh](https://github.com/datvu1502/Do_An_1/assets/118582440/b93e5ddb-5511-4ea5-85fe-47931b9d20f1)

•	Trong đó:
–	Trục tung là giá trị dự đoán sử dụng mô hình đã ước lượng trên bộ dữ liệu test.

–	Trục hoành là giá trị thực tế.

–	Đường màu cam là đường y_test = y_test_predict.
![sailech](https://github.com/datvu1502/Do_An_1/assets/118582440/3009bfc2-6907-4e05-b0d4-1adf5377846e)

## •	Nhận xét:

–	Ta thấy mô hình của chúng ta dự đoán khá đúng với các xe có giá ở mức trung bình do các điểm tập trung sát và dày đặc quanh đường thẳng y_test = y_test_predict.

–	Đối với các xe có giá thấp và cao, mô hình có vẻ dự đoán không tốt do các điểm có xu hướng phân tán qua đường y_test = y_test_predict.

## •	Tiến hành xem xét cụ thể qua sai số và tỷ lệ phần trăm sai lệch:
 
– Nhận xét:

∗ Sự chênh lệch lớn nhất là 104,57%, mô hình dự báo giá thấp hơn hơn khoảng 2 lần so với thực tế.

∗ Sự chênh lệch nhỏ nhất là -51,035%, mô hình dự báo giá cao hơn khoảng 1,5 lần so với thực tế.

Sự sai lệch này xuất hiện do một số yếu tố thực tế mà chưa đưa vào mô hình như: thị trường xe cũ, yếu tố cung cầu khi nghiên cứu, giá xe mới, chi phí thuế và một số chi phí khác,...

# Kết luận:
•	Mô hình dự báo giá xe cũ bằng phương pháp bình phương cực tiểu với hệ số xác định R2 = 0.834, khá cao và thỏa mãn các giả thiết mà phương pháp đặt ra .Từ đó cho thấy đây là một mô hình khá phù hợp để dự báo giá xe ô tô cũ.

•	Mô hình có thể đưa thêm một số yếu tố để dự đoán hoặc tăng kích thước mẫu điều tra để cải thiện độ chính xác cả mô hình.



