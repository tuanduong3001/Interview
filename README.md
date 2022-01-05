# 10 Câu hỏi phỏng vấn thường gặp trong ngành Machine Learning (Học Máy)
## 1. Tại sao chúng ta cần một validation set and test set? Sự khác biệt của chúng là gì?
**Khi tranining một model, chúng ta chia dữ liệu có sẵn thành ba bộ riêng biệt:**
- Traning dataset được sử dụng để phù hợp với các thông số của model. Tuy nhiên, độ chính xác mà chúng tôi đạt được trên Training Set là không đáng tin cậy để dự đoán nếu model cũng sẽ chính xác trên sample mới.
- Validation Dataset được sử dụng để đo lường mức độ hiệu quả của models trên các ví dụ không phải là một phần của Training dataset. Các số liệu được tính toán trên Validation dataset có thể được sử dụng để điều chỉnh các hyperparameters của model. Tuy nhiên, mỗi khi chúng ta đánh giá Validation dataset và chúng ta đưa ra quyết định dựa trên những điểm số đó, chúng ta leaking thông tin từ Validation dataset vào model. Càng đánh giá nhiều hơn, càng có nhiều thông tin bị leaking. Vì vậy, chúng ta có thể kết thúc việc ghi đè lên Validation dataset và một lần nữa, validation score sẽ không đáng tin cậy để dự đoán hành vi của model trong thế giới thực.
- Test dataset được sử dụng để đo lường mức độ hiệu quả của model trên các ví dụ không nhìn thấy trước đó. Nó chỉ nên được sử dụng khi chúng tôi đã điều chỉnh các thông số bằng cách sử dụng validation set

Vì vậy, nếu chúng ta bỏ qua test set và chỉ sử dụng validation set, validation score sẽ không phải là ước tính tốt cho việc khái quát hoá model.
## 2. Stratified cross-validation là gì và khi nào chúng ta nên sử dụng nó?
Cross-validation là một kỹ thuật để chia dữ liệu giữa các training set và validation sets. Trên mỗi Cross-validation điển hình, việc chia tách này được thực hiện ngẫu nhiên. Tuy nhiên, trong Stratified cross-validation, sự phân chia tỷ lệ của các categories trên cả training và validation datasets.

Ví dụ, nếu chúng tra có một tập dữ liệu với 10% của loại A và 90% của loại B, và chúng tôi sử dụng stratified cross-validation, chúng tôi sẽ có tỷ lệ tương tự training và validation. Ngược lại, nếu chúng ta sử dụng cross-validation đơn giản, trong trường hợp xấu nhất, chúng ta có thể thấy rằng không có mẫu nào của loại A trong validation set.

**Có thể áp dụng  stratified cross-validation trong các trường hợp sau:**
- Trên dataset có nhiều categories. Các Dataset càng nhỏ và càng mất cân đối giữa các Categories thì nên sử dụng stratified cross-validation.
- Trên dataset với data phân chia khác nhau. Ví dụ: trong dataset để điều khiển tự động, chúng tôi có thể chụp ảnh vào ban ngày và ban đêm. Nếu chúng tôi không đảm bảo rằng cả hai loại đều xuất hiện trong training và validation, thì sẽ nảy sinh một số vấn đề chung khác.

## 3. Tại sao ensembles thường có điểm số cao hơn các model riêng lẻ?
Ensembles là sự kết hợp của nhiều models để tạo ra một dự đoán duy nhất. Ý tưởng chính để đưa ra dự đoán tốt hơn là các models nên tạo ra các lỗi khác nhau. Bằng cách đó, các lỗi của một model sẽ được bù đắp bằng các dự đoán đúng của các models khác và do đó số điểm của ensembles sẽ cao hơn.
**Chúng ta cần các models đa dạng để tạo ra một ensembles. Sự đa dang có thể đạt được bằng cách:**
- Sự dụng các thuật toán ML khác nhau. Ví dụ: bạn có thể kết hợp logistic regression, knn và decision trees.
- Sử dụng các tập con khác nhau data for training, hay còn được gọi là bagging
- Đưa ra một trọng lượng khác nhau cho mỗi sample training set. Nếu điều này được thực hiện lặp đi lặp lại, hãy kiểm tra trọng lượng của các samples thông qua lỗi ensembles, hay còn gọi là boosting.

## 4. Regularization là gì? Bạn có thể đưa ra một số ví dụ về kỹ thuật regularization không?
Regulazition, một cách cơ bản, là thay đổi mô hình một chút để tránh overfitting trong khi vẫn giữ được tính tổng quát của nó (tính tổng quát là tính mô tả được nhiều dữ liệu, trong cả tập training và test). Một cách cụ thể hơn, ta sẽ tìm cách di chuyển nghiệm của bài toán tối ưu hàm mất mát tới một điểm gần nó. Hướng di chuyển sẽ là hướng làm cho mô hình ít phức tạp hơn mặc dù giá trị của hàm mất mát có tăng lên một chút.

