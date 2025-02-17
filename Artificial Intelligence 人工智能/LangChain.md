## Khái niệm
* LangChain là một khung phần mềm giúp đơn giản hóa việc xây dựng các ứng dụng được hỗ trợ bởi các mô hình ngôn ngữ lớn (LLM). Nó cung cấp các công cụ và trừu tượng để cải thiện khả năng tùy biến, độ chính xác và mức độ liên quan của thông tin mà các mô hình này tạo ra.
* Được ra mắt vào tháng 10 năm 2022 bởi Harrison Chase và nhanh chóng trở nên phổ biến, với sự đóng góp từ hàng trăm cộng tác viên trên GitHub.

## Mục tiêu: 
LangChain nhằm mục đích tạo điều kiện thuận lợi cho việc tích hợp LLMs vào các ứng dụng, chẳng hạn như chatbot, phân tích tài liệu và tóm tắt, và phân tích mã.

## Tính năng: 
LangChain cung cấp một giao diện tiêu chuẩn cho các chuỗi, tích hợp với các công cụ khác và các chuỗi đầu cuối cho các ứng dụng phổ biến. Các thành phần mô-đun của LangChain có thể được "xâu chuỗi" với nhau để tạo các ứng dụng, giảm thiểu lượng mã và kiến thức chuyên sâu cần thiết để thực hiện các tác vụ NLP phức tạp.

## Ưu điểm:
* Cho phép so sánh động các lời nhắc khác nhau và thậm chí các mô hình nền tảng khác nhau với nhu cầu tối thiểu để viết lại mã.
* Cho phép các chương trình sử dụng nhiều LLM.
* Cung cấp cho các nhà phát triển AI các công cụ để kết nối các mô hình ngôn ngữ với các nguồn dữ liệu bên ngoài mà không cần đào tạo lại.

## Ngôn ngữ: 
LangChain có sẵn trong cả thư viện dựa trên Python và Javascript.

## So sánh ẩn dụ
Hãy tưởng tượng bạn có một siêu đầu bếp (LLM) có khả năng nấu bất kỳ món ăn nào trên thế giới chỉ dựa vào công thức trong đầu. Đầu bếp này rất giỏi, nhưng gặp một số hạn chế:

* Chỉ biết những công thức đã học: Đầu bếp chỉ có thể nấu những món ăn mà họ đã được đào tạo về công thức. Nếu bạn muốn họ nấu một món ăn mới mà họ chưa từng nghe đến, họ sẽ không thể làm được. (Giống như LLM chỉ biết những thông tin đã được đào tạo.)
* Không biết nguồn cung cấp nguyên liệu ở đâu: Đầu bếp không biết bạn có bao nhiêu nguyên liệu, hoặc nơi để mua nguyên liệu tươi ngon nhất. (LLM không biết cách truy cập thông tin bên ngoài.)
* Không biết bạn thích ăn gì: Đầu bếp không biết bạn thích ăn cay, ngọt, hay chua. (LLM không biết bối cảnh cụ thể của người dùng.)

Trong khi đó, LangChain giống như một người quản lý nhà bếp:

* Cung cấp công thức mới (chuỗi lời nhắc): Người quản lý này có thể tìm kiếm các công thức mới trên internet (các chuỗi lời nhắc) và đưa cho đầu bếp để mở rộng khả năng nấu nướng của họ.
* Tìm kiếm nguyên liệu (công cụ): Người quản lý biết nơi mua nguyên liệu tươi ngon nhất (công cụ), biết cách sử dụng tủ lạnh (cơ sở dữ liệu) để kiểm tra xem bạn còn những gì.
* Nắm bắt sở thích của bạn (bộ nhớ): Người quản lý ghi nhớ những món ăn bạn thích, những món bạn không thích, và các yêu cầu đặc biệt của bạn (bộ nhớ).

=> Nhờ có người quản lý nhà bếp (LangChain), siêu đầu bếp (LLM) giờ đây có thể:

* Nấu nhiều món ăn hơn, kể cả những món mới (có tính tự học tập).
* Sử dụng nguyên liệu tốt nhất có sẵn (có tính phân tích).
* Nấu ăn theo sở thích cá nhân của bạn (cá nhân hóa dữ liệu).
