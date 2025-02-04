## Khái niệm Prompt Chaining
Prompt Chaining là kỹ thuật chia nhỏ một tác vụ phức tạp thành một chuỗi các bước nhỏ, mỗi bước được giải quyết thông qua một prompt riêng biệt. Quá trình này có nghĩa là kết quả đầu ra của prompt ở bước trước sẽ được sử dụng làm đầu vào cho bước tiếp theo.

## Đặc điểm chính:
* Chia nhỏ nhiệm vụ: Thay vì yêu cầu mô hình thực hiện toàn bộ nhiệm vụ trong một lần (một prompt “to” duy nhất), prompt chaining giúp chia nhỏ vấn đề thành nhiều bước như: soạn thảo, phản biện và tinh chỉnh.
* Tăng tính kiểm soát: Mỗi bước được thiết lập riêng, cho phép người dùng kiểm soát tốt hơn quá trình xử lý và điều chỉnh từng phần nếu cần.

Ví dụ thực tế: Trong một nhiệm vụ tóm tắt văn bản, bạn có thể yêu cầu mô hình tạo ra một bản tóm tắt sơ khởi, sau đó yêu cầu nó cung cấp phản hồi (phản biện) về bản tóm tắt đó và cuối cùng tinh chỉnh lại bản tóm tắt dựa trên phản hồi đó.

## Lợi ích:
* Giúp mô hình tập trung tốt hơn vào từng phần của nhiệm vụ.
* Cho phép dễ dàng điều chỉnh và cải thiện từng bước dựa trên phản hồi cụ thể từ mô hình.
* Thường mang lại kết quả chất lượng cao hơn, đặc biệt với các tác vụ đòi hỏi suy luận nhiều bước.

Prompt ví dụ:
* Hãy áp dụng phương pháp prompt chaining để cho công việc Phát triển chatbot và tác nhân AI hỗ trợ các công đoạn từ định nghĩa yêu cầu cho đến system test của dự án phát triển phần mềm

## HƯỚNG DẪN PROMPT TỪNG BƯỚC:
### Bước 1: Xác định yêu cầu và mục tiêu của dự án ERP
Prompt 1:

*“Với vai trò là chuyên gia phân tích nghiệp vụ ERP, hãy liệt kê và mô tả chi tiết các yêu cầu chức năng và phi chức năng cần có cho chatbot và tác nhân AI hỗ trợ dự án ERP. Bao gồm các giai đoạn: định nghĩa yêu cầu, thiết kế, triển khai, kiểm thử và bảo trì. Phân loại các yêu cầu thành:
Yêu cầu về hỗ trợ người dùng (ví dụ: hướng dẫn sử dụng module ERP, giải đáp thắc mắc về quy trình nghiệp vụ).
Yêu cầu về tích hợp hệ thống (kết nối với các module ERP như kế toán, quản lý kho, bán hàng,…).
Yêu cầu hiệu năng và bảo mật.”*

Đầu ra mong đợi:

Danh sách chi tiết các yêu cầu của hệ thống ERP được phân chia theo nhóm như:
* Hỗ trợ người dùng: Chatbot cần có khả năng giải đáp thắc mắc về quy trình đặt hàng, báo cáo tài chính, kiểm tra tồn kho,…
* Tích hợp: Hỗ trợ truy xuất dữ liệu từ các module ERP khác nhau (kế toán, nhân sự, sản xuất, v.v.) thông qua API.
* Hiệu năng & Bảo mật: Phản hồi nhanh (ví dụ dưới 1 giây), khả năng xử lý đồng thời nhiều yêu cầu và bảo mật dữ liệu khách hàng, thông tin kinh doanh.

### Bước 2: Xây dựng luồng hội thoại và kịch bản tương tác
Prompt 2 (dựa trên kết quả bước 1):

*“Dựa trên danh sách yêu cầu ở Bước 1, hãy tạo ra các kịch bản hội thoại mẫu cho chatbot ERP. Mỗi kịch bản cần bao gồm:
Đầu vào của người dùng (ví dụ: ‘Làm sao để tạo đơn hàng mới trong hệ thống ERP?’).
Phản hồi của chatbot với các bước hướng dẫn cụ thể (ví dụ: ‘Để tạo đơn hàng mới, hãy truy cập vào module bán hàng, nhấp vào “Tạo đơn hàng”, điền thông tin cần thiết…’).
Các tình huống ngoại lệ (ví dụ: ‘Nếu đơn hàng bị lỗi, làm thế nào để chỉnh sửa?’).”*

Đầu ra mong đợi:
* Một tập hợp các kịch bản hội thoại mẫu, với các bước rõ ràng và logic, giúp định hướng người dùng trong quy trình sử dụng ERP.

### Bước 3: Xác định nguồn dữ liệu đào tạo và tạo bộ dữ liệu mẫu
Prompt 3 (dựa trên kết quả bước 2):

“Hãy liệt kê các nguồn tài liệu nội bộ ERP (tài liệu hướng dẫn, SOP, báo cáo, FAQ, …) mà chatbot cần học để đưa ra các phản hồi chính xác. Sau đó, tạo ra một bộ dữ liệu mẫu gồm các cặp câu hỏi – trả lời cho các tình huống được mô tả ở bước 2.”