**Một số kỹ thuật Regularization:**
- L1 cố gắng giảm thiểu absolute value của các parameters trong models. Nó tạo ra sparse parameters.
- L2 cố gắng giảm thiểu square value của các parameters trong models. Nó tạo ra các parameters với small values.
- Dropout là một kỹ thuật được áp dụng cho các neural networks được đặt một cách ngẫu nhiên và cho ra kết quả đầu ra của các neurons bằng 0 trong quá trình training.
- Early stopping sẽ dừng training khi validation score ngừng cải thiện, ngay cả khi training score có thể được cải thiện. Điều này giúp ngăn chặn overfitting trên training dataset.

## 5. Dimensionality reduction là gì? Có cách nào giảm tải tính toán nhưng vẫn giữ được độ chính xác?
Một kỹ thuật khác cùng hướng tiếp cận unsupervised learning đó là giảm số chiều (dimemsionality reduction). Dimensionality reduction là một cách để đơn giản hoá dữ liệu, giúp dữ liệu dễ trao đổi, tính toán nhanh hơn và dễ lưu trữ hơn.

Về mặt ý tưởng, dimensionality reduction nhằm mô tả dữ liệu ngắn gọn hơn. Ví dụ như điểm GPA. Để đánh giá một sinh viên trong quá trình học, ta cần biết hàng chục lớp học sinh viên đó tham gia, hàng trăm bài kiểm tra và hàng ngàn bài tập mà sinh viên đó đã làm. Mỗi bài kiểm tra sẽ cho biết sinhh viên này hiểu được nội dung bài giảng đến đâu. Nhưng đối với nhà tuyển dụng việc đọc hết các điểm số này là quá sức. May mắn thay, ta có thể tổng hợp điểm số lại bằng cách lấy trung bình. Ta không cần quan tâm đến hàng đống điểm vừa rồi mà chỉ cần quan sát điểm GPA để đánh giá lực học của sinh viên đó. 

## 6. Imbalanced dataset là gì? Liệt kê một số cách để đối phó với nó?
Imbalanced dataset là tập dữ liệu có tỷ lệ các categories khác nhau. Ví dụ, một tập dữ liệu với các hình ảnh y tế mà chúng ta phát hiện trong một số bệnh thường sẽ có nhiều mẫu âm tính hơn dương tính, ví dụ: 98% hình ảnh không có bệnh và 2% hình ảnh bị bệnh.

**Có các tuỳ chọn khác nhau để xử lý các imbalanced dataset:**
- Oversampling hoặc undersampling
- Data augmentation. Chúng ta có thể thêm data vào các categories ít thường xuyên hơn bằng cách sửa đổi data hiện có theo cách được kiểm soát. Trong dataset mẫu, chúng ta có thể lật hình ảnh bị bệnh hoặc thêm nhiễu vào bản sao của hình ảnh theo cách mà bệnh vẫn có thể nhìn thấy được.
- Sử dụng các metrics thích hợp. Trong dataset mẫu, nếu chúng ta có một model luôn đưa ra các dự đoán tiêu cực, nó sẽ đạt được độ chính xác 98%. Ngoài ra còn có các metrics khác như độ chính xác, số lần truy cập và F-score để mô tả độ chính xác của một model tốt hơn khi sử dụng imbalanced dataset.

## 7. Giải thích được sự khác biệt giữa supervised, unsupervised và reinforcement learning?
**Supervised learning** là thuật toán dự đoán đầu ra (outcome) của một dữ liệu mới (new input) dựa trên các cặp (input, outcome) đã biết từ trước. Cặp dữ liệu này còn được gọi là (data, label), tức (dữ liệu, nhãn). Trong Supervised learning, chúng ta train một model để tìm hiểu về mối quan hệ giữa input và output data. Chúng ta cần có label data để có thể thực hiện được quá trình supervised learning.

Với **Unsupervised learning**, chúng ta chỉ có unlabeled data. Thuật toán unsupervised learning sẽ dựa vào cấu trúc của dữ liệu để thực hiện một công việc nào đó, ví dụ như phân nhóm (clustering) hoặc giảm số chiều của dữ liệu (dimension reduction) để thuận tiện trong việc lưu trữ và tính toán. Unsupervised learning thường được sử dụng để khởi tạo các parameters của model khi chúng ta có rất nhiều unlabeled data và một phần nhỏ labeled data. Trước tiên, chúng ta train một Unsupervised Models và sau đó chúng ta sử dụng trọng số của models để train một supervised model.

Trong **reinforcement learning**, model có một số input data và phần thưởng tuỳ thuộc vào output của model. Reinforcement learning là các bài toán giúp cho một hệ thống tự động xác định hành vi dựa trên hoàn cảnh để đạt được lợi ích cao nhất (maximizing the performance). Hiện tại, Reinforcement learning chủ yếu được áp dụng vào Lý Thuyết Trò Chơi (Game Theory), các thuật toán cần xác định nước đi tiếp theo để đạt được điểm số cao nhất. 
