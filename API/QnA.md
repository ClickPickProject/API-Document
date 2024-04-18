- 질문 작성
    - **API** : `/api/member/question`
    - **Method : POST**
    - **Body :  raw (json)**
    - **Request**
    
    ```jsonc
    {
        "title" : 질문의 제목(not null),
        "content" : 질문의 내용(not null),
        "lock" : 공개 여부 (공개 시 "UNLOCK", 비공개시 "LOCKED"),(not null)
    }
    ```
    
    - **Response**
      
        - ***200 OK***
          
        ```jsonc
        질문을 등록하였습니다.
        ```
        
        - ***404 NOT FOUND***
        
        ```jsonc
        존재하지 않는 이메일(아이디) 입니다.
        ```

- 질문 삭제
    - **API** : `/api/member/question/{question_id}`
    - **Method : DELETE**
    - **Response**
      
        - ***200 OK***
          
        ```jsonc
        질문을 삭제하였습니다.
        ```
        
        - ***403 FORBIDDEN***
        
        ```jsonc
        사용자가 삭제할 수 없는 질문입니다.
        ```
- 질문 수정
    - **API** : `/api/member/question/{question_id}`
    - **Method : Post**
    - **Body :  raw (json)**
    - **Request**
    
    ```jsonc
    {
        "title" : 수정하고자 하는 제목,
        "content" : 수정하고자 하는 내용,
        "lock" : 공개 여부 (공개 시 "UNLOCK", 비공개시 "LOCKED"),(not null)
    }
    ```
    
    - **Response**
      
        - ***200 OK***
          
        ```jsonc
        질문이 수정되었습니다.
        ```
        
        - ***403 FORBIDDEN***
        
        ```jsonc
        사용자가 수정할 수 없는 질문입니다.
        ```

- 답변 작성
    - **API** : `/api/admin/{question_id}/answer`
    - **Method : POST**
    - **Body :  raw (json)**
    - **Request**
    
    ```jsonc
    {
        "title" : 답변의 제목(not null),
        "content" : 답변의 내용(not null),
    }
    ```
    
    - **Response**
      
        - ***200 OK***
          
        ```jsonc
        답변을 작성하였습니다.
        ```
        
        - ***404 NOT FOUND***
        
        ```jsonc
        질문이 존재하지 않습니다.
        ```

- 답변 및 추가 질문/답변 삭제
    - **API** : `/api/admin/answer/{answer_id}`
    - **Method : DELETE**
    - **Response**
      
        - ***200 OK***
          
        ```jsonc
        답변을 삭제하였습니다.
        ```
        
        - ***403 FORBIDDEN***
        
        ```jsonc
        삭제할 수 없는 답변입니다.
        ```
- 답변 및 추가 질문/답변 수정
    - **API** : `/api/admin/answer/{answer_id}`
    - **Method : Post**
    - **Body :  raw (json)**
    - **Request**
    
    ```jsonc
    {
        "title" : 수정하고자 하는 제목,
        "content" : 수정하고자 하는 내용,
    }
    ```
    
    - **Response**
      
        - ***200 OK***
          
        ```jsonc
        답변을 수정하였습니다.
        ```
        
        - ***403 FORBIDDEN***
        
        ```jsonc
        사용자가 수정할 수 없는 답변입니다.
        ```
        
- 추가 질문/답변 작성
    - **API** : `/api/member/{question_id}/{answer_id}/reanswer`
    - **Method : POST**
    - **Body :  raw (json)**
    - **Request**
    
    ```jsonc
    {
        "title" : 답변의 제목(not null),
        "content" : 답변의 내용(not null),
    }
    ```
    
    - **Response**
      
        - ***200 OK***
          
        ```jsonc
        추가 질문을 작성하였습니다. (질문 작성자)
        or
        추가 답변을 작성하였습니다. (어드민)
        ```
        
        - ***403 FORBIDDEN***
        
        ```jsonc
        본인이 작성한 질문이 아닙니다.
        ```
        
- 질문 상세 조회
    - **API** : `/api/question/{question_id}`
    - **Method : GET**
    - **Body :  raw (json)**
    - **Request**
    - **Response**
      
        - ***200 OK***
          
        ```jsonc
        {
            "questionId" : 질문 아이디,
            "userId" : 작성자 아이디,
            "nickname" : 작성자 닉네임,
            "title" : 질문 제목,
            "content" : 질문 내용,
            "status" : 질문 상태 표시(COMPLETE, AWAITING),
            "date" : 질문 작성 날짜,
            "profileUrl" : 프로필 url
            "answer" : [ (답변 없으면 빈리스트 반환 [])
                "answerId" : 답변 아이디,
                "questionId" : 답변이 달린 질문 아이디,
                "adminId" : 답변 작성 관리자 아이디,
                "nickname" : ADMIN(고정),
                "title" : 답변 제목,
                "content" : 답변 내용,
                "date" : 답변 날짜,
                "profileUrl" : 프로필 url
            ]
        
        }
        
        ```
        
        - ***404 NOT FOUND***
        
        ```jsonc
        존재하지 않는 질문입니다.
        ```

        - ***403 FORBIDDEN***
        
        ```jsonc
        비공개된 질문입니다..
        ```

