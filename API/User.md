## User API List

- 회원가입
    - **API** : `/api/signup/user`
    - **Method : POST**
    - **Body :  raw (json)**
    - **Request**
    
    ```jsonc
    {
    	"id" : user의 ID (e-mail 형식),
    	"password" : user의 Password,
    	"name" : user의 Name,
    	"nickname" : user의 NickName,
    	"phone" : user의 PhoneNumber
    }
    ```
    
    - **Response**
        - ***200 OK***
        
        ```jsonc
        회원으로 가입되었습니다.
        ```
        
        - ***409 CONFLICT***
        
        ```jsonc
        이미 가입된 ID 입니다.
        ```


- ID 중복 체크
    - **API** : `/api/check/userid/{user_id}`
    - **Method : GET**
   - **Request**
    
    ```jsonc
    {
        "user_id" : 사용할 ID
    }
    ```
    
    - **Response**
        - ***200 OK***
        
        ```jsonc
        사용할 수 있는 ID 입니다.
        ```
        
        - ***409 CONFLICT***
        
        ```jsonc
        이미 가입된 ID 입니다.
        ```
        
- 닉네임 중복 체크
    - **API** : `/api/check/nickname/{nickname}`
    - **Method : GET**
   - **Request**
    
    ```jsonc
    {
        "nickname" : 사용할 별명
    }
    ```
    
    - **Response**
        - ***200 OK***
        
        ```jsonc
        사용할 수 있는 별명 입니다.
        ```
        
        - ***409 CONFLICT***
        
        ```jsonc
        존재하는 별명입니다.
        ```
        
- 전화번호 중복 체크
    - **API** : `/api/check/phone/{phone}`
    - **Method : GET**
   - **Request**
    
    ```jsonc
    {
        "phone" : 사용자 전화번호
    }
    ```
    
    - **Response**
        - ***200 OK***
        
        ```jsonc
        사용할 수 있는 전화번호입니다.
        ```
        
        - ***409 CONFLICT***
        
        ```jsonc
        이미 가입된 전화번호 입니다.
        ```
        
- 로그인
    - **API** : `/api/login`
    - **Method : POST**
    - **Body :  raw (json)**

   - **Request**
    
    ```jsonc
    {
        "id" : 사용자 아이디,
        "password" : 사용자 비밀번호
    }
    ```
    
    - **Response**
        - ***200 OK***
        
        ```jsonc
        {
            "nickname" : 유저 닉네임,
            "message" : 로그인 되었습니다.
        }
        ```
        
        - ***404 NOT FOUND***
        
        ```jsonc
        잘못된 아이디 또는 비밀번호 입니다.
        ```
        
- 아이디 찾기
    - **API** : `/api/login/id`
    - **Method : POST**
    - **Body :  raw (json)**

   - **Request**
    
    ```jsonc
    {
        "name" : 사용자 이름,
        "phone" : 사용자 전화번호
    }
    ```
    
    - **Response**
        - ***200 OK***
        
        ```jsonc
        {
            "id" : 사용자 아이디
        }
        ```
        
        - ***404 NOT FOUND***
        
        ```jsonc
        존재하지 않는 전화번호 및 이름입니다.
        ```
        
- 비밀번호 찾기
    - **API** : `/api/login/password`
    - **Method : POST**
    - **Body :  raw (json)**

   - **Request**
    
    ```jsonc
    {
        "id" : 사용자 아이디,
        "name" : 사용자 이름,
        "phone" : 사용자 전화번호
    }
    ```
    
    - **Response**
        - ***200 OK***
        
        ```jsonc
        해당 이메일(아이디)로 인증번호를 발송하였습니다.
        ```
        
        - ***404 NOT FOUND***
        
        ```jsonc
        존재하지 않는 이메일(아이디) 입니다.
        ```
        
- 인증코드 확인
    - **API** : `/api/login/id`
    - **Method : POST**
    - **Body :  raw (json)**

   - **Request**
    
    ```jsonc
    {
        "name" : 사용자 이름
        "phone" : 사용자 전화번호
    }
    ```
    
    - **Response**
        - ***200 OK***
        
        ```jsonc
        인증에 성공하였습니다.
        ```
        
        - ***404 NOT FOUND***
        
        ```jsonc
        인증번호가 일치하지 않습니다.
        ```
        
