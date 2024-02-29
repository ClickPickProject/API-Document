## Post API List

- 게시글 작성
    - **API** : `/api/post`
    - **Method : POST**
    - **Body :  raw (json)**
    - **Request**
    
    ```jsonc
    {
    	"userId" : user의 ID (e-mail 형식)(not null),
    	"title" : 게시글의 제목(not null),
    	"content" : 게시글의 내용(not null),
    	"position" : 위치 정보(null일 경우 ""으로 전송),
    	"hashtag" : 해시태그(null일 경우 ""으로 전송)(ex #data #sample)
    }
    ```
    
    - **Response**
      
        - ***200 OK***
          
        ```jsonc
        게시글이 등록되었습니다.
        ```
        
        - ***404 CONFLICT***
        
        ```jsonc
        존재하지 않는 이메일(아이디) 입니다.
        ```