- 질문 리스트 조회
    - **API** : `/api/question/list`
    - **Method : GET**
    - **Request**
       ```jsonc
       http://~/api/question/list?page=1 (0번일 경우 page=0 생략가능)
       ```
    - **Response**
      
        - ***200 OK***
          
        ```jsonc
        {
            "content": [
                {
                    "questionId" : 질문 Id,
                    "userId" : 작성한 유저 아이디,
                    "nickname" : 작성한 유저 닉네임,
                    "title" : 질문 제목,
                    "createAt" : 잘성 날짜,
                    "status" :  질문 상태 표시(COMPLETE, AWAITING),
                    "profileUrl" : 프로필 url    
                },

                ...,
  
            ],
            "pageable": {
                "pageNumber": 현재 페이지 ,
                "pageSize": 한 페이지당 가능한 게시글 수,
                "sort": {
                    "empty": 정렬 정보가 비어있는지 여부,
                    "sorted": 페이징 결과 정렬 여부,
                    "unsorted": 페이징 결과 정렬 여부,
                    },
                "offset": 현재 페이지의 게시글 시작 위치,
                "paged": 페이징 여부,
                "unpaged": 페이징 여부
                },
            "last": 현재 페이지가 마지막 페이지 인지,
            "totalPages": 총 페이지의 개수,
            "totalElements": 게시글 총 개수,
            "first": 첫 게시글인지 여부,
            "size": 페이지 당 표시 가능한 게시글 수,
            "number": 현재 페이지 번호,
            "sort": {
                "empty": 정렬 정보가 비어 있는지 여부,
                "sorted": 페이징 결과 정렬 여부,
                "unsorted": 페이징 결과 정렬 여부
            },
            "numberOfElements": 현재 페이지에 포함된 게시글의 수,
            "empty": 현재 페이지의 결과가 비어 있는지 여부    
        }
        ```
        
- 작성한 질문 리스트 조회
    - **API** : `/api/member/question/list`
    - **Method : GET**
    - **Request**
       ```jsonc
       http://~/api/member/question/list?page=1 (0번일 경우 page=0 생략가능)
       ```
    - **Response**
      
        - ***200 OK***
          
        ```jsonc
        {
            "content": [
                {
                    "questionId" : 질문 Id,
                    "userId" : 작성한 유저 아이디,
                    "nickname" : 작성한 유저 닉네임,
                    "title" : 질문 제목,
                    "createAt" : 잘성 날짜,
                    "status" :  질문 상태 표시(COMPLETE, AWAITING),
                    "profileUrl" : 프로필 url
                    
                },

                ...,
  
            ],
            "pageable": {
                "pageNumber": 현재 페이지 ,
                "pageSize": 한 페이지당 가능한 게시글 수,
                "sort": {
                    "empty": 정렬 정보가 비어있는지 여부,
                    "sorted": 페이징 결과 정렬 여부,
                    "unsorted": 페이징 결과 정렬 여부,
                    },
                "offset": 현재 페이지의 게시글 시작 위치,
                "paged": 페이징 여부,
                "unpaged": 페이징 여부
                },
            "last": 현재 페이지가 마지막 페이지 인지,
            "totalPages": 총 페이지의 개수,
            "totalElements": 게시글 총 개수,
            "first": 첫 게시글인지 여부,
            "size": 페이지 당 표시 가능한 게시글 수,
            "number": 현재 페이지 번호,
            "sort": {
                "empty": 정렬 정보가 비어 있는지 여부,
                "sorted": 페이징 결과 정렬 여부,
                "unsorted": 페이징 결과 정렬 여부
            },
            "numberOfElements": 현재 페이지에 포함된 게시글의 수,
            "empty": 현재 페이지의 결과가 비어 있는지 여부    
        }
        ```
                
- 상태별 질문 리스트 조회
    - **API** : `/api/question/list/{status}`
    - **Method : GET**
    - **Request**
       ```jsonc
       http://~/api/question/list/AWAITING?page=1 (0번일 경우 page=0 생략가능)
       or
       http://~/api/question/list/COMPLETE?page=1 (0번일 경우 page=0 생략가능)
       ```
    - **Response**
      
        - ***200 OK***
          
        ```jsonc
        {
            "content": [
                {
                    "questionId" : 질문 Id,
                    "userId" : 작성한 유저 아이디,
                    "nickname" : 작성한 유저 닉네임,
                    "title" : 질문 제목,
                    "createAt" : 잘성 날짜,
                    "status" :  질문 상태 표시(COMPLETE, AWAITING),
                    "profileUrl" : 프로필 url
                    
                },

                ...,
  
            ],
            "pageable": {
                "pageNumber": 현재 페이지 ,
                "pageSize": 한 페이지당 가능한 게시글 수,
                "sort": {
                    "empty": 정렬 정보가 비어있는지 여부,
                    "sorted": 페이징 결과 정렬 여부,
                    "unsorted": 페이징 결과 정렬 여부,
                    },
                "offset": 현재 페이지의 게시글 시작 위치,
                "paged": 페이징 여부,
                "unpaged": 페이징 여부
                },
            "last": 현재 페이지가 마지막 페이지 인지,
            "totalPages": 총 페이지의 개수,
            "totalElements": 게시글 총 개수,
            "first": 첫 게시글인지 여부,
            "size": 페이지 당 표시 가능한 게시글 수,
            "number": 현재 페이지 번호,
            "sort": {
                "empty": 정렬 정보가 비어 있는지 여부,
                "sorted": 페이징 결과 정렬 여부,
                "unsorted": 페이징 결과 정렬 여부
            },
            "numberOfElements": 현재 페이지에 포함된 게시글의 수,
            "empty": 현재 페이지의 결과가 비어 있는지 여부    
        }
        ```
        - ***404 NOT FOUND***
        
        ```jsonc
        잘못된 요청입니다.
        ```
