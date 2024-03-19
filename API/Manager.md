## Admin Api List

- 공지사항 작성
    - **API** : `/api/admin/notice`
    - **Method : POST**
    - **Body :  raw (json)**
    - **Request**
    
    ```jsonc
    {
    "title" : "공지사항입니다.",
    "content" : "공지입니다."
    }
    ```
    
    - **Response**
        - ***200 OK***
        
        ```jsonc
        공지사항이 등록되었습니다.
        ```


- 공지사항 수정
    - **API** : `/api/admin/notice/{noticeId}`
    - **Method : DELETE**
    - **Body :  raw (json)**
    - **Request**
    
    ```jsonc
    noticeId : 삭제하고자 하는 공지사항 아이디
    ```
    
    - **Response**
        - ***200 OK***
        
        ```jsonc
        수정이 완료되었습니다.
        ```


- 공지사항 삭제
    - **API** : `/api/admin/notice`
    - **Method : POST**
    - **Body :  raw (json)**
    - **Request**
    
    ```jsonc
    {
    noticeId : 삭제하고자 하는 공지사항 아이디
    }
    ```
    
    - **Response**
        - ***200 OK***
        
        ```jsonc
        공지사항 삭제가 완료되었습니다. 
        ```

