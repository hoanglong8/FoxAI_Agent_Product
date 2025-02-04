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


### File n8n json:
```json
{
  "name": "Prepare_data",
  "nodes": [
    {
      "parameters": {},
      "type": "n8n-nodes-base.manualTrigger",
      "typeVersion": 1,
      "position": [
        -1120,
        840
      ],
      "id": "ed3a521a-b963-4b4c-b85c-e9dcac406641",
      "name": "When clicking ‘Test workflow’"
    },
    {
      "parameters": {
        "content": "## Lấy ID của tất cả sheet",
        "height": 320,
        "width": 600,
        "color": 4
      },
      "type": "n8n-nodes-base.stickyNote",
      "position": [
        -1240,
        1360
      ],
      "typeVersion": 1,
      "id": "7dff268c-c8b0-48ae-90fd-35706bde5fde",
      "name": "Sticky Note1"
    },
    {
      "parameters": {
        "documentId": {
          "__rl": true,
          "value": "1Fc_Q5XAAwCwRo93uFNT0FwUb1CWScBf5CFgzTutiTxg",
          "mode": "list",
          "cachedResultName": "Bảng lương T10 (1)",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1Fc_Q5XAAwCwRo93uFNT0FwUb1CWScBf5CFgzTutiTxg/edit?usp=drivesdk"
        },
        "sheetName": {
          "__rl": true,
          "value": "={{ $json.sheetId }}",
          "mode": "id"
        },
        "options": {}
      },
      "type": "n8n-nodes-base.googleSheets",
      "typeVersion": 4.5,
      "position": [
        -240,
        1460
      ],
      "id": "39d91a8a-191f-4d0a-a2fd-5c35b613a0b3",
      "name": "Google Sheets",
      "credentials": {
        "googleSheetsOAuth2Api": {
          "id": "TZLjhkBIcfOyPeUh",
          "name": "Google Sheets account"
        }
      }
    },
    {
      "parameters": {
        "options": {}
      },
      "type": "n8n-nodes-base.splitInBatches",
      "typeVersion": 3,
      "position": [
        -580,
        1460
      ],
      "id": "55aeecfa-eb80-4ebc-8a4a-87fb147a2e56",
      "name": "Loop Over Items2",
      "alwaysOutputData": false,
      "executeOnce": false
    },
    {
      "parameters": {
        "jsCode": "// Lấy tất cả dữ liệu từ đầu vào\nconst inputItems = $input.all();\n\n// Tạo mảng mới để chứa sheetId và title\nconst outputItems = [];\n\n// Duyệt qua từng item trong input\nfor (const item of inputItems) {\n  const sheets = item.json.sheets;\n\n  // Duyệt qua từng sheet để lấy sheetId và title\n  for (const sheet of sheets) {\n    const sheetId = sheet.properties.sheetId;\n    const title = sheet.properties.title;\n\n    // Thêm sheetId và title vào output với định dạng JSON\n    outputItems.push({\n      json: {\n        sheetId: sheetId, // Sheet ID của tab\n        title: title      // Title (Tên) của tab\n      }\n    });\n  }\n}\n\n// Trả về output đã định dạng\nreturn outputItems;\n"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        -800,
        1460
      ],
      "id": "02649d0a-5a78-4dd0-a371-e11e6ffaa6c6",
      "name": "Code"
    },
    {
      "parameters": {
        "assignments": {
          "assignments": [
            {
              "id": "95204eb0-87cc-4e83-8fc5-d63c22557edd",
              "name": "sheets",
              "value": "={{ $json.sheets }}",
              "type": "array"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.set",
      "typeVersion": 3.4,
      "position": [
        -980,
        1460
      ],
      "id": "e4edfcfb-2d9d-4778-9e27-98f96900c63f",
      "name": "Edit Fields"
    },
    {
      "parameters": {
        "url": "https://sheets.googleapis.com/v4/spreadsheets/1Fc_Q5XAAwCwRo93uFNT0FwUb1CWScBf5CFgzTutiTxg",
        "authentication": "predefinedCredentialType",
        "nodeCredentialType": "googleSheetsOAuth2Api",
        "options": {}
      },
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 4.2,
      "position": [
        -1180,
        1460
      ],
      "id": "4b639dd3-0f75-4d78-9ade-2f53655a67d8",
      "name": "HTTP Request",
      "credentials": {
        "googleSheetsOAuth2Api": {
          "id": "TZLjhkBIcfOyPeUh",
          "name": "Google Sheets account"
        }
      }
    },
    {
      "parameters": {
        "jsCode": "// Lấy dữ liệu từ đầu vào (Google Sheets hoặc một nguồn khác)\nconst inputItems = $input.all();\n\n// Tạo mảng để chứa dữ liệu đã lọc\nconst filteredItems = [];\n\n// Duyệt qua từng dòng trong input\nfor (const item of inputItems) {\n  const rowID = item.json[\"ID\"]; // Truy cập cột ID của dòng hiện tại\n  \n  // Kiểm tra nếu ID tồn tại (không null, không undefined, không trống)\n  if (rowID && rowID.trim() !== \"\") {\n    filteredItems.push(item); // Nếu tồn tại, thêm vào mảng kết quả\n  }\n}\n\n// Trả về toàn bộ dòng dữ liệu có ID\nreturn filteredItems;\n"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        -100,
        1460
      ],
      "id": "e8e8d881-48f1-4a5c-b8fc-64d73f916463",
      "name": "Filter_ID"
    },
    {
      "parameters": {
        "jsCode": "// Lấy dữ liệu từ đầu vào\nconst inputItems = $input.all();\n\n// Tạo mảng chứa dữ liệu đã lọc\nconst filteredItems = [];\n\n// Duyệt qua từng dòng trong input\nfor (const item of inputItems) {\n  const row = item.json;\n\n  // Lọc các cột không bắt đầu bằng \"col_\" và không rỗng (sử dụng \"và\")\n  const filteredRow = {};\n  for (const key in row) {\n    if (!key.startsWith(\"col_\") && row[key] && row[key] !== \"[empty]\") {\n      filteredRow[key] = row[key];\n    }\n  }\n\n  // Nếu dòng có dữ liệu sau khi lọc, thêm vào kết quả\n  if (Object.keys(filteredRow).length > 0) {\n    filteredItems.push({ json: filteredRow });\n  }\n}\n\n// Trả về các dòng đã lọc\nreturn filteredItems;\n"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        60,
        1460
      ],
      "id": "c79328a4-81ba-437c-9347-f2b833c256f1",
      "name": "Filter_columns"
    },
    {
      "parameters": {
        "jsCode": "// Lấy tất cả dữ liệu từ đầu vào\nconst inputItems = $input.all();\n\n// Tạo một mảng chứa các dòng text\nconst outputText = [];\n\n// Lặp qua từng dòng dữ liệu\nfor (const item of inputItems) {\n  const row = item.json; // Lấy dữ liệu JSON của dòng\n\n  // Chuyển mỗi cặp key-value thành text\n  let rowText = '';\n  for (const key in row) {\n    rowText += `${key}: ${row[key]}, `; // Format: \"key: value\" và cách nhau bằng dấu phẩy\n  }\n\n  // Xóa dấu phẩy cuối cùng và thêm dòng này vào mảng output\n  outputText.push(rowText.slice(0, -2)); // Xóa dấu phẩy và khoảng trắng cuối cùng\n}\n\n// Gộp tất cả các dòng thành một chuỗi text lớn với phân cách\nconst resultText = outputText.join('\\n-----------------\\n');\n\n// Trả về dưới dạng text (output thành 1 item duy nhất)\nreturn [\n  {\n    json: {\n      text: resultText // Output là chuỗi text\n    }\n  }\n];\n"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        220,
        1460
      ],
      "id": "6408f460-ac6f-40c6-b51a-61d38fa1e8f9",
      "name": "Format_text"
    },
    {
      "parameters": {
        "operation": "update",
        "documentURL": "={{ $('Google Docs').first().json.id }}\n",
        "actionsUi": {
          "actionFields": [
            {
              "action": "insert",
              "text": "={{ $('Format_text').item.json.text }}"
            }
          ]
        }
      },
      "type": "n8n-nodes-base.googleDocs",
      "typeVersion": 2,
      "position": [
        820,
        1500
      ],
      "id": "d9e55f86-45c1-455f-a85e-49e619948226",
      "name": "Google Docs2",
      "credentials": {
        "googleDocsOAuth2Api": {
          "id": "Oh3rX4hHk2t0w7zT",
          "name": "Google Docs account"
        }
      }
    },
    {
      "parameters": {
        "assignments": {
          "assignments": [
            {
              "id": "e0f836e3-107a-4ebb-bef2-f6256d696e5b",
              "name": "sheetId",
              "value": "={{ $json.sheetId }}",
              "type": "number"
            },
            {
              "id": "8e56a0b5-71de-44eb-9385-39cb2ef5a768",
              "name": "title",
              "value": "={{ $json.title }}",
              "type": "string"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.set",
      "typeVersion": 3.4,
      "position": [
        -400,
        1460
      ],
      "id": "5da1f63a-75ef-491c-89af-a6fd586a52ff",
      "name": "Edit Fields1"
    },
    {
      "parameters": {
        "folderId": "19O3VWhgTUsQFe6RaJ1lEeiJKiC3VMAbr",
        "title": "={{ $('Edit Fields1').first().json.title }}"
      },
      "type": "n8n-nodes-base.googleDocs",
      "typeVersion": 2,
      "position": [
        620,
        1460
      ],
      "id": "aaef02ec-6ffe-414c-ab1a-3f2e82fa3665",
      "name": "Google Docs",
      "credentials": {
        "googleDocsOAuth2Api": {
          "id": "Oh3rX4hHk2t0w7zT",
          "name": "Google Docs account"
        }
      }
    },
    {
      "parameters": {
        "options": {}
      },
      "type": "n8n-nodes-base.splitInBatches",
      "typeVersion": 3,
      "position": [
        -540,
        840
      ],
      "id": "18998fbf-c0ce-45f3-a2b4-e1fde01c4c58",
      "name": "Loop Over Items"
    },
    {
      "parameters": {
        "dataType": "binary",
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.documentDefaultDataLoader",
      "typeVersion": 1,
      "position": [
        -80,
        1020
      ],
      "id": "b22bbd22-c948-491b-8d58-5d6de2b1682a",
      "name": "Default Data Loader"
    },
    {
      "parameters": {
        "chunkSize": 10000,
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.textSplitterRecursiveCharacterTextSplitter",
      "typeVersion": 1,
      "position": [
        -40,
        1160
      ],
      "id": "68976369-e468-45c1-a090-2b8cdb173900",
      "name": "Recursive Character Text Splitter"
    },
    {
      "parameters": {
        "model": "text-embedding-3-large",
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.embeddingsOpenAi",
      "typeVersion": 1.2,
      "position": [
        -400,
        1120
      ],
      "id": "51b81897-c073-45c5-96ae-1738eb3a1ac9",
      "name": "Embeddings OpenAI",
      "credentials": {
        "openAiApi": {
          "id": "6VL4MweiROPFfOYn",
          "name": "OpenAi account"
        }
      }
    },
    {
      "parameters": {
        "mode": "insert",
        "pineconeIndex": {
          "__rl": true,
          "value": "sample",
          "mode": "list",
          "cachedResultName": "sample"
        },
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.vectorStorePinecone",
      "typeVersion": 1,
      "position": [
        -300,
        840
      ],
      "id": "2147dff0-096e-47ca-a6cc-4859b1e96f2c",
      "name": "Pinecone Vector Store",
      "credentials": {
        "pineconeApi": {
          "id": "Tm6jKScBBGvHuhHS",
          "name": "PineconeApi account 2"
        }
      }
    },
    {
      "parameters": {
        "content": "## Trích xuất và format lại từng trang tính có trong spreadsheet\n",
        "height": 380,
        "width": 920
      },
      "type": "n8n-nodes-base.stickyNote",
      "position": [
        -500,
        1360
      ],
      "typeVersion": 1,
      "id": "a6d9697c-a241-4308-956f-021450e466a3",
      "name": "Sticky Note"
    },
    {
      "parameters": {
        "content": "## Update docs lên google drive\n",
        "height": 460,
        "width": 620
      },
      "type": "n8n-nodes-base.stickyNote",
      "position": [
        480,
        1320
      ],
      "typeVersion": 1,
      "id": "f3983606-8000-472f-bc7f-1b263a87d682",
      "name": "Sticky Note2"
    },
    {
      "parameters": {
        "content": "## Tải tất cả file docs trong folder",
        "height": 360,
        "width": 500
      },
      "type": "n8n-nodes-base.stickyNote",
      "position": [
        -1140,
        720
      ],
      "typeVersion": 1,
      "id": "1d852133-5f11-454b-9c88-b19223399e9e",
      "name": "Sticky Note3"
    },
    {
      "parameters": {
        "operation": "download",
        "fileId": {
          "__rl": true,
          "value": "={{ $json.id }}",
          "mode": "id"
        },
        "options": {}
      },
      "type": "n8n-nodes-base.googleDrive",
      "typeVersion": 3,
      "position": [
        -760,
        840
      ],
      "id": "743b32bf-d643-447e-85fd-45861acde5ab",
      "name": "Download_binary",
      "credentials": {
        "googleDriveOAuth2Api": {
          "id": "6MdI8zDc7dIfxEEU",
          "name": "Google Drive account"
        }
      }
    },
    {
      "parameters": {
        "resource": "fileFolder",
        "returnAll": true,
        "filter": {
          "folderId": {
            "__rl": true,
            "value": "19O3VWhgTUsQFe6RaJ1lEeiJKiC3VMAbr",
            "mode": "list",
            "cachedResultName": "attendance chatbot",
            "cachedResultUrl": "https://drive.google.com/drive/folders/19O3VWhgTUsQFe6RaJ1lEeiJKiC3VMAbr"
          }
        },
        "options": {}
      },
      "type": "n8n-nodes-base.googleDrive",
      "typeVersion": 3,
      "position": [
        -940,
        840
      ],
      "id": "4aa13e68-e109-41f7-8c27-e48f40550f25",
      "name": "Search__file",
      "credentials": {
        "googleDriveOAuth2Api": {
          "id": "6MdI8zDc7dIfxEEU",
          "name": "Google Drive account"
        }
      }
    },
    {
      "parameters": {
        "content": "## Insert file vào pinecone",
        "height": 600,
        "width": 800,
        "color": 4
      },
      "type": "n8n-nodes-base.stickyNote",
      "position": [
        -580,
        720
      ],
      "typeVersion": 1,
      "id": "24f06b14-5529-4e5d-ad0c-f1ccf4c477a1",
      "name": "Sticky Note4"
    },
    {
      "parameters": {
        "model": "gpt-4o",
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.lmChatOpenAi",
      "typeVersion": 1,
      "position": [
        400,
        700
      ],
      "id": "2fb0a9ed-8fc7-4007-8f5c-cdaafce78b73",
      "name": "OpenAI Chat Model2",
      "credentials": {
        "openAiApi": {
          "id": "6VL4MweiROPFfOYn",
          "name": "OpenAi account"
        }
      }
    },
    {
      "parameters": {
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.chatTrigger",
      "typeVersion": 1.1,
      "position": [
        400,
        440
      ],
      "id": "42fbe507-6f65-4027-a5a1-c259dbb90d08",
      "name": "When chat message received",
      "webhookId": "6b6103d2-5676-4a07-8c1d-811da9478c25"
    },
    {
      "parameters": {
        "model": "text-embedding-3-large",
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.embeddingsOpenAi",
      "typeVersion": 1.2,
      "position": [
        680,
        1020
      ],
      "id": "cc4ac5ef-b09d-4568-9806-2002ed0dc719",
      "name": "Embeddings OpenAI1",
      "credentials": {
        "openAiApi": {
          "id": "6VL4MweiROPFfOYn",
          "name": "OpenAi account"
        }
      }
    },
    {
      "parameters": {},
      "type": "@n8n/n8n-nodes-langchain.memoryBufferWindow",
      "typeVersion": 1.3,
      "position": [
        560,
        700
      ],
      "id": "23fd6eaa-d929-4188-87ae-2024de82aeba",
      "name": "Window Buffer Memory"
    },
    {
      "parameters": {
        "model": "gpt-4o",
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.lmChatOpenAi",
      "typeVersion": 1.1,
      "position": [
        1040,
        820
      ],
      "id": "f71250ab-a4e6-4984-b297-fae4dc21f81a",
      "name": "OpenAI Chat Model",
      "credentials": {
        "openAiApi": {
          "id": "6VL4MweiROPFfOYn",
          "name": "OpenAi account"
        }
      }
    },
    {
      "parameters": {
        "name": "data",
        "description": "gọi đến công cụ này mỗi khi trả lời câu hỏi của người dùng"
      },
      "type": "@n8n/n8n-nodes-langchain.toolVectorStore",
      "typeVersion": 1,
      "position": [
        760,
        620
      ],
      "id": "cb0acfd3-90e4-4582-94e9-6270e4fb9ef9",
      "name": "Answer questions with a vector store"
    },
    {
      "parameters": {
        "promptType": "define",
        "text": "={{ $json.chatInput }}",
        "options": {
          "systemMessage": "Bạn là một trợ lý nhân sự chuyên trả lời các câu hỏi chuyên về thông tin của nhân viên. Tất cả thông tin đều có trong vector store tools sẽ luôn tìm được câu trả lời trong dữ liệu cung cấp. Không bao giờ trả lời là không có thông tin\n\ndưới đây là một số ký hiệu có trong dữ liệu bạn sẽ đọc và thay thế thành dạng chữ hoặc nhận biết câu hỏi chính xác\n\nKPI trong dữ liệu có dạng 1.2 có nghĩ là 120% hoặc 0.8 có nghĩa là 80%\n\nLương thời gian cả ngày offline: x  \nLương nửa thời gian (buổi chiều): c  \nNghỉ lễ hưởng nguyên lương: L  \nĐi làm cả ngày thiếu giờ dưới 30ph: X-  \nLương thời gian cả ngày online: os  \nLương nửa thời gian (buổi chiều), buổi sáng nghỉ phép: cp  \nNghỉ không hưởng lương không phép: 0  \nNgày công 7 giờ: X-1  \nLương nửa thời gian (buổi sáng): s  \nNghỉ hưởng nguyên lương (phép, theo chế độ): N  \nLương làm thêm giờ: OT  \nKhông chấm công ra hoặc vào: -  \nLương nửa thời gian buổi sáng buổi chiều nghỉ phép: sp  \nNghỉ không lương có phép: 0P \n\n"
        }
      },
      "type": "@n8n/n8n-nodes-langchain.agent",
      "typeVersion": 1.7,
      "position": [
        620,
        440
      ],
      "id": "cd5d7072-ee16-4d74-84bc-fb217bde8219",
      "name": "AI Agent"
    },
    {
      "parameters": {
        "pineconeIndex": {
          "__rl": true,
          "value": "sample",
          "mode": "list",
          "cachedResultName": "sample"
        },
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.vectorStorePinecone",
      "typeVersion": 1,
      "position": [
        700,
        820
      ],
      "id": "c2bd21ff-5cb1-479e-bf09-c435dc3e96e9",
      "name": "Pinecone Vector Store1",
      "credentials": {
        "pineconeApi": {
          "id": "Tm6jKScBBGvHuhHS",
          "name": "PineconeApi account 2"
        }
      }
    },
    {
      "parameters": {
        "content": "## RAG AI Agent với Pinecone\n",
        "height": 880,
        "width": 1000
      },
      "type": "n8n-nodes-base.stickyNote",
      "position": [
        280,
        380
      ],
      "typeVersion": 1,
      "id": "6b12c193-59cc-42d7-ae0b-9a55418fd2c6",
      "name": "Sticky Note5"
    }
  ],
  "pinData": {},
  "connections": {
    "When clicking ‘Test workflow’": {
      "main": [
        [
          {
            "node": "Search__file",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Google Sheets": {
      "main": [
        [
          {
            "node": "Filter_ID",
            "type": "main",
            "index": 0
          }
        ],
        []
      ]
    },
    "Loop Over Items2": {
      "main": [
        [],
        [
          {
            "node": "Edit Fields1",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Code": {
      "main": [
        [
          {
            "node": "Loop Over Items2",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Edit Fields": {
      "main": [
        [
          {
            "node": "Code",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "HTTP Request": {
      "main": [
        [
          {
            "node": "Edit Fields",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Filter_ID": {
      "main": [
        [
          {
            "node": "Filter_columns",
            "type": "main",
            "index": 0
          }
        ],
        []
      ]
    },
    "Filter_columns": {
      "main": [
        [
          {
            "node": "Format_text",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Format_text": {
      "main": [
        [
          {
            "node": "Google Docs",
            "type": "main",
            "index": 0
          }
        ],
        []
      ]
    },
    "Edit Fields1": {
      "main": [
        [
          {
            "node": "Google Sheets",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Google Docs": {
      "main": [
        [
          {
            "node": "Google Docs2",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Google Docs2": {
      "main": [
        [
          {
            "node": "Loop Over Items2",
            "type": "main",
            "index": 0
          }
        ],
        []
      ]
    },
    "Loop Over Items": {
      "main": [
        [],
        [
          {
            "node": "Pinecone Vector Store",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Default Data Loader": {
      "ai_document": [
        [
          {
            "node": "Pinecone Vector Store",
            "type": "ai_document",
            "index": 0
          }
        ]
      ]
    },
    "Recursive Character Text Splitter": {
      "ai_textSplitter": [
        [
          {
            "node": "Default Data Loader",
            "type": "ai_textSplitter",
            "index": 0
          }
        ]
      ]
    },
    "Embeddings OpenAI": {
      "ai_embedding": [
        [
          {
            "node": "Pinecone Vector Store",
            "type": "ai_embedding",
            "index": 0
          }
        ]
      ]
    },
    "Pinecone Vector Store": {
      "main": [
        [
          {
            "node": "Loop Over Items",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Download_binary": {
      "main": [
        [
          {
            "node": "Loop Over Items",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Search__file": {
      "main": [
        [
          {
            "node": "Download_binary",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "OpenAI Chat Model2": {
      "ai_languageModel": [
        [
          {
            "node": "AI Agent",
            "type": "ai_languageModel",
            "index": 0
          }
        ]
      ]
    },
    "When chat message received": {
      "main": [
        [
          {
            "node": "AI Agent",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Embeddings OpenAI1": {
      "ai_embedding": [
        [
          {
            "node": "Pinecone Vector Store1",
            "type": "ai_embedding",
            "index": 0
          }
        ]
      ]
    },
    "Window Buffer Memory": {
      "ai_memory": [
        [
          {
            "node": "AI Agent",
            "type": "ai_memory",
            "index": 0
          }
        ]
      ]
    },
    "OpenAI Chat Model": {
      "ai_languageModel": [
        [
          {
            "node": "Answer questions with a vector store",
            "type": "ai_languageModel",
            "index": 0
          }
        ]
      ]
    },
    "Answer questions with a vector store": {
      "ai_tool": [
        [
          {
            "node": "AI Agent",
            "type": "ai_tool",
            "index": 0
          }
        ]
      ]
    },
    "Pinecone Vector Store1": {
      "ai_vectorStore": [
        [
          {
            "node": "Answer questions with a vector store",
            "type": "ai_vectorStore",
            "index": 0
          }
        ]
      ]
    }
  },
  "active": false,
  "settings": {
    "executionOrder": "v1"
  },
  "versionId": "3145a703-c87a-4cfb-81fa-d4cd9fc3813f",
  "meta": {
    "templateCredsSetupCompleted": true,
    "instanceId": "eadd110a3cd81ee1c3f6d9f99a44e6aff0a02530e4a09806c718935ac1617289"
  },
  "id": "INYRPlV3YRlD8ip6",
  "tags": []
}
```
