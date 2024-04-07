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
- 질문 수정
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

        

