# 10 Câu hỏi phỏng vấn thường gặp trong ngành Machine Learning (Học Máy)
## 1.Tại sao chúng ta cần một validation set and test set? Sự khác biệt của chúng là gì?
**Khi tranining một model, chúng ta chia dữ liệu có sẵn thành ba bộ riêng biệt:**
- Traning dataset được sử dụng để phù hợp với các thông số của model. Tuy nhiên, độ chính xác mà chúng tôi đạt được trên Training Set là không đáng tin cậy để dự đoán nếu model cũng sẽ chính xác trên sample mới.
- Validation Dataset được sử dụng để đo lường mức độ hiệu quả của models trên các ví dụ không phải là một phần của Training dataset. Các số liệu được tính toán trên Validation dataset có thể được sử dụng để điều chỉnh các hyperparameters của model. Tuy nhiên, mỗi khi chúng ta đánh giá Validation dataset và chúng ta đưa ra quyết định dựa trên những điểm số đo, chúng ta leaking thông tin từ Validation dataset vào model. Các đánh giá nhiều hơn, càng có nhiều thông tin bị leaking. Vì vậy, chúng ta có thể kết thúc việc ghi đè lên Validation dataset và một lần nữa, validation score sẽ không đáng tin cậy để dự đoán hành vi của model trong thế giới thực.
- Test dataset được sử dụng để đo lường mức độ hiệu quả của model trên các ví dụ không nhìn thấy trước đó. Nó chỉ nên được sử dụng khi chúng tôi đã điều chỉnh các thông số bằng cách sử dụng validation set

Vì vậy, nếu chúng ta bỏ qua test set và chỉ sử dụng validation set, validation score sẽ không phải là ước tính tốt cho việc khái quát hoá model.
