# API 명세서(회원가입/로그인/교재제작/퀴즈제작)

**https://www.notion.so/API-2a333b8ab6f680f59d17e1a89308e23e**

# File API
**- 인증:** ❌  

### 1. POST /api/file (파일 업로드)

- 요청
```json
{
  "file": "<업로드할 실제 파일>",
  "category": "user_profile | textbook_cover | page_content | main_banner | other",
  "id": "3"
}
```

- 응답(201)
```json
{
  "fileId": 1,
  "url": "http://localhost:3000/files/sample.jpg"
}
```

### 2. GET /api/file/by-target (category + id 조합으로 최신 파일 1개 조회)

- 요청
```json
{
  "category": "user_profile",
  "id": "3"
}
```
- id 생략 예시 (main_banner)
```json
{
  "category": "main_banner"
}
```

- 응답 (200 OK)
```json
{
  "fileId": 1,
  "url": "http://localhost:3000/files/sample.jpg"
}
```

- 응답 (404 Not Found)
```json
{
  "message": "해당 category/id에 해당하는 파일이 없습니다."
}
```
### 3. GET /api/file/{fileId} (file_id(PK)로 단일 파일 정보 조회)

- 요청
```json
{
  "fileId": 1
}
```

- 응답 (200 OK)
```json
{
  "fileId": 1,
  "url": "http://localhost:3000/files/sample.jpg"
}
```

- 응답 (404 Not Found)
```json
{
  "message": "파일을 찾을 수 없습니다."
}
```

### 4. DELETE /api/file/{fileId} (파일 삭제)

- 요청
```json
{
  "fileId": 1
}
```

- 응답 (200 OK)
```json
{
  "message": "삭제되었습니다.",
  "fileId": 1
}
```

- 응답 (404 Not Found)
```json
{
  "message": "파일을 찾을 수 없습니다."
}
```

### category 값 설명(JSON)
```json
{
  "user_profile": {
    "description": "사용자 프로필 이미지",
    "id": "user_id (예: 3)"
  },
  "textbook_cover": {
    "description": "교재 표지 이미지",
    "id": "textbook_id"
  },
  "page_content": {
    "description": "교재 페이지 내부 이미지",
    "id": "page_id"
  },
  "main_banner": {
    "description": "메인 배너 이미지",
    "id": "없음 (id 미전송)"
  },
  "other": {
    "description": "기타 용도",
    "id": "필요 시 전송"
  }
}
