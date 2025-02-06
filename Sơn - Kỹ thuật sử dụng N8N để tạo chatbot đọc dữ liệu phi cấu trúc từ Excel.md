# Nội dung
1.[Xây dựng chatbot private hỗ trợ truy vấn và phản hồi dữ liệu phi cấu trúc bằng N8N](https://github.com/hoanglong8/Document-Data-science/blob/main/S%C6%A1n%20-%20K%E1%BB%B9%20thu%E1%BA%ADt%20s%E1%BB%AD%20d%E1%BB%A5ng%20N8N%20%C4%91%E1%BB%83%20t%E1%BA%A1o%20chatbot%20%C4%91%E1%BB%8Dc%20d%E1%BB%AF%20li%E1%BB%87u%20phi%20c%E1%BA%A5u%20tr%C3%BAc%20t%E1%BB%AB%20Excel.md)
2.[Xây dựng workflow speech-to-text bằng N8N](https://github.com/hoanglong8/Document-Data-science/blob/main/S%C6%A1n%20-%20K%E1%BB%B9%20thu%E1%BA%ADt%20s%E1%BB%AD%20d%E1%BB%A5ng%20N8N%20%C4%91%E1%BB%83%20t%E1%BA%A1o%20chatbot%20%C4%91%E1%BB%8Dc%20d%E1%BB%AF%20li%E1%BB%87u%20phi%20c%E1%BA%A5u%20tr%C3%BAc%20t%E1%BB%AB%20Excel.md)
3.Xây dựng workflow tự động dịch văn bản bằng N8N

# 1.RAG Chatbot Excel - Chatbot hỗ trợ đọc file excel

Bài gốc [ở đây](https://shrub-midnight-a8f.notion.site/RAG-Chatbot-Excel-17e527e535d9808b827ff0c4c77fb976)

Tổng quan: Sử dụng phương pháp RAG với công cụ Pinecone

Điểm mạnh: 

- Quy trình tự động hóa khá cao
- Không cần sửa đổi dữ liệu nhiều
- Chi phí thấp
- Khả năng tra cứu nhanh và chính xác

Điểm yếu:

- Tình trạng nhiễu dữ liệu khi thêm vào các file docs lớn - nhiều thông tin như giờ MCC

## Workflow 1: Tải và định dạng toàn bộ sheet trong spreadsheet

### Ý tưởng:

- Sử dụng tính năng của HTTP Google Sheet để lấy ID của tất cả sheet
- Cho vào vòng lặp → lọc tất cả dòng không có ID → Format lại thành text → Tạo và lưu vào file docs trên Google Drive.

Triển khai:
![Hình ảnh 1](https://shrub-midnight-a8f.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F043a9a8f-6006-44cb-b853-e7caf25e509c%2Fee4e5047-7d32-4192-be6b-4e9cc28195bd%2Fimage.png?table=block&id=184527e5-35d9-8027-98ad-c5641028362a&spaceId=043a9a8f-6006-44cb-b853-e7caf25e509c&width=1420&userId=&cache=v2)

![Gif 1](https://media2.giphy.com/media/v1.Y2lkPTc5MGI3NjExaGJweGQxOHF1ZzVzMjk2aTdlbmR5MTJsejJjdDJleTJoaHNrZWg5cyZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/8xEj3WObFBKvBJexCa/giphy.gif)

Diễn Giải:

| Công cụ lõi | Tính năng | Chi phí |
| --- | --- | --- |
| HTTP request | Sử dụng API của Google Sheet để đọc tất cả ID của sheet | 0 |
|  |  |  |
1. Điểm mạnh:
    1. Nhanh
    2. Chi phí thấp
    3. Đồng dạng format
2. Điểm yếu:
    1. Tính dynamics cho từng sheet thấp

## Workflow 2: Insert file docs vào Pincone

### Ý tưởng:

- Sử dụng công cụ Pinecone vectore để lưu toàn bộ file docs
- Tải dưới dạng Binary —> Cho vào vòng lặp —>  Insert vào Pinecone.

Triển khai:
![Hình ảnh 2](https://shrub-midnight-a8f.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F043a9a8f-6006-44cb-b853-e7caf25e509c%2Fa89b5bdc-d5dc-466c-9c8a-5f642bf48c69%2Fimage.png?table=block&id=184527e5-35d9-80cd-9c27-fe83b352d36e&spaceId=043a9a8f-6006-44cb-b853-e7caf25e509c&width=1420&userId=&cache=v2)

![Gif 2](https://media3.giphy.com/media/v1.Y2lkPTc5MGI3NjExNTgybXVzcnczNTlleTVubjE4N3Njb2lvb2txODZrbHFuZ2doZjVqbyZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/ODA5iIQqJwiIRV2EyS/giphy.gif)

Diễn Giải:
|Công cụ lõi|Tính năng|Chi phí|
|---|---|---|
|Pinecone Vector store|Pinecone là cơ sở dữ liệu vector cho phép quản lý và tương tác với dữ liệu vector hiệu quả. Người dùng có thể chèn và truy xuất tài liệu, cung cấp dữ liệu cho bộ tìm kiếm hoặc kết nối với tác nhân để thực hiện nhiệm vụ cụ thể. Điều này mang lại tính linh hoạt trong phát triển và triển khai ứng dụng AI, đặc biệt khi xử lý dữ liệu vector lớn|Gần như miễn phí với dữ liệu thấp.|

## Workflow 3: RAG AI Agent

### Ý tưởng:

- Sử dụng tính năng của HTTP google sheet để lấy ID của tất cả sheet
- Cho vào vòng lặp —> lọc tất cả dòng không có ID —> Fomart lại thành text —> Tạo và lưu vào file docs trên google drive.

Triển khai:
![Hình ảnh 3](https://shrub-midnight-a8f.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F043a9a8f-6006-44cb-b853-e7caf25e509c%2F425f17e6-eb0a-4b91-80a0-5ba5f3a7d3f2%2Fimage.png?table=block&id=184527e5-35d9-80e4-a321-ef5d31032723&spaceId=043a9a8f-6006-44cb-b853-e7caf25e509c&width=1420&userId=&cache=v2)

![Gif 3](https://media3.giphy.com/media/v1.Y2lkPTc5MGI3NjExZG82bjZhd2N4em5hd3l2ZXlkYmU0MWE1bG55YjEzM2Y3ZXE0NG02dyZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/VZiQEkLL3ma2lPViT9/giphy.gif)

Diễn Giải:
|Công cụ lõi|Tính năng|Chi phí|
|---|---|---|
|ChatGPT - model 4o|Được coi là bộ não của mô hình Agent này|**Prompt đầu vào**: $0.06 / 1K tokens và **Completion đầu ra**: $0.12 / 1K tokens|

### Video demo:

https://imgur.com/a/KOYQwwz

[File Workflow n8n.json](https://github.com/hoanglong8/Document-Data-science/blob/main/n8n.json)

# 2.Tự động hóa chuyển đổi giọng nói thành văn bản (Speech-to-Text)

Bài gốc [ở đây](https://www.facebook.com/photo/?fbid=9669846533035177&set=gm.1113969847129710&idorvanity=1113089147217780)

Trong thời đại số hóa, việc tự động hóa quy trình làm việc giúp tiết kiệm thời gian và tăng hiệu suất công việc. Một trong những ứng dụng phổ biến là chuyển đổi giọng nói thành văn bản (Speech-to-Text) và gửi kết quả qua email. Trong bài viết này, chúng ta sẽ cùng khám phá một workflow trên n8n giúp tự động hóa quá trình này.

![Hình ảnh](https://scontent.fhan17-1.fna.fbcdn.net/v/t39.30808-6/476118129_9669846543035176_7887554522809818612_n.jpg?_nc_cat=107&ccb=1-7&_nc_sid=aa7b47&_nc_eui2=AeFp-DRKDKbSBlH_ZJd1Bq5kGtkfGaEJywMa2R8ZoQnLA9LbqUyyqF8KhDgX0aEGlvU&_nc_ohc=OUXQnNXv9AgQ7kNvgGT1TIB&_nc_oc=AdjC3RfX8p8vnxzKVOeDQilm9nLAGkTYR4dDoECdUIsSl9paOG5c-bJ0OPBLkkdp0g0&_nc_zt=23&_nc_ht=scontent.fhan17-1.fna&_nc_gid=AtvunKb4PrvDz4iPwDmWQeV&oh=00_AYA-B5-nraxzzHKWRT5QJiRw7Q40r-_kNLVoURouZw05Yw&oe=67A8E192)

## Mô tả tổng quan về workflow
Workflow này được thiết kế để:
* Nhận file âm thanh hoặc video từ biểu mẫu trực tuyến.
* Upload file lên Google Drive.
* Tải file từ Google Drive xuống và gửi đến API DeepGram để chuyển đổi giọng nói thành văn bản.
* Sử dụng Google Gemini AI để chỉnh sửa và tối ưu hóa kết quả.
* Xuất dữ liệu ra hai định dạng: TXT (văn bản) và SRT (phụ đề).
* Upload lại file văn bản lên Google Drive.
* Gửi kết quả qua email cho người dùng.

## Chi tiết các bước trong workflow:
1. Nhận file từ biểu mẫu (Form Submission)
Workflow bắt đầu bằng một biểu mẫu trực tuyến (Form Submission) nơi người dùng tải lên file âm thanh hoặc video cần chuyển đổi. Biểu mẫu này thu thập:
* File cần xử lý.
* Email của người nhận kết quả.
* Ngôn ngữ của nội dung.

2. Phân loại ngôn ngữ bằng Switch Node
* Một Switch Node được sử dụng để xử lý các file theo từng ngôn ngữ khác nhau (Vietnamese, English, French, Russian...)

3. Upload file lên Google Drive
* Sau khi nhận được file, workflow sẽ sử dụng Google Drive Upload Node để lưu file lên Google Drive.

4. Tải file xuống và gửi đến DeepGram để chuyển đổi giọng nói thành văn bản
* File sau đó được tải xuống thông qua Google Drive Download Node.
* Sử dụng HTTP Request Node để gửi file đến API của DeepGram – một dịch vụ AI mạnh mẽ để chuyển đổi giọng nói thành văn bản.

5. Xử lý văn bản với Google Gemini AI
* Kết quả từ DeepGram được gửi đến Google Gemini AI để tối ưu hóa, sửa lỗi chính tả và định dạng phù hợp.

6. Xuất văn bản thành file TXT và SRT
* Văn bản sau khi xử lý sẽ được lưu thành file TXT (dành cho đọc hiểu) và file SRT (dành cho phụ đề video).

7. Upload lại file lên Google Drive
* Các file TXT và SRT được tải lên Google Drive thông qua Google Drive Upload Node.

8. Sử dụng Wait Node để tránh gửi email quá nhanh
* Để tránh gửi quá nhiều email trong một khoảng thời gian ngắn, Wait Node được chèn vào trước bước gửi email. Điều này giúp hệ thống hoạt động ổn định và tránh bị giới hạn từ Gmail.

9. Gửi email kết quả cho người dùng
* Cuối cùng, workflow sử dụng Gmail Node để gửi email chứa link tải file TXT và SRT cho người dùng.

Lợi ích của workflow này:
* ✅ Tự động hóa hoàn toàn: Giúp tiết kiệm thời gian xử lý thủ công.
* ✅ Hỗ trợ nhiều ngôn ngữ: Có thể mở rộng sang nhiều ngôn ngữ khác nhau.
* ✅ Ứng dụng công nghệ AI mạnh mẽ: Kết hợp DeepGram và Google Gemini để cải thiện độ chính xác của văn bản.
* ✅ Tối ưu hóa hiệu suất: Sử dụng Wait Node để đảm bảo hệ thống gửi email hợp lý.
* ✅ Tích hợp với Google Drive và Gmail: Giúp dễ dàng quản lý file và gửi kết quả đến người dùng.

Kết luận:

Workflow này là một giải pháp mạnh mẽ để tự động hóa việc chuyển đổi giọng nói thành văn bản, phục vụ cho nhiều ứng dụng như phụ đề video, ghi chú cuộc họp, dịch thuật nội dung... Nếu bạn đang tìm kiếm một cách hiệu quả để xử lý file âm thanh/video, hãy thử triển khai workflow này trên n8n!
