# AI Agents - Huyền Chip tóm lược một cách ngắn gọn
Link bài gốc [ở đây](https://huyenchip.com//2025/01/07/agents.html)
## Lời nói đầu
Nhiều người coi các tác nhân thông minh là mục tiêu cuối cùng của AI. Cuốn sách kinh điển của Stuart Russell và Peter Norvig, Artificial Intelligence: A Modern Approach (Prentice Hall, 1995), định nghĩa lĩnh vực nghiên cứu AI là “ nghiên cứu và thiết kế các tác nhân hợp lý ” .

Khả năng chưa từng có của các mô hình nền tảng đã mở ra cánh cửa cho các ứng dụng đại lý mà trước đây không thể tưởng tượng được. Những khả năng mới này cuối cùng cũng giúp phát triển các đại lý thông minh, tự chủ để hoạt động như trợ lý, đồng nghiệp và huấn luyện viên của chúng ta. Chúng có thể giúp chúng ta tạo trang web, thu thập dữ liệu, lập kế hoạch cho chuyến đi, nghiên cứu thị trường, quản lý tài khoản khách hàng, tự động nhập dữ liệu, chuẩn bị cho chúng ta phỏng vấn, phỏng vấn ứng viên, đàm phán thỏa thuận, v.v. Các khả năng dường như vô tận và giá trị kinh tế tiềm năng của các đại lý này là rất lớn.

Phần này sẽ bắt đầu bằng tổng quan về các tác nhân và sau đó tiếp tục với hai khía cạnh xác định khả năng của tác nhân: công cụ và lập kế hoạch. Các tác nhân, với các chế độ hoạt động mới của chúng, có các chế độ thất bại mới. Phần này sẽ kết thúc bằng một cuộc thảo luận về cách đánh giá các tác nhân để phát hiện những thất bại này.

Bài đăng này được chuyển thể từ mục Agents của AI Engineering (2025) với một số chỉnh sửa nhỏ để trở thành một bài đăng độc lập.

Các tác nhân được hỗ trợ bởi AI là một lĩnh vực mới nổi không có khuôn khổ lý thuyết nào được thiết lập để xác định, phát triển và đánh giá chúng. Phần này là nỗ lực hết sức để xây dựng một khuôn khổ từ các tài liệu hiện có, nhưng nó sẽ phát triển khi lĩnh vực này phát triển. So với phần còn lại của cuốn sách, phần này mang tính thử nghiệm nhiều hơn. Tôi đã nhận được phản hồi hữu ích từ những người đánh giá ban đầu và tôi hy vọng cũng sẽ nhận được phản hồi từ độc giả của bài đăng trên blog này.
Ngay trước khi cuốn sách này ra mắt, Anthropic đã đăng một bài đăng trên blog về Xây dựng các tác nhân hiệu quả (tháng 12 năm 2024). Tôi rất vui khi thấy bài đăng trên blog của Anthropic và mục tác nhân của tôi có sự thống nhất về mặt khái niệm , mặc dù có các thuật ngữ hơi khác nhau. Tuy nhiên, bài đăng của Anthropic tập trung vào các mô hình riêng lẻ, trong khi bài đăng của tôi đề cập đến lý do và cách thức mọi thứ hoạt động. Tôi cũng tập trung nhiều hơn vào việc lập kế hoạch, lựa chọn công cụ và các chế độ thất bại.

## Tổng quan về tác nhân AI
Thuật ngữ tác nhân đã được sử dụng trong nhiều bối cảnh kỹ thuật khác nhau, bao gồm nhưng không giới hạn ở tác nhân phần mềm, tác nhân thông minh, tác nhân người dùng, tác nhân đàm thoại và tác nhân học tăng cường. Vậy, tác nhân chính xác là gì?

Một tác nhân là bất kỳ thứ gì có thể nhận thức được môi trường của nó và tác động lên môi trường đó. Trí tuệ nhân tạo: Một cách tiếp cận hiện đại (1995) định nghĩa một tác nhân là bất kỳ thứ gì có thể được xem là nhận thức được môi trường của nó thông qua các cảm biến và tác động lên môi trường đó thông qua các bộ truyền động.

Điều này có nghĩa là một tác nhân được đặc trưng bởi môi trường mà nó hoạt động và tập hợp các hành động mà nó có thể thực hiện.

Môi trường mà một tác nhân có thể hoạt động được xác định bởi trường hợp sử dụng của nó. Nếu một tác nhân được phát triển để chơi một trò chơi (ví dụ: Minecraft, Go, Dota ), thì trò chơi đó là môi trường của nó. Nếu bạn muốn một tác nhân thu thập tài liệu từ internet, thì môi trường đó là internet. Môi trường của một tác nhân xe tự lái là hệ thống đường bộ và các khu vực lân cận.

Bộ hành động mà một tác nhân AI có thể thực hiện được tăng cường bởi các công cụ mà nó có quyền truy cập. Nhiều ứng dụng AI tạo ra mà bạn tương tác hàng ngày là các tác nhân có quyền truy cập vào các công cụ, mặc dù là những công cụ đơn giản. ChatGPT là một tác nhân. Nó có thể tìm kiếm trên web, thực thi mã Python và tạo hình ảnh. Các hệ thống RAG là các tác nhân—trình truy xuất văn bản, trình truy xuất hình ảnh và trình thực thi SQL là các công cụ của chúng.

Có sự phụ thuộc mạnh mẽ giữa môi trường của tác nhân và bộ công cụ của nó. Môi trường xác định những công cụ mà tác nhân có thể sử dụng. Ví dụ, nếu môi trường là một ván cờ vua, thì hành động khả thi duy nhất của tác nhân là các nước cờ hợp lệ. Tuy nhiên, kho công cụ của tác nhân hạn chế môi trường mà nó có thể hoạt động. Ví dụ, nếu hành động duy nhất của rô-bốt là bơi, thì nó sẽ bị giới hạn trong môi trường nước.

Hình 6-8 cho thấy hình ảnh trực quan của SWE-agent (Yang và cộng sự, 2024), một tác nhân được xây dựng trên GPT-4. Môi trường của nó là máy tính có thiết bị đầu cuối và hệ thống tệp. Bộ hành động của nó bao gồm điều hướng kho lưu trữ, tìm kiếm tệp, xem tệp và chỉnh sửa dòng.

[Hình 6-8.](https://imgur.com/a/WBFAAvQ)
SWE-agent là một tác nhân mã hóa có môi trường là máy tính và các hành động của nó bao gồm điều hướng, tìm kiếm, xem tệp và chỉnh sửa

Một tác nhân AI có nhiệm vụ thực hiện các nhiệm vụ thường do người dùng cung cấp. Trong một tác nhân AI, AI là bộ não xử lý nhiệm vụ, lập kế hoạch cho một chuỗi hành động để đạt được nhiệm vụ này và xác định xem nhiệm vụ đã được hoàn thành hay chưa.

Hãy quay lại hệ thống RAG với dữ liệu dạng bảng trong ví dụ Kitty Vogue ở trên. Đây là một tác nhân đơn giản với ba hành động:

* Tạo phản hồi;
* Tạo truy vấn SQL;
* Thực hiện truy vấn SQL;
Với truy vấn này `"Project the sales revenue for Fruity Fedora over the next three months"`, tác nhân có thể thực hiện chuỗi hành động sau:

* Lập luận về cách thực hiện nhiệm vụ này, ví dụ như để dự đoán doanh số trong tương lai, trước tiên cần có số liệu bán hàng trong năm năm qua. Lập luận của một tác nhân có thể được thể hiện dưới dạng phản hồi trung gian.
* Gọi lệnh tạo truy vấn SQL để tạo truy vấn nhằm lấy số liệu bán hàng trong năm năm qua.
* Gọi lệnh thực thi truy vấn SQL thứ nhất.
* Lập luận về đầu ra của công cụ (đầu ra từ việc thực hiện truy vấn SQL) và cách chúng giúp dự đoán doanh số. Nó có thể nhận biết rằng những con số này không đủ để đưa ra dự báo đáng tin cậy, có thể là do thiếu giá trị. Sau đó, nó quyết định sẽ cần lấy thêm thông tin về các chiến dịch tiếp thị trước đây.
* Gọi lệnh tạo truy vấn SQL để tạo các truy vấn cho các chiến dịch tiếp thị trước đây.
* Gọi thực thi truy vấn SQL thứ hai.
* Lập luận là thông tin mới này đủ để giúp dự đoán doanh số trong tương lai. Sau đó, nó tạo ra một dự báo.
* Lập luận nhiệm vụ đã được hoàn thành thành công.

So với các trường hợp sử dụng không phải tác nhân, tác nhân thường yêu cầu các mô hình mạnh hơn vì hai lý do:

* **Lỗi phức hợp:** một tác nhân thường cần thực hiện nhiều bước để hoàn thành một nhiệm vụ và độ chính xác tổng thể sẽ bị giảm khi số bước tăng. Nếu độ chính xác của mô hình là 95% cho mỗi bước, sau 10 bước, độ chính xác sẽ giảm xuống còn 60% và sau 100 bước, độ chính xác sẽ chỉ còn 0,6%.
* **Rủi ro cao hơn:** khi có quyền truy cập vào các công cụ, các tác nhân có khả năng thực hiện các nhiệm vụ có tác động lớn hơn, nhưng bất kỳ lỗi nào cũng có thể gây ra hậu quả nghiêm trọng hơn.
Một nhiệm vụ đòi hỏi nhiều bước có thể tốn thời gian và tiền bạc để chạy. Một lời phàn nàn phổ biến là các tác nhân chỉ giỏi đốt token API của bạn. Tuy nhiên, nếu các tác nhân có thể tự chủ, họ có thể tiết kiệm thời gian của con người, khiến chi phí của họ trở nên xứng đáng.

Với một môi trường, sự thành công của một tác nhân trong môi trường phụ thuộc vào công cụ mà nó có thể truy cập và sức mạnh của trình lập kế hoạch AI. Hãy bắt đầu bằng cách xem xét các loại công cụ khác nhau mà một mô hình có thể sử dụng. Chúng ta sẽ phân tích khả năng lập kế hoạch của AI tiếp theo.

### Công cụ
Một hệ thống không cần truy cập vào các công cụ bên ngoài để trở thành một tác nhân. Tuy nhiên, nếu không có các công cụ bên ngoài, khả năng của tác nhân sẽ bị hạn chế. Bản thân một mô hình thường có thể thực hiện một hành động—một LLM có thể tạo văn bản và một trình tạo hình ảnh có thể tạo hình ảnh. Các công cụ bên ngoài giúp tác nhân có khả năng hơn rất nhiều.

Các công cụ giúp tác nhân vừa nhận thức được môi trường vừa hành động theo môi trường đó. Các hành động cho phép tác nhân nhận thức được môi trường là các hành động chỉ đọc , trong khi các hành động cho phép tác nhân hành động theo môi trường là các hành động ghi .

Bộ công cụ mà một tác nhân có thể truy cập là kho công cụ của tác nhân đó. Vì kho công cụ của tác nhân xác định những gì tác nhân có thể làm, nên điều quan trọng là phải suy nghĩ kỹ xem nên cung cấp cho tác nhân những gì và bao nhiêu công cụ. Nhiều công cụ hơn sẽ cung cấp cho tác nhân nhiều khả năng hơn. Tuy nhiên, càng có nhiều công cụ, thì việc hiểu và sử dụng chúng tốt càng khó khăn hơn. Cần phải thử nghiệm để tìm ra bộ công cụ phù hợp, như đã thảo luận sau trong phần “ Lựa chọn công cụ ”.

Tùy thuộc vào môi trường của tác nhân, có nhiều công cụ khả thi. Sau đây là ba loại công cụ mà bạn có thể muốn cân nhắc: tăng cường kiến ​​thức (tức là xây dựng ngữ cảnh), mở rộng khả năng và các công cụ cho phép tác nhân của bạn tác động vào môi trường của nó.

### Tăng cường kiến ​​thức
Tôi hy vọng rằng cuốn sách này, cho đến nay, đã thuyết phục bạn về tầm quan trọng của việc có bối cảnh liên quan đến chất lượng phản hồi của mô hình. Một danh mục công cụ quan trọng bao gồm các công cụ giúp tăng cường kiến ​​thức của tác nhân của bạn. Một số trong số chúng đã được thảo luận: trình thu thập văn bản, trình thu thập hình ảnh và trình thực thi SQL. Các công cụ tiềm năng khác bao gồm tìm kiếm người nội bộ, API kiểm kê trả về trạng thái của các sản phẩm khác nhau, truy xuất Slack, trình đọc email, v.v.

Nhiều công cụ như vậy bổ sung cho mô hình bằng các quy trình và thông tin riêng tư của tổ chức bạn. Tuy nhiên, các công cụ cũng có thể cung cấp cho mô hình quyền truy cập vào thông tin công khai, đặc biệt là từ internet.

Duyệt web là một trong những khả năng sớm nhất và được mong đợi nhất được tích hợp vào ChatGPT. Duyệt web giúp mô hình không bị cũ. Mô hình trở nên cũ khi dữ liệu được đào tạo trở nên lỗi thời. Nếu dữ liệu đào tạo của mô hình bị cắt vào tuần trước, mô hình sẽ không thể trả lời các câu hỏi yêu cầu thông tin từ tuần này trừ khi thông tin này được cung cấp trong ngữ cảnh. Nếu không có duyệt web, mô hình sẽ không thể cho bạn biết về thời tiết, tin tức, sự kiện sắp tới, giá cổ phiếu, tình trạng chuyến bay, v.v.

Tôi sử dụng thuật ngữ duyệt web để chỉ tất cả các công cụ truy cập internet, bao gồm trình duyệt web và các API như API tìm kiếm, API tin tức, API GitHub hoặc API mạng xã hội.

Trong khi duyệt web cho phép tác nhân của bạn tham khảo thông tin mới nhất để tạo ra phản hồi tốt hơn và giảm ảo giác, nó cũng có thể mở ra cho tác nhân của bạn những hố sâu của internet. Hãy lựa chọn API Internet của bạn một cách cẩn thận.

### Mở rộng khả năng
Bạn cũng có thể cân nhắc các công cụ giải quyết những hạn chế cố hữu của các mô hình AI. Chúng là những cách dễ dàng để tăng hiệu suất cho mô hình của bạn. Ví dụ, các mô hình AI nổi tiếng là kém về toán học. Nếu bạn hỏi một mô hình 199.999 chia cho 292 bằng bao nhiêu, thì mô hình đó có khả năng sẽ thất bại. Tuy nhiên, phép tính này sẽ trở nên đơn giản nếu mô hình có quyền truy cập vào máy tính. Thay vì cố gắng đào tạo mô hình để giỏi số học, thì việc chỉ cần cung cấp cho mô hình quyền truy cập vào một công cụ sẽ tiết kiệm tài nguyên hơn nhiều.

Các công cụ đơn giản khác có thể tăng cường đáng kể khả năng của mô hình bao gồm lịch, bộ chuyển đổi múi giờ, bộ chuyển đổi đơn vị (ví dụ: từ lbs sang kg) và trình dịch có thể dịch sang và từ các ngôn ngữ mà mô hình không giỏi.

Các công cụ phức tạp hơn nhưng mạnh mẽ hơn là trình thông dịch mã. Thay vì đào tạo một mô hình để hiểu mã, bạn có thể cấp cho mô hình quyền truy cập vào trình thông dịch mã để thực thi một đoạn mã, trả về kết quả hoặc phân tích lỗi của mã. Khả năng này cho phép các tác nhân của bạn hoạt động như trợ lý mã hóa, nhà phân tích dữ liệu và thậm chí là trợ lý nghiên cứu có thể viết mã để chạy thử nghiệm và báo cáo kết quả. Tuy nhiên, việc thực thi mã tự động đi kèm với rủi ro bị tấn công tiêm mã, như đã thảo luận trong Chương 5 trong phần “Kỹ thuật nhắc nhở phòng thủ ” . Các phép đo bảo mật phù hợp là rất quan trọng để giữ an toàn cho bạn và người dùng của bạn.

Các công cụ có thể biến mô hình chỉ có văn bản hoặc chỉ có hình ảnh thành mô hình đa phương thức. Ví dụ, một mô hình chỉ có thể tạo văn bản có thể tận dụng mô hình văn bản thành hình ảnh làm công cụ, cho phép tạo cả văn bản và hình ảnh. Với yêu cầu văn bản, trình lập kế hoạch AI của tác nhân sẽ quyết định có nên gọi tạo văn bản, tạo hình ảnh hay cả hai. Đây là cách ChatGPT có thể tạo cả văn bản và hình ảnh—nó sử dụng DALL-E làm trình tạo hình ảnh của mình.

Các tác nhân cũng có thể sử dụng trình thông dịch mã để tạo biểu đồ và đồ thị, trình biên dịch LaTex để hiển thị các phương trình toán học hoặc trình duyệt để hiển thị các trang web từ mã HTML.

Tương tự như vậy, một mô hình chỉ có thể xử lý đầu vào văn bản có thể sử dụng công cụ chú thích hình ảnh để xử lý hình ảnh và công cụ phiên âm để xử lý âm thanh. Nó có thể sử dụng công cụ OCR (nhận dạng ký tự quang học) để đọc PDF.

Việc sử dụng công cụ có thể tăng đáng kể hiệu suất của mô hình so với chỉ nhắc nhở hoặc thậm chí tinh chỉnh . Chameleon (Lu và cộng sự, 2023) cho thấy một tác nhân chạy bằng GPT-4, được tăng cường bằng một bộ 13 công cụ, có thể vượt trội hơn GPT-4 một mình trên một số điểm chuẩn. Ví dụ về các công cụ mà tác nhân này sử dụng là truy xuất kiến ​​thức, trình tạo truy vấn, trình chú thích hình ảnh, trình phát hiện văn bản và tìm kiếm Bing.

Trên ScienceQA, một chuẩn mực trả lời câu hỏi khoa học, Chameleon cải thiện kết quả ít lần xuất bản tốt nhất lên 11,37%. Trên TabMWP (Tabular Math Word Problems) (Lu và cộng sự, 2022), một chuẩn mực liên quan đến các câu hỏi toán học dạng bảng, Chameleon cải thiện độ chính xác lên 17%.

### Viết hành động
Cho đến nay, chúng ta đã thảo luận về các hành động chỉ đọc cho phép mô hình đọc từ các nguồn dữ liệu của nó. Nhưng các công cụ cũng có thể thực hiện các hành động ghi, tạo ra các thay đổi đối với các nguồn dữ liệu. Một trình thực thi SQL có thể truy xuất bảng dữ liệu (đọc) và thay đổi hoặc xóa bảng (ghi). Một API email có thể đọc email nhưng cũng có thể phản hồi email đó. Một API ngân hàng có thể truy xuất số dư hiện tại của bạn, nhưng cũng có thể khởi tạo chuyển khoản ngân hàng.

Viết hành động cho phép hệ thống làm nhiều hơn. Chúng có thể cho phép bạn tự động hóa toàn bộ quy trình tiếp cận khách hàng: nghiên cứu khách hàng tiềm năng, tìm kiếm thông tin liên lạc của họ, soạn email, gửi email đầu tiên, đọc phản hồi, theo dõi, trích xuất đơn hàng, cập nhật cơ sở dữ liệu của bạn với đơn hàng mới, v.v.

Tuy nhiên, viễn cảnh trao cho AI khả năng tự động thay đổi cuộc sống của chúng ta là điều đáng sợ. Cũng giống như bạn không nên trao cho thực tập sinh quyền xóa cơ sở dữ liệu sản xuất của mình, bạn không nên cho phép một AI không đáng tin cậy khởi tạo chuyển khoản ngân hàng. Tin tưởng vào khả năng của hệ thống và các biện pháp bảo mật của nó là rất quan trọng. Bạn cần đảm bảo rằng hệ thống được bảo vệ khỏi những kẻ xấu có thể cố gắng thao túng nó để thực hiện các hành động có hại.

Bất cứ khi nào tôi nói về các tác nhân AI tự động với một nhóm người, thường có người nhắc đến xe tự lái. “ Sẽ thế nào nếu ai đó hack vào xe để bắt cóc bạn? ” Trong khi ví dụ về xe tự lái có vẻ bản năng vì tính vật lý của nó, một hệ thống AI có thể gây hại mà không cần hiện diện trong thế giới vật lý. Nó có thể thao túng thị trường chứng khoán, đánh cắp bản quyền, vi phạm quyền riêng tư, củng cố thành kiến, phát tán thông tin sai lệch và tuyên truyền, v.v., như đã thảo luận trong phần “Kỹ thuật nhắc nhở phòng thủ” trong Chương 5.

Đây đều là những mối quan tâm chính đáng và bất kỳ tổ chức nào muốn tận dụng AI đều cần phải coi trọng vấn đề an toàn và bảo mật. Tuy nhiên, điều này không có nghĩa là các hệ thống AI không bao giờ được trao khả năng hoạt động trong thế giới thực. Nếu chúng ta có thể tin tưởng một cỗ máy đưa chúng ta vào không gian, tôi hy vọng rằng một ngày nào đó, các biện pháp an ninh sẽ đủ để chúng ta tin tưởng các hệ thống AI tự động. Bên cạnh đó, con người cũng có thể thất bại. Cá nhân tôi sẽ tin tưởng một chiếc xe tự lái hơn là một người lạ trung bình cho tôi đi nhờ xe.

Cũng giống như các công cụ phù hợp có thể giúp con người làm việc hiệu quả hơn rất nhiều—bạn có thể tưởng tượng việc kinh doanh mà không cần Excel hay xây dựng một tòa nhà chọc trời mà không cần cần cẩu không?—các công cụ cho phép các mô hình thực hiện nhiều nhiệm vụ hơn nữa. Nhiều nhà cung cấp mô hình đã hỗ trợ sử dụng công cụ với các mô hình của họ, một tính năng thường được gọi là gọi hàm. Trong tương lai, tôi mong đợi việc gọi hàm với một bộ công cụ rộng sẽ phổ biến với hầu hết các mô hình.

## Kế hoạch
Trọng tâm của một tác nhân mô hình nền tảng là mô hình chịu trách nhiệm giải quyết các nhiệm vụ do người dùng cung cấp. Một nhiệm vụ được xác định bởi mục tiêu và ràng buộc của nó. Ví dụ, một nhiệm vụ là lên lịch cho chuyến đi kéo dài hai tuần từ San Francisco đến Ấn Độ với ngân sách là 5.000 đô la. Mục tiêu là chuyến đi kéo dài hai tuần. Ràng buộc là ngân sách.

Các nhiệm vụ phức tạp đòi hỏi phải lập kế hoạch. Đầu ra của quá trình lập kế hoạch là một kế hoạch, là một lộ trình phác thảo các bước cần thiết để hoàn thành một nhiệm vụ. Lập kế hoạch hiệu quả thường yêu cầu mô hình phải hiểu nhiệm vụ, xem xét các tùy chọn khác nhau để hoàn thành nhiệm vụ này và chọn tùy chọn hứa hẹn nhất.

Nếu bạn đã từng tham gia bất kỳ cuộc họp lập kế hoạch nào, bạn sẽ biết rằng lập kế hoạch rất khó. Là một vấn đề tính toán quan trọng, lập kế hoạch được nghiên cứu kỹ lưỡng và sẽ cần nhiều tập để trình bày. Tôi sẽ chỉ có thể trình bày sơ lược ở đây.

### Tổng quan về kế hoạch
Với một nhiệm vụ, có nhiều cách có thể giải quyết, nhưng không phải tất cả đều dẫn đến kết quả thành công. Trong số các giải pháp đúng, một số hiệu quả hơn những giải pháp khác. Hãy xem xét truy vấn, `"How many companies without revenue have raised at least $1 billion?"`, và hai giải pháp ví dụ:

* Tìm tất cả các công ty không có doanh thu, sau đó lọc theo số tiền huy động được.
* Tìm tất cả các công ty đã huy động được ít nhất 1 tỷ đô la, sau đó lọc theo doanh thu.

Lựa chọn thứ hai hiệu quả hơn. Có nhiều công ty không có doanh thu hơn là các công ty đã huy động được 1 tỷ đô la. Chỉ với hai lựa chọn này, một tác nhân thông minh nên chọn lựa chọn 2.

Bạn có thể kết hợp lập kế hoạch với thực hiện trong cùng một lời nhắc. Ví dụ, bạn đưa ra lời nhắc cho mô hình, yêu cầu nó suy nghĩ từng bước (chẳng hạn như với lời nhắc chuỗi suy nghĩ), rồi thực hiện tất cả các bước đó trong một lời nhắc. Nhưng nếu mô hình đưa ra một kế hoạch 1.000 bước mà thậm chí không đạt được mục tiêu thì sao? Nếu không có sự giám sát, một tác nhân có thể chạy các bước đó trong nhiều giờ, lãng phí thời gian và tiền bạc vào các cuộc gọi API, trước khi bạn nhận ra rằng nó không đi đến đâu cả.

Để tránh thực hiện vô ích, cần tách kế hoạch khỏi thực hiện . Bạn yêu cầu tác nhân tạo một kế hoạch trước và chỉ sau khi kế hoạch này được xác thực thì nó mới được thực hiện. Kế hoạch có thể được xác thực bằng phương pháp tìm kiếm. Ví dụ, một phương pháp tìm kiếm đơn giản là loại bỏ các kế hoạch có hành động không hợp lệ. Nếu kế hoạch được tạo ra yêu cầu tìm kiếm trên Google và tác nhân không có quyền truy cập vào Tìm kiếm trên Google, thì kế hoạch này không hợp lệ. Một phương pháp tìm kiếm đơn giản khác có thể là loại bỏ tất cả các kế hoạch có nhiều hơn X bước.

Một kế hoạch cũng có thể được xác thực bằng cách sử dụng các thẩm phán AI. Bạn có thể yêu cầu một mô hình đánh giá xem kế hoạch có hợp lý không hoặc làm thế nào để cải thiện nó.

Nếu kế hoạch được tạo ra được đánh giá là không tốt, bạn có thể yêu cầu người lập kế hoạch tạo ra một kế hoạch khác. Nếu kế hoạch được tạo ra là tốt, hãy thực hiện nó.

Nếu kế hoạch bao gồm các công cụ bên ngoài, lệnh gọi hàm sẽ được gọi. Đầu ra từ việc thực hiện kế hoạch này sau đó sẽ cần được đánh giá lại. Lưu ý rằng kế hoạch được tạo không nhất thiết phải là kế hoạch đầu cuối cho toàn bộ tác vụ. Nó có thể là một kế hoạch nhỏ cho một tác vụ phụ. Toàn bộ quy trình trông giống như Hình 6-9.

[Hình 6-9.](https://imgur.com/vmpZDUp)
Tách rời kế hoạch và thực hiện để chỉ những kế hoạch đã được xác thực mới được thực hiện

Hệ thống của bạn hiện có ba thành phần: `một để tạo kế hoạch`, `một để xác thực kế hoạch` và `một để thực hiện kế hoạch`. Nếu bạn coi mỗi thành phần là một tác nhân, thì đây có thể được coi là hệ thống đa tác nhân. Vì hầu hết các quy trình làm việc của tác nhân đều đủ phức tạp để liên quan đến nhiều thành phần, nên hầu hết các tác nhân đều là đa tác nhân.

Để tăng tốc quá trình, thay vì tạo kế hoạch tuần tự, bạn có thể tạo nhiều kế hoạch song song và yêu cầu người đánh giá chọn kế hoạch hứa hẹn nhất. Đây là một sự đánh đổi khác về độ trễ–chi phí, vì tạo nhiều kế hoạch cùng lúc sẽ phát sinh thêm chi phí.

Lập kế hoạch đòi hỏi phải hiểu được ý định đằng sau một nhiệm vụ: người dùng đang cố gắng làm gì với truy vấn này? Một trình phân loại ý định thường được sử dụng để giúp các tác nhân lập kế hoạch. Như được trình bày trong Chương 5 trong phần “Chia các nhiệm vụ phức tạp thành các nhiệm vụ con đơn giản hơn ” , phân loại ý định có thể được thực hiện bằng cách sử dụng một lời nhắc khác hoặc một mô hình phân loại được đào tạo cho nhiệm vụ này. Cơ chế phân loại ý định có thể được coi là một tác nhân khác trong hệ thống đa tác nhân của bạn.

Biết được mục đích có thể giúp nhân viên chọn đúng công cụ. Ví dụ, đối với bộ phận hỗ trợ khách hàng, nếu truy vấn liên quan đến thanh toán, nhân viên có thể cần truy cập vào công cụ để lấy lại các khoản thanh toán gần đây của người dùng. Nhưng nếu truy vấn liên quan đến cách đặt lại mật khẩu, nhân viên có thể cần truy cập vào chức năng lấy lại tài liệu.

```Mẹo :
Một số truy vấn có thể nằm ngoài phạm vi của tác nhân. Bộ phân loại ý định phải có khả năng phân loại các yêu cầu để IRRELEVANTtác nhân có thể lịch sự từ chối các yêu cầu đó thay vì lãng phí FLOP để đưa ra các giải pháp không thể.
```
Cho đến nay, chúng tôi đã giả định rằng tác nhân tự động hóa cả ba giai đoạn: tạo kế hoạch, xác thực kế hoạch và thực hiện kế hoạch. Trên thực tế, con người có thể tham gia vào bất kỳ giai đoạn nào để hỗ trợ quá trình và giảm thiểu rủi ro.

* Một chuyên gia con người có thể cung cấp một kế hoạch, xác nhận một kế hoạch hoặc thực hiện một phần của một kế hoạch. Ví dụ, đối với các nhiệm vụ phức tạp mà một tác nhân gặp khó khăn khi tạo ra toàn bộ kế hoạch, một chuyên gia con người có thể cung cấp một kế hoạch cấp cao mà tác nhân có thể mở rộng.
* Nếu một kế hoạch liên quan đến các hoạt động rủi ro, chẳng hạn như cập nhật cơ sở dữ liệu hoặc hợp nhất thay đổi mã, hệ thống có thể yêu cầu sự chấp thuận rõ ràng của con người trước khi thực hiện hoặc chuyển giao cho con người thực hiện các hoạt động này. Để thực hiện được điều này, bạn cần xác định rõ mức độ tự động hóa mà một tác nhân có thể có cho mỗi hành động.

Tóm lại, việc giải quyết một nhiệm vụ thường bao gồm các quy trình sau. Lưu ý rằng phản xạ không phải là bắt buộc đối với một tác nhân, nhưng nó sẽ thúc đẩy đáng kể hiệu suất của tác nhân.

* Tạo kế hoạch : đưa ra kế hoạch để hoàn thành nhiệm vụ này. Kế hoạch là một chuỗi các hành động có thể quản lý được, vì vậy quá trình này còn được gọi là phân tích nhiệm vụ.
* Phản ánh và sửa lỗi : đánh giá kế hoạch đã tạo. Nếu đó là kế hoạch tồi, hãy tạo một kế hoạch mới.
* Thực hiện : thực hiện các hành động được nêu trong kế hoạch đã tạo. Điều này thường liên quan đến việc gọi các hàm cụ thể.
* Suy ngẫm và sửa lỗi : khi nhận được kết quả hành động, hãy đánh giá những kết quả này và xác định xem mục tiêu đã đạt được chưa. Xác định và sửa lỗi. Nếu mục tiêu chưa hoàn thành, hãy lập kế hoạch mới.

Bạn đã thấy một số kỹ thuật để lập kế hoạch và phản ánh trong cuốn sách này. Khi bạn yêu cầu một mô hình "suy nghĩ từng bước", bạn đang yêu cầu nó phân tích một nhiệm vụ. Khi bạn yêu cầu một mô hình "xác minh xem câu trả lời của bạn có đúng không", bạn đang yêu cầu nó phản ánh.

### Mô hình nền tảng như những người lập kế hoạch
Một câu hỏi mở là các mô hình nền tảng có thể lập kế hoạch tốt như thế nào. Nhiều nhà nghiên cứu tin rằng các mô hình nền tảng, ít nhất là những mô hình được xây dựng trên các mô hình ngôn ngữ tự hồi quy, không thể. Nhà khoa học AI trưởng của Meta, Yann LeCun tuyên bố chắc chắn rằng các LLM tự hồi quy không thể lập kế hoạch (2023).

Mặc dù có nhiều bằng chứng giai thoại cho thấy LLM không có khả năng lập kế hoạch tốt, nhưng vẫn chưa rõ liệu đó là do chúng ta không biết cách sử dụng LLM đúng cách hay vì về cơ bản, LLM không có khả năng lập kế hoạch.

Về bản chất, lập kế hoạch là một vấn đề tìm kiếm . Bạn tìm kiếm giữa các con đường khác nhau hướng tới mục tiêu, dự đoán kết quả (phần thưởng) của mỗi con đường và chọn con đường có kết quả hứa hẹn nhất. Thông thường, bạn có thể xác định rằng không có con đường nào có thể đưa bạn đến mục tiêu.

Tìm kiếm thường yêu cầu quay lại . Ví dụ, hãy tưởng tượng bạn đang ở một bước có hai hành động khả thi: A và B. Sau khi thực hiện hành động A, bạn vào trạng thái không hứa hẹn, vì vậy bạn cần quay lại trạng thái trước đó để thực hiện hành động B.

Một số người cho rằng mô hình hồi quy tự động chỉ có thể tạo ra các hành động tiến. Nó không thể quay lại để tạo ra các hành động thay thế. Vì lý do này, họ kết luận rằng các mô hình hồi quy tự động không thể lập kế hoạch. Tuy nhiên, điều này không nhất thiết đúng. Sau khi thực hiện một đường dẫn với hành động A, nếu mô hình xác định rằng đường dẫn này không hợp lý, nó có thể sửa đổi đường dẫn bằng hành động B thay thế, thực sự là quay lại. Mô hình cũng luôn có thể bắt đầu lại và chọn một đường dẫn khác.

Cũng có thể là LLM là những người lập kế hoạch kém vì họ không được cung cấp các công cụ cần thiết để lập kế hoạch. Để lập kế hoạch, cần phải biết không chỉ các hành động khả thi mà còn cả kết quả tiềm năng của từng hành động . Ví dụ đơn giản, giả sử bạn muốn đi bộ lên núi. Các hành động tiềm năng của bạn là rẽ phải, rẽ trái, quay lại hoặc đi thẳng. Tuy nhiên, nếu rẽ phải khiến bạn rơi xuống vực, bạn có thể không cân nhắc đến hành động này. Về mặt kỹ thuật, một hành động đưa bạn từ trạng thái này sang trạng thái khác và cần phải biết trạng thái kết quả để xác định có nên thực hiện hành động hay không.

Điều này có nghĩa là việc thúc đẩy một mô hình chỉ tạo ra một chuỗi hành động giống như kỹ thuật thúc đẩy chuỗi suy nghĩ phổ biến là không đủ. Bài báo “ Lý luận với Mô hình Ngôn ngữ là Lập kế hoạch với Mô hình Thế giới ” (Hao và cộng sự, 2023) lập luận rằng một LLM, bằng cách chứa rất nhiều thông tin về thế giới, có khả năng dự đoán kết quả của mỗi hành động. LLM này có thể kết hợp dự đoán kết quả này để tạo ra các kế hoạch mạch lạc.

Ngay cả khi AI không thể lập kế hoạch, nó vẫn có thể là một phần của một người lập kế hoạch. Có thể tăng cường LLM bằng một công cụ tìm kiếm và hệ thống theo dõi trạng thái để giúp nó lập kế hoạch.

Thanh bên: Mô hình nền tảng (FM) so với các nhà lập kế hoạch học tăng cường (RL)

Tác nhân là một khái niệm cốt lõi trong RL, được định nghĩa trên Wikipedia là một lĩnh vực “ liên quan đến cách một tác nhân thông minh phải thực hiện các hành động trong một môi trường năng động để tối đa hóa phần thưởng tích lũy ” .

Các tác nhân RL và các tác nhân FM có nhiều điểm tương đồng. Cả hai đều được đặc trưng bởi môi trường và các hành động có thể xảy ra. Sự khác biệt chính là cách thức hoạt động của các nhà lập kế hoạch.

Trong một tác nhân RL, trình lập kế hoạch được đào tạo bởi một thuật toán RL. Việc đào tạo trình lập kế hoạch RL này có thể tốn nhiều thời gian và tài nguyên.
Trong một tác nhân FM, mô hình là người lập kế hoạch. Mô hình này có thể được nhắc nhở hoặc tinh chỉnh để cải thiện khả năng lập kế hoạch của nó và thường đòi hỏi ít thời gian và ít tài nguyên hơn.
Tuy nhiên, không có gì ngăn cản tác nhân FM kết hợp các thuật toán RL để cải thiện hiệu suất của nó. Tôi nghi ngờ rằng về lâu dài, các tác nhân FM và tác nhân RL sẽ hợp nhất.

### Tạo kế hoạch
Cách đơn giản nhất để biến một mô hình thành một trình tạo kế hoạch là sử dụng kỹ thuật nhắc nhở. Hãy tưởng tượng rằng bạn muốn tạo một tác nhân để giúp khách hàng tìm hiểu về các sản phẩm tại Kitty Vogue. Bạn cấp cho tác nhân này quyền truy cập vào ba công cụ bên ngoài: truy xuất sản phẩm theo giá, truy xuất các sản phẩm hàng đầu và truy xuất thông tin sản phẩm. Sau đây là ví dụ về lời nhắc để tạo kế hoạch. Lời nhắc này chỉ nhằm mục đích minh họa. Lời nhắc sản xuất có thể phức tạp hơn.

#### NHẮC NHỞ CỦA HỆ THỐNG :
