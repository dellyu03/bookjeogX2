# 📚 북적북적
> Made by : dellyu03  
> [인프런 워밍업 클럽 2기 백엔드 프로젝트 과정](https://www.inflearn.com/course/offline/warmup-club-2-be-bk#program) 미니 프로젝트

<br>

## 📕 프로젝트 소개
- 독서 습관을 만들고 싶지만 혼자서는 힘들었던 사람들을 위해 만든 프로젝트
- 책을 선정해서 목표를 정해서 읽고 다른 사람들과 감상을 공유하는 사이트
- 사용자는 읽고자 하는 책과 책 읽기 계획을 정하여 다른 사람들과 공유할 수 있다.
- 각 목표 완수시마다 책에 대한 감상이나 내용정리를 적고 다른 사람들과 공유할 수 있다.
- 다른 사용자의 글을 구경할 수 있고 좋아요와 댓글을 달 수 있다.

<br>

## 📗 사용 기술 스택

### 🖥 Language

<img src="https://img.shields.io/badge/Kotlin-7F52FF?style=for-the-badge&logo=kotlin&logoColor=white">




### 🛠 FrameWork

<img src="https://img.shields.io/badge/Spring boot-6DB33F?style=for-the-badge&logo=springboot&logoColor=white"> 

<br>

## 프로젝트 ERD 구성

<img src = "./img/erd.png">

## API 설계

## I. User

### 1. 회원 가입
- URL : /api/v1/signup
- Method : POST
- Headers : Content-type: application/json

- Body
```json
{
    "username": "Yoo Seung Hwan",
    "password": "password123",
    "email": "seunghwan081@gmail.com",
    "nickname": "dellyu03",
    "signupDate": "2024-10-07"
}
```

- Response
```json
{
  "message": "User created successfully",
  "userId": "string"
}

```

### 2. 로그인
- URL : /api/v1/signin
- Method : POST
- Headers : Content-type: application/json

- Body
```json
{
  "username": "Yoo Seung Hwan",
  "password": "password123"
}
```

- Response
```json
{
  "message": "Login successful",
  "token": "string"
}
```

## II. Book
### 1. 도서 등록
- URL : /api/v1/books
- Method : POST
- Headers : Content-type: application/json

- Body
```json
{
  "bookId": "12345",
  "title": "Example Book Title",
  "author": "Author Name",
  "publisher": "Publisher Name",
  "rating": 4.5,
  "registrationDate": "2024-10-07",
  "modificationDate": "2024-10-07"
}
```

- Response
```json
{
  "message": "Book registered successfully",
  "bookId": "12345"
}
```

### 2. 도서 정보 조회
- URL : /api/v1/books/{bookId}
- Method : GET
- Params 
    - bookId : 조회할 책의 Id
- Headers : Authorization: Bearer `<token>` - 유저 개별 토큰


- Response
```json
{
  "bookId": "12345",
  "title": "Example Book Title",
  "author": "Author Name",
  "publisher": "Publisher Name",
  "rating": 4.5,
  "registrationDate": "2024-10-07",
  "modificationDate": "2024-10-07"
} 

```

### 3. 책 선택
- URL : /api/v1/books/{bookId}/select
- Method : GET
- Params 
    - userId : 책을 선택하는 사용자의 Id
    - bookId : 선택할 책의 Id
- Headers : Authorization: Bearer `<token>` - 유저 개별 토큰, Content-Type:application.json

- Response
```json
{
  "message": "Book selected successfully",
  "userId": "user_12345",
  "bookId": "book_67890",
  "selectedDate": "2024-10-07"
}
```

## III. Goal
### 1. 목표 설정
- URL : /api/v1/books/{bookId}/goals
- Method : POST
- Params : bookId - 관련 목표를 생성할 책의 ID
- Headers : Content-Type: apllication/json, Authorization: Bearer`<token>`
- Body
```json
{
  "userId": "user_12345",
  "goals": [
    {
      "goalId": "goal_1",
      "description": "Read 50 pages",
      "creationDate": "2024-10-07",
      "modificationDate": "2024-10-07",
      "completionDate": null,
      "isCompleted": false,
      "completionMessage": null,
      "content": "This is the content of the goal."
    }
  ]
}
```

- Response
```json
{
  "message": "Goals set successfully",
  "userId": "user_12345",
  "bookId": "book_67890",
  "goals": [
    {
      "goalId": "goal_1",
      "description": "Read 50 pages",
      "creationDate": "2024-10-07",
      "modificationDate": "2024-10-07",
      "completionDate": null,
      "isCompleted": false,
      "completionMessage": null,
      "content": "This is the content of the goal."
    }
  ]
}

```

### 2. 목표 조회
- URL : /api/v1/books/{bookId}/goals
- Method : GET
- Params : userId-조회할 사용자 ID, bookId-조회할 책의 Id
- Headers :  Authorization: Bearer`<token>`

- Response
```json
{
  "userId": "user_12345",
  "bookId": "book_67890",
  "goals": [
    {
      "goalId": "goal_1",
      "description": "Read 50 pages",
      "creationDate": "2024-10-07",
      "modificationDate": "2024-10-08",
      "completionDate": "2024-11-01",
      "isCompleted": true,
      "completionMessage": "Finished reading 50 pages!",
      "content": "This is the content of the goal."
    }
  ]
}


```

## IV. 댓글
### 1. 생성
- URL : /api/v1/goals{goalId}/comments
- Method : POST
- Params : goalId - 댓글을 달 목표의 Id 

- Headers : Content-type: apllication/josn, Authorization: Bearer`<token>`
- Body 
```json
{
  "userId": "user_12345",
  "comment": "This is my comment on this goal."
}
```

- Response
```json
{
  "message": "Comment created successfully.",
  "commentId": "comment_67890",
  "goalId": "goal_1",
  "userId": "user_12345",
  "comment": "This is my comment on this goal.",
  "creationDate": "2024-10-07"
}
```

### 2. 수정
- URL : /api/v1/goals/{goalId}/comments/{commentId}
- Method: PUT
- Params : goalId - 댓글이 달린 목표의 ID, commentId : 수정할 댓글의 Id
- Headers : Content-Type : application/json, Authorization: Bearer `<token>`

- Body
```json
{
  "userId": "user_12345",
  "comment": "This is my updated comment on this goal."
}

```

- Response
```json
{
  "message": "Comment updated successfully.",
  "commentId": "comment_67890",
  "goalId": "goal_1",
  "userId": "user_12345",
  "comment": "This is my updated comment on this goal.",
  "modificationDate": "2024-10-08"
}
```

### 3. 삭제
- URL : /api/v1/goals/{goalId}/comments/{commentId}
- Method : DELETE
- Params : goalId-댓글이 달린 목표의 ID, commentId-삭제할 댓글의 ID
- Headers : Authorization : Bearer `<token>`
- Response
```json
{
  "message": "Comment deleted successfully.",
  "commentId": "comment_67890",
  "goalId": "goal_1"
}

```