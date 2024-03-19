## Comment API List

- 댓글 작성
    - **API** : `/api/member/comment`
    - **Method : POST**
    - **Body :  raw (json)**
    - **Request**
    
    ```jsonc
    {
        "postId" : 작성하고자 하는 댓글의 게시글 id,
        "content" : 댓글 내용
    }
    ```
    
    - **Response**
      
        - ***200 OK***
          
        ```jsonc
        댓글이 등록되었습니다.
        ```
        
        - ***404 NOT_FOUND***
        
        ```jsonc
        존재하지 않는 게시글입니다.
        ```
        - ***403 FORBIDDEN***
        
        ```jsonc
        회원만 가능한 기능입니다.
        ```


- 댓글 삭제
    - **API** : `/api/member/comment/{comment_id}`
    - **Method : DELETE**
    - **Request**
    
    ```jsonc
      comment_id : 삭제하고자 하는 댓글 아이디
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
- 댓글 수정
    - **API** : `/api/member/comment/{comment_id}`
    - **Method : Post**
    - **Body :  raw (json)**
    - **Request**
    
    ```jsonc
    {
        "postId" : 작성하고자 하는 댓글의 게시글 id,
        "content" : 댓글 내용
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
        
- 댓글 좋아요
    - **API** : `/api/member/likedcomment/{comment_id}`
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
        댓글을 찾을 수 없습니다.
        ```
- 대댓글 작성
    - **API** : `/api/member/recomment`
    - **Method : POST**
    - **Body :  raw (json)**
    - **Request**
    
    ```jsonc
    {
        "parentcommentId" : 대댓글을 달고자 하는 댓글 id,
        "postId" : 작성하고자 하는 댓글의 게시글 id,
        "content" : 댓글 내용
    }
    ```
    
    - **Response**
      
        - ***200 OK***
          
        ```jsonc
        댓글이 등록되었습니다.
        ```
        
        - ***404 404 NOT_FOUND***
        
        ```jsonc
        존재하지 않는 게시글입니다.
        or
        상위 댓글을 찾을 수 없습니다.
        ```
        - ***403 FORBIDDEN***
        
        ```jsonc
        회원만 가능한 기능입니다.
        ```
