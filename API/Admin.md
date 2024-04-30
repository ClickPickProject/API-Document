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
    - **Method : POST**
    - **Body :  raw (json)**
    
    - **Response**
        - ***200 OK***
        
        ```jsonc
        수정이 완료되었습니다.
        ```

- 공지사항 삭제
    - **API** : `/api/admin/notice`
    - **Method : DELETE**
    - **Response**
        - ***200 OK***
        
        ```jsonc
        공지사항 삭제가 완료되었습니다. 
        ```
        
- 유저 리스트
    - **API** : `/api/admin/userlist`
    - **Method : GET**
    - **Request**
       ```jsonc
       http://~/api/admin/userlist?page=0?status="normal" or "ban" ("" 제외하고 입력, 소문자)
       ```
    - **Response**
        - ***200 OK***
        ```jsonc
        {
            "content": [
                {
                    "id" : 유저의 id,
                    "nickname" : 유저의 닉네임,
                    "name" : 유저의 이름,
                    "phone" : 유저의 전화번호,
                    "createAt" : 유저의 가입일,
                    "userStatus" : 유저의 상태
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

- 정지된 유저 리스트
    - **API** : `/api/admin/banuserlist`
    - **Method : GET**
    - **Response**
        - ***200 OK***
              
            ```jsonc
            {
                "content": [
                    {
                        "id" : 정지된 유저 id,
                        "nickname" : 정지된 유저 닉네임,
                        "name" : 정지된 유저 이름,
                        "phone" : 정지된 유저 전화번호,
                        "startDate" : 정지 시작일,
                        "endDate" : 정지 종료일 
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

- 정지 유저 기간 변경
    - **API** : `/api/admin/ban/period`
    - **Method : POST**
    - **Body :  raw (json)**
    - **Request**
    
        ```jsonc
        {
            "userId" : 기간을 변경하고자 하는 유저 id,
            "days" : 정지 기간 (Long)
        }
        ```
    
    - **Response**
        - ***200 OK***
        
        ```jsonc
        정지 기간을 변경하였습니다.
        ```

        - ***404 NON FOUND***
        
        ```jsonc
        정지 유저에 존재하지 않습니다.
        ```
- 정지 유저 삭제
    - **API** : `/api/admin/ban/{userId}`
    - **Method : DELETE**
    - **Response**
        - ***200 OK***
        
        ```jsonc
        정지 유저에서 삭제하였습니다.
        ```

        - ***404 NON FOUND***
        
        ```jsonc
        정지 유저에 존재하지 않습니다.
        ```
        
- 공지사항 리스트 조회
    - **API** : `/api/notice/list`
    - **Method : GET**
    - **Request**
       ```jsonc
       http://~/api/notice/list?page=0
       ```
    - **Response**
      
        - ***200 OK***
          
            ```jsonc
            {
                "content": [
                    {
                        "noticeId": 공지사항 Id,
                        "nickname": "ADMIN" (고정),
                        "title": 공지사항의 제목,
                        "createAt": 공지사항 작성일자
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

- 공지사항 상세 조회
    - **API** : `/api/notice/{notice_id}`
    - **Method : GET**    
    - **Response**
      
        - ***200 OK***
              
        ```jsonc
        {
            "noticeId" : 공지사항 아이디,
            "nickname" : "ADMIN" (고정),
            "title" : 해당 공지사항의 제목,
            "content" : 해당 공지사항의 내용,
            "date" : 해당 공지사항의 작성일자
        }
        ```
        
        - ***404 NOT FOUND***
            
        ```jsonc
        게시글을 찾을 수 없습니다.
        ```

- 신고된 게시글 처리
    - **API** : `/api/admin/postban`
    - **Method : POST**
    - **Body :  raw (json)**
    - **Request**
    
        ```jsonc
        {
            "reportId" : 신고된 게시글의 ID (신고된 게시글 테이블의 자체 아이디),
            "reportedUserId" : 신고된 유저의 id,
            "reason" : 신고 사유,
            "banDays" : 정지 기간 (Long)
        }
        ```
    
    - **Response**
        - ***200 OK***
        
        ```jsonc
        사용자를 정지 시켰습니다. 
        or
        정지기간을 연장하였습니다.
        ```

        - ***404 NOT FOUND***
        
        ```jsonc
        사용자를 찾을 수 없습니다.
        ```

- 신고된 댓글 처리
    - **API** : `/api/admin/commentban`
    - **Method : POST**
    - **Body :  raw (json)**
    - **Request**
    
        ```jsonc
        {
            "reportId" : 신고된 댓글의 ID (신고된 댓글 테이블의 자체 아이디),
            "reportedUserId" : 신고된 유저의 id,
            "reason" : 신고 사유,
            "banDays" : 정지 기간 (Long)
        }
        ```
    
    - **Response**
        - ***200 OK***
        
        ```jsonc
        사용자를 정지 시켰습니다. 
        or
        정지기간을 연장하였습니다.
        ```

        - ***404 NOT FOUND***
        
        ```jsonc
        사용자를 찾을 수 없습니다.
        ```


- 신고된 게시글 리스트 조회
    - **API** : `/api/admin/reportpostlist`
    - **Method : GET**
    - **Request**
       ```jsonc
       http://~/api/notice/list?page=0
       ```
    - **Response**
      
        - ***200 OK***
          
        ```jsonc
        {
            "content": [
                {
                    "reportPostId": 신고된 게시글의 ID (신고된 게시글 테이블의 자체 아이디),
                    "reportUserId": 신고한 유저의 id,
                    "reportedUserId": 신고당한 유저의 id,
                    "postId": 신고된 게시글의 id (게시글 자체 id),
                    "reason": 신고 사유,
                    "reportStatus": 상태
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

  - 신고된 댓글 리스트 조회
    - **API** : `/api/admin/reportcommentlist`
    - **Method : GET**
    - **Request**
       ```jsonc
       http://~/api/notice/list?page=0
       ```
    - **Response**
      
        - ***200 OK***
          
        ```jsonc
        {
            "content": [
                {
                    "reportCommentId": 신고된 댓글의 ID (신고된 댓글 테이블의 자체 아이디),
                    "reportUserId": 신고한 유저의 id,
                    "reportedUserId": 신고당한 유저의 id,
                    "commentId": 신고된 댓글의 id (댓글 자체의 id),
                    "reason": 신고 사유,
                    "reportStatus": 상태
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


    - 월별 가입자 카운팅
    - **API** : `/api/admin/user/month/{year}`
    - **Method : GET**
    - **Response**
        - ***200 OK***
        ```jsonc
            {
            "userCount": 해당 월의 가입자 수,
            "monthYear": 입력받은 년도와 해당 월
            }
        ```
