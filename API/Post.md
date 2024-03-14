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
        "hashtags" : [해시태그 배열] (null일 경우 []으로 빈 배열 전송)(ex ["#data" ,"#sample"]) or ([]),
        "postCategory" : "자유", "여행지", "음식" 중 하나
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
         - ***404 CONFLICT***
        
        ```jsonc
        존재하지 않는 카테고리입니다.
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
        "hashtags" : [해시태그 배열] (null일 경우 []으로 빈 배열 전송)(ex ["#data" ,"#sample"]) or ([]),
        "postCategory" : "자유", "여행지", "음식" 중 하나
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
        - ***404 CONFLICT***
        
        ```jsonc
        존재하지 않는 카테고리입니다.
        ```
        
- 게시글 상세 조회
    - **API** : `/api/post/{post_id}`
    - **Method : GET**    
    - **Response**
      
        - ***200 OK***
          
    ```jsonc
    {
        "postId" : 게시글 아이디,
        "nickname" : 게시글을 작성한 유저의 닉네임,
        "title" : 해당 게시글의 제목,
        "content" : 해당 게시글의 내용,
        "date" : 해당 게시글의 작성일자,
        "likeCount" : 해당 게시글의 좋아요 수,
        "viewCount" : 해당 게시글의 조회수,
        "position" : 해당 게시글의 등록된 위치,
        "photoDate" : 해당 게시글의 이미지 날짜,
        "hashtags" : [해당 게시글에 등록된 해시태그 리스트],
        "postCategory" : 해당 게시글의 카테고리,
        "commentCount" : 댓글 수,
        "likePostCount" : 게시글 좋아요 여부,
        "comments" : [
                        {
                            "commentId" : 댓글 아이디 ,
                            "nickname" : 댓글 작성자 닉네임 ,
                            "content" : 댓글 내용 ,
                            "createAt" : 댓글 작성일자,
                            "likeCount" : 댓글 좋아요 수,
                            "likeCommentCheck" : 댓글 좋아요 여부 
                        }
                        ]
    }
    ```
        
  - ***404 NOT FOUND***
        
    ```jsonc
    게시글을 찾을 수 없습니다.
    ```
- 게시글 좋아요
    - **API** : `/api/member/likedpost/{post_id}`
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
        
- 게시글 리스트 조회
    - **API** : `/api/post/list`
    - **Method : GET**
    - **Request**
       ```jsonc
       http://~/api/post/list?page=1
       ```
    - **Response**
      
        - ***200 OK***
          
        ```jsonc
        {
            "content": [
                {
                    "postId": 게시글 Id,
                    "nickname": 작성한 유저 닉네임,
                    "title": 게시글 제목,
                    "createAt": 작성일자,
                    "viewCount": 조회수,
                    "likeCount": 좋아요 수,
                    "hashtags": [해시태그 리스트],
                    "postCategory" : "자유", "여행지", "음식" 중 하나,
                    "CommentCount" : 댓글 수
                    
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
                "offset": 현재 펭지ㅣ의 게시글 시작 위치,
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

- 자신이 작성한 게시글 리스트 조회
    - **API** : `/api/member/post/list`
    - **Method : GET**
    - **Request**
       ```jsonc
       http://~/api/member/post/list?page=1
       ```
    - **Response**
      
        - ***200 OK***
          
        ```jsonc
        {
            "content": [
                {
                    "postId": 게시글 Id,
                    "nickname": 작성한 유저 닉네임,
                    "title": 게시글 제목,
                    "createAt": 작성일자,
                    "viewCount": 조회수,
                    "likeCount": 좋아요 수,
                    "hashtags": [해시태그 리스트],
                    "postCategory" : "자유", "여행지", "음식" 중 하나,
                    "CommentCount" : 댓글 수
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
                "offset": 현재 펭지ㅣ의 게시글 시작 위치,
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

  - 베스트 게시글 리스트 조회
    - **API** : `/api/post/list/best`
    - **Method : GET**
    - **Response**
      
        - ***200 OK***
          
        ```jsonc
        {
            [
                {
                    "postId": 게시글 아이디,
                    "nickname": 작성자 닉네임,
                    "title": 게시글 제목,
                    "createAt": 게시글 작성일자,
                    "viewCount": 조회수,
                    "likeCount": 좋아요 수,
                    "hashtags": [해시태그 리스트],
                    "postCategory": 게시글 카테고리,
                    "commentCount": 댓글수
                },
                {
                },
                {
                }
            
            ]
        }  
        ```
- 게시글을 작성한 유저 닉네임 검색
    - **API** : `/api/post/nickname`
    - **Method : GET**
    - **Request**
       ```jsonc
       http://~/api/post/list?page=0?nickname="nickname" ("" 제외하고 입력)
       ```
    - **Response**
      
        - ***200 OK***
          
        ```jsonc
        {
            "content": [
                {
                    "postId": 게시글 Id,
                    "nickname": 작성한 유저 닉네임,
                    "title": 게시글 제목,
                    "createAt": 작성일자,
                    "viewCount": 조회수,
                    "likeCount": 좋아요 수,
                    "hashtags": [해시태그 리스트],
                    "postCategory" : "자유", "여행지", "음식" 중 하나,
                    "CommentCount" : 댓글 수
                    
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
                "offset": 현재 펭지ㅣ의 게시글 시작 위치,
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
- 게시글 제목 검색
    - **API** : `/api/post/title`
    - **Method : GET**
    - **Request**
       ```jsonc
       http://~/api/post/list?page=0?title="title" ("" 제외하고 입력)
       ```
    - **Response**
      
        - ***200 OK***
          
        ```jsonc
        {
            "content": [
                {
                    "postId": 게시글 Id,
                    "nickname": 작성한 유저 닉네임,
                    "title": 게시글 제목,
                    "createAt": 작성일자,
                    "viewCount": 조회수,
                    "likeCount": 좋아요 수,
                    "hashtags": [해시태그 리스트],
                    "postCategory" : "자유", "여행지", "음식" 중 하나,
                    "CommentCount" : 댓글 수
                    
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
                "offset": 현재 펭지ㅣ의 게시글 시작 위치,
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
- 게시글 내용 검색
    - **API** : `/api/post/content`
    - **Method : GET**
    - **Request**
       ```jsonc
       http://~/api/post/list?page=0?content="content" ("" 제외하고 입력)
       ```
    - **Response**
      
        - ***200 OK***
          
        ```jsonc
        {
            "content": [
                {
                    "postId": 게시글 Id,
                    "nickname": 작성한 유저 닉네임,
                    "title": 게시글 제목,
                    "createAt": 작성일자,
                    "viewCount": 조회수,
                    "likeCount": 좋아요 수,
                    "hashtags": [해시태그 리스트],
                    "postCategory" : "자유", "여행지", "음식" 중 하나,
                    "CommentCount" : 댓글 수
                    
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
                "offset": 현재 펭지ㅣ의 게시글 시작 위치,
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
- 게시글 리스트 조회
    - **API** : `/api/post/hashtag`
    - **Method : GET**
    - **Request**
       ```jsonc
       http://~/api/post/list?page=0?hashtag="#hashtag" ("" 제외하고 입력, #은 %23으로 인코딩 해서 사용해야함)
       ```
    - **Response**
      
        - ***200 OK***
          
        ```jsonc
        {
            "content": [
                {
                    "postId": 게시글 Id,
                    "nickname": 작성한 유저 닉네임,
                    "title": 게시글 제목,
                    "createAt": 작성일자,
                    "viewCount": 조회수,
                    "likeCount": 좋아요 수,
                    "hashtags": [해시태그 리스트],
                    "postCategory" : "자유", "여행지", "음식" 중 하나,
                    "CommentCount" : 댓글 수
                    
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
                "offset": 현재 펭지ㅣ의 게시글 시작 위치,
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

