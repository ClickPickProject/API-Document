## Post API List

- 게시글 작성
    - **API** : `/api/member/post`
    - **Method : POST**
    - **Body :  raw (json)**
    - **Request**
    
    ```jsonc
    {
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

- 게시글 삭제
    - **API** : `/api/member/post/{post_id}`
    - **Method : DELETE**
    - **Request**
    
    ```jsonc
    post_id : 삭제하고자 하는 게시글 아이디
    ```
    
    - **Response**
      
        - ***200 OK***
          
        ```jsonc
        삭제가 완료되었습니다.
        ```
        
        - ***403 FORBIDDEN***
        
        ```jsonc
        사용자가 삭제할 수 없는 게시글입니다.
        ```
- 게시글 수정
    - **API** : `/api/member/post/{post_id}`
    - **Method : Post**
    - **Body :  raw (json)**
    - **Request**
    
    ```jsonc
    {
        "title" : 수정하고자 하는 제목,
        "content" : 수정하고자 하는 내용,
        "position" : 위치 정보(null일 경우 ""으로 전송),
        "hashtag" : 해시태그(null일 경우 ""으로 전송)
    }
    ```
    
    - **Response**
      
        - ***200 OK***
          
        ```jsonc
        수정이 완료되었습니다.
        ```
        
        - ***403 FORBIDDEN***
        
        ```jsonc
        사용자가 수정할 수 없는 게시글입니다.
        ```
- 게시글 상세 조회
    - **API** : `/api/post/{post_id}`
    - **Method : GET**    
    - **Response**
      
        - ***200 OK***
          
    ```jsonc
    {
        "nickname" : 게시글을 작성한 유저의 닉네임,
        "title" : 해당 게시글의 제목,
        "content" : 해당 게시글의 내용,
        "date" : 해당 게시글의 작성일자,
        "likeCount" : 해당 게시글의 좋아요 수,
        "viewCount" : 해당 게시글의 조회수,
        "position" : 해당 게시글의 등록된 위치,
        "photoDate" : 해당 게시글의 이미지 날짜,
        "hashtags" : 해당 게시글에 등록된 해시태그 리스트
    }
    ```
        
  - ***404 NOT FOUND***
        
    ```jsonc
    게시글을 찾을 수 없습니다.
    ```
- 게시글 좋아요
    - **API** : `/api/likedpost/{post_id}/{user_id}`
    - **Method : GET**    
    - **Response**
      
        - ***200 OK***
          
        ```jsonc
        해당 게시글을 좋아요 하였습니다. (좋아요 시)
        좋아요를 취소하였습니다. (좋아요 취소 시)
        ```
        
        - ***403 FORBIDDEN***
        
        ```jsonc
        회원만 가능한 기능입니다.
        ```

        - ***404 NOT FOUND***
        
        ```jsonc
        게시글을 찾을 수 없습니다.
        ```
        
