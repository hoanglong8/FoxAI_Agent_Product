Bài gốc [ở đây](https://shrub-midnight-a8f.notion.site/RAG-Chatbot-Excel-17e527e535d9808b827ff0c4c77fb976)

# RAG Chatbot Excel

## Chatbot hỗ trợ đọc file excel

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

Diễn Giải:
|Công cụ lõi|Tính năng|Chi phí|
|---|---|---|
|ChatGPT - model 4o|Được coi là bộ não của mô hình Agent này|**Prompt đầu vào**: $0.06 / 1K tokens và **Completion đầu ra**: $0.12 / 1K tokens|

### Video demo:

![Ảnh gif](https://imgur.com/a/KOYQwwz)

[File Workflow n8n.json](https://github.com/hoanglong8/Document-Data-science/blob/main/n8n.json)
