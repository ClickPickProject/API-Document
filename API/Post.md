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
        "xPosition" : 지도 API를 통해 얻은 x 좌표 (소수점 형태 (double), null일 경우 ""으로 전송),
        "yPosition" : 지도 API를 통해 얻은 y 좌표 (소수점 형태 (double), null일 경우 ""으로 전송),
        "hashtags" : [해시태그 배열] (null일 경우 []으로 빈 배열 전송)(ex ["#data" ,"#sample"]) or ([]),
        "postCategory" : "자유", "여행지", "음식" 중 하나,
        "thumbnailImage" : 해당 게시글의 썸네일 이미지 이름,
        "imageNames" : [해당 게시글의 사진 이름 리스트] (게시글 사진 추가 시 반환되는 url에서 images 뒤의 파일명(확장자 포함))  
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
        "xPosition" : 지도 API를 통해 얻은 x 좌표 (소수점 형태 (double), null일 경우 ""으로 전송),
        "yPosition" : 지도 API를 통해 얻은 y 좌표 (소수점 형태 (double), null일 경우 ""으로 전송),
        "hashtags" : [해시태그 배열] (null일 경우 []으로 빈 배열 전송)(ex ["#data" ,"#sample"]) or ([]),
        "postCategory" : "자유", "여행지", "음식" 중 하나,
        "thumbnailImage" : 해당 게시글의 썸네일 이미지 이름,
        "updateImageNames" : [변경된 해당 게시글의 사진 이름 리스트] (게시글 사진 추가 시 반환되는 url에서 images 뒤의 파일명(확장자 포함))  
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
        "profileUrl": 프로필 url
        "comments" : [
                        {
                            "commentId" : 댓글 아이디 ,
                            "nickname" : 댓글 작성자 닉네임 ,
                            "content" : 댓글 내용 ,
                            "createAt" : 댓글 작성일자,
                            "likeCount" : 댓글 좋아요 수,
                            "likeCommentCheck" : 댓글 좋아요 여부,
                            "commentStatus" : 삭제 되었으며 "DELETE", 아니라면 "LIVE",
                            "profileUrl": 프로필 url,
                            "recommentList" : [ 
                                                "commentId" : 대댓글 아이디,
                                                "nickname" : 대댓글 작성자 닉네임,
                                                "content" : 대댓글 내용,
                                                "createAt" : 작성 날자,
                                                "likeCount" : 대댓글 좋아요 수,
                                                "likeCommentCheck" : 대댓글 좋아요 여부,
                                                "profileUrl": 프로필 url,
                                                "parentId" : 부모 댓글 id
                                                ]
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
                    "CommentCount" : 댓글 수,
                    "profileUrl": 프로필 url
                    
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
                    "commentCount": 댓글수,
                    "profileUrl": 프로필 url,
                    "thumbnail" : 해당 게시글 썸네이리 이미지 url
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
                    "CommentCount" : 댓글 수,
                    "profileUrl": 프로필 url
                    
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
- 게시글 제목 검색
    - **API** : `/api/post/title`
    - **Method : GET**
    - **Request**
       ```jsonc
       http://~/api/post/title?page=0?title="title" ("" 제외하고 입력)
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
                    "CommentCount" : 댓글 수,
                    "profileUrl": 프로필 url
                    
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
- 게시글 내용 검색
    - **API** : `/api/post/content`
    - **Method : GET**
    - **Request**
       ```jsonc
       http://~/api/post/content?page=0?content="content" ("" 제외하고 입력)
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
                    "CommentCount" : 댓글 수,
                    "profileUrl": 프로필 url
                    
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
- 게시글 해시태그 검색
    - **API** : `/api/post/hashtag`
    - **Method : GET**
    - **Request**
       ```jsonc
       http://~/api/post/hashtag?page=0?hashtag="#hashtag" ("" 제외하고 입력, #은 %23으로 인코딩 해서 사용해야함)
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
- 게시글 카테고리 정렬
    - **API** : `/api/post/category`
    - **Method : GET**
    - **Request**
       ```jsonc
       http://~/api/post/category?page=0?cagegory="category" ("" 제외하고 입력)
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
  - 게시글 신고
    - **API** : `/api/member/report/post`
    - **Method : POST**
    - **Body :  raw (json)**
    - **Request**
    
    ```jsonc
    {
        "reportedUserNickname" : 신고하고자 하는 댓글 작성자 닉네임,
        "postId" : 신고하고자 하는 게시글 아이디,
        "reason" : 신고 이유
    }
    ```
    
    - **Response**
      
        - ***200 OK***
          
        ```jsonc
        신고를 완료하였습니다.
        ```
        - ***404 NOT_FOUND***
        
        ```jsonc
        게시글과 작성자가 올바르지 않습니다.
        ```
        - ***403 FORBIDDEN***
        
        ```jsonc
        회원만 가능한 기능입니다.
        ```
        - ***409 CONFLICT***
          
        ```jsonc
        이미 처리된 신고입니다.
        ```

- 게시글 사진 추가 / 조회
    - **API** : `/api/member/post/image`
    - **Method : POST**
    - **Body :  form-data**
    - **Request**
    
    ```jsonc
    	image : "이미지 파일 ex)jpg,png ..."
    ```
    
    - **Response**
        - ***200 OK***
        
        ```jsonc
            {
                url : "업로드한 사진 url",
                capacity : 파일 용량
                
            }
        ```
        
        - ***409 CONFLICT***
        
        ```jsonc
        이미지만 업로드 가능합니다.
        ```
        - ***403 FORBIDDEN***
        
        ```jsonc
        회원만 사용 가능한 기능입니다.
        ```

- 게시글 사진 삭제
    - **API** : `/api/member/post/image/{image_name}`
    - **Method : DELETE**
    
    - **Response**
        - ***200 OK***
        
        ```jsonc
        해당 이미지가 삭제되었습니다.
        ```
        - ***404 NOT FOUND***
        
        ```jsonc
        사진이 존재하지 않습니다.
        ```
        - ***403 FORBIDDEN***
        
        ```jsonc
        회원만 사용 가능한 기능입니다.
        ```

