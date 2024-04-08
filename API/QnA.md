- 질문 작성
    - **API** : `/api/member/question`
    - **Method : POST**
    - **Body :  raw (json)**
    - **Request**
    
    ```jsonc
    {
        "title" : 질문의 제목(not null),
        "content" : 질문의 내용(not null),
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

- 답변 삭제
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
- 답변 수정
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
            "answer" : [ (답변 없으면 빈리스트 반환 [])
                "answerId" : 답변 아이디,
                "questionId" : 답변이 달린 질문 아이디,
                "adminId" : 답변 작성 관리자 아이디,
                "nickname" : ADMIN(고정),
                "title" : 답변 제목,
                "content" : 답변 내용,
                "date" : 답변 날짜
            ]
        
        }
        
        ```
        
        - ***404 NOT FOUND***
        
        ```jsonc
        존재하지 않는 질문입니다.
        ```
        