- 비밀번호 변경
    - **API** : `/api/login/id`
    - **Method : POST**
    - **Body :  raw (json)**

   - **Request**
    
    ```jsonc
    {
        "name" : 사용자 이름
        "phone" : 사용자 전화번호
    }
    ```
    
    - **Response**
        - ***200 OK***
        
        ```jsonc
        비밀번호를 변경하였습니다.
        ```
        
        - ***404 NOT FOUND***
        
        ```jsonc
        존재하지 않는 이메일(아이디)입니다.
        ```
        - ***409 CONFLICT***
        
        ```jsonc
        기존 비밀번호와 동일합니다.
        ```
        
  - 유저정보 확인
    - **API** : `/api/member/userinfo`
    - **Method : GET**

    - **Response**
        - ***200 OK***
        
        ```jsonc
            {
                "id" : 유저 아이디,
                "name" : 유저 이름,
                "nickname" : 유저 닉네임,
                "phone" :  유저 전화번호,
                "createAt" : 유저 가입일
            }
        ```
        
        - ***403 FORBIDDEN***
        
        ```jsonc
        회원만 사용 가능한 기능입니다.
        ```
        
  - 닉네임 변경
    - **API** : `/api/member/new-nickname/{nickname}`
    - **Method : GET**

    - **Response**
        - ***200 OK***
        
        ```jsonc
        닉네임이 변경되었습니다.
        ```
        
        - ***403 FORBIDDEN***
        
        ```jsonc
        회원만 사용 가능한 기능입니다.
        ```
        - ***409 CONFLICT***
        
        ```jsonc
        존재하는 닉네임입니다.
        ```
        
  - 전화번호 변경
    - **API** : `/api/member/new-phone-number/{phone-number}`
    - **Method : GET**

    - **Response**
        - ***200 OK***
        
        ```jsonc
        전화번호가 변경되었습니다.
        ```
        
        - ***403 FORBIDDEN***
        
        ```jsonc
        회원만 사용 가능한 기능입니다.
        ```
        - ***409 CONFLICT***
        
        ```jsonc
        존재하는 전화번호입니다.
        ```
        
  - 회원 탈퇴
    - **API** : `/api/member
    - **Method : DELETE**

    - **Response**
        - ***200 OK***
        
        ```jsonc
        회원탈퇴가 완료되었습니다.
        ```
        
        - ***403 FORBIDDEN***
        
        ```jsonc
        회원만 사용 가능한 기능입니다.
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

- 자신이 작성한 댓글의 게시글 리스트 조회
    - **API** : `/api/member/comment/list`
    - **Method : GET**
    - **Request**
       ```jsonc
       http://~/api/member/comment/list?page=1
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

- 좋아요 한 게시글 리스트 조회
    - **API** : `/api/member/liked/post/list`
    - **Method : GET**
    - **Request**
       ```jsonc
       http://~/api/member/liked/post/list?page=1
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

- 좋아요한 댓글의 게시글 리스트 조회
    - **API** : `/api/member/liked/comment/list`
    - **Method : GET**
    - **Request**
       ```jsonc
       http://~/api/member/liked/comment/list?page=1
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

- 프로필 사진 추가/변경
    - **API** : `/api/member/profile/image`
    - **Method : POST**
    - **Body :  form-data**
    - **Request**
    
    ```jsonc
    	image : "이미지 파일 ex)jpg,png ..."
    ```
    
    - **Response**
        - ***200 OK***
        
        ```jsonc
        프로필사진을 등록하였습니다.
        or
        프로필사진이 변경되었습니다.
        ```
        
        - ***409 CONFLICT***
        
        ```jsonc
        이미지만 업로드 가능합니다.
        ```

- 프로필 사진 삭제
    - **API** : `/api/member/profile/image`
    - **Method : DELETE**
    
    - **Response**
        - ***200 OK***
        
        ```jsonc
        프로필사진이 삭제되었습니다.
        ```
        
        - ***409 NOT FOUND***
        
        ```jsonc
        프로필 사진이 등록되어 있지 않습니다.
        ```

- 프로필 사진 조회
    - **API** : `/api/profile/image`
    - **Method : GET**
    
    - **Response**
        - ***200 OK***
        
        ```jsonc
        {
            url : 이미지 url,
            capacity : 이미지 용량
        }
        ```

- access 토큰 연장
    - **API** : `/api/reissue`
    - **Method : POST**
    - **Body :  raw (json)**
    - **Request**
    
    ```jsonc
    쿠키의 refresh토큰
    ```
    
    - **Response**
        - ***200 OK***
        
        ```jsonc
        토큰을 연장하였습니다.
        ```
        

        