Đầu ra mong đợi:
* Danh sách các nguồn tài liệu đào tạo kèm theo một tập hợp các cặp Q&A mẫu, ví dụ:
 * Q: “Làm sao để tạo đơn hàng mới?”
 * A: “Bạn hãy truy cập vào module bán hàng, chọn ‘Tạo đơn hàng’, sau đó điền thông tin khách hàng, sản phẩm, số lượng… và nhấn ‘Lưu’.”

### Bước 4: Xây dựng kiến trúc hệ thống và luồng xử lý của chatbot ERP
Prompt 4 (dựa trên kết quả bước 3):

*“Hãy mô tả kiến trúc hệ thống cho chatbot và tác nhân AI trong dự án ERP. Bao gồm các thành phần chính như:
Giao diện người dùng (chat window tích hợp trên hệ thống ERP hoặc web portal).
Bộ xử lý ngôn ngữ tự nhiên (NLP) để hiểu yêu cầu người dùng.
Mô hình trả lời (response engine) dựa trên dữ liệu đào tạo đã được xây dựng.
Các API kết nối với các module ERP (kế toán, kho, bán hàng,…).
Bộ lưu trữ lịch sử hội thoại và xử lý trạng thái.”*

Đầu ra mong đợi:
* Một sơ đồ kiến trúc hoặc mô tả chi tiết về luồng xử lý từ lúc người dùng gửi yêu cầu đến khi nhận phản hồi từ chatbot, giải thích cách các thành phần (NLP, API, hệ thống lưu trữ) hoạt động phối hợp.

### Bước 5: Triển khai prototype và tích hợp với hệ thống ERP trong môi trường thử nghiệm
Prompt 5 (dựa trên kết quả bước 4):

*“Hãy mô tả quy trình triển khai prototype của chatbot ERP vào môi trường thử nghiệm (staging environment). Bao gồm các bước:
Tích hợp chatbot với các API của hệ thống ERP.
Cấu hình giao diện và xác định quyền truy cập của người dùng.
Kiểm thử giao diện và phản hồi của chatbot với các tình huống thực tế.
Thu thập phản hồi từ người dùng thử và điều chỉnh.”*

Đầu ra mong đợi:
* Quy trình triển khai chi tiết, nêu rõ các bước cần thực hiện để tích hợp chatbot vào môi trường ERP, đảm bảo mọi thành phần hoạt động chính xác và phản hồi theo kịch bản đã xây dựng.

### Bước 6: Thiết lập quy trình kiểm thử (system test) cho hệ thống chatbot ERP
Prompt 6 (dựa trên kết quả bước 5):

*“Hãy thiết lập quy trình kiểm thử toàn bộ hệ thống chatbot ERP, bao gồm:
Kiểm thử chức năng (functional testing): Đảm bảo các kịch bản hội thoại hoạt động đúng, phản hồi chính xác theo yêu cầu.
Kiểm thử hiệu năng (performance testing): Đo thời gian phản hồi, khả năng xử lý đồng thời các yêu cầu.
Kiểm thử bảo mật (security testing): Đảm bảo dữ liệu được bảo vệ, không có lỗ hổng khi truy xuất qua API.
Kiểm thử tích hợp (integration testing): Đảm bảo chatbot hoạt động liền mạch với các module ERP khác.”*

Đầu ra mong đợi:
* Một kế hoạch kiểm thử chi tiết, nêu rõ các công cụ và chỉ số đánh giá (ví dụ: thời gian phản hồi, tỉ lệ lỗi, số lượng người dùng đồng thời) để xác nhận hệ thống hoạt động đúng như yêu cầu.

## Tổng kết quy trình Prompt Chaining cho dự án ERP
* Định nghĩa yêu cầu và mục tiêu: Sử dụng Prompt 1 để liệt kê và phân loại các yêu cầu ERP cho chatbot.
* Xây dựng kịch bản hội thoại: Dựa trên yêu cầu, dùng Prompt 2 để tạo các kịch bản tương tác mẫu.
* Xác định nguồn dữ liệu đào tạo: Dùng Prompt 3 để chọn lọc và xây dựng bộ dữ liệu Q&A từ tài liệu ERP.
* Xây dựng kiến trúc hệ thống: Dùng Prompt 4 để mô tả chi tiết kiến trúc hệ thống hỗ trợ chatbot ERP.
* Triển khai prototype: Dùng Prompt 5 để mô tả quy trình tích hợp và triển khai thử nghiệm chatbot ERP.
* Thiết lập kiểm thử: Cuối cùng, dùng Prompt 6 để xác định quy trình kiểm thử toàn diện từ chức năng, hiệu năng đến bảo mật.

Việc áp dụng phương pháp prompt chaining như trên cho phép quá trình phát triển chatbot ERP trở nên có cấu trúc, dễ kiểm soát và hiệu quả hơn, đảm bảo rằng mỗi bước được xây dựng dựa trên kết quả của bước trước đó. Qua đó, hệ thống chatbot và tác nhân AI sẽ đáp ứng tốt yêu cầu của dự án ERP, từ định nghĩa yêu cầu đến kiểm thử hệ thống hoàn chỉnh.
