Bài gốc [ở đây](https://shrub-midnight-a8f.notion.site/RAG-Chatbot-Excel-17e527e535d9808b827ff0c4c77fb976)

# RAG Chatbot Excel

# Chatbot hỗ trợ đọc file excel

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

