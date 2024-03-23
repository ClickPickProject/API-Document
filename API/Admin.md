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
- 유저 리스트
    - **API** : `/api/admin/manager/userlist`
    - **Method : GET**
    - **Response**
        - ***200 OK***
        
        ```jsonc
        {
            "content": [  //유저 리스트
                {
                    "id": "tm4839@naver.com",
                    "name": "태민",
                    "nickname": "태민",
                    "phone": "01012345678"
                },
                {
                    "id": "ban@naver.com",
                    "name": "ban",
                    "nickname": "ban",
                    "phone": "01012345679"
                }
            ],
            "pageable": {
                "pageNumber": 0,
                "pageSize": 10,
                "sort": {
                    "empty": false,
                    "unsorted": false,
                    "sorted": true
                },
                "offset": 0,
                "paged": true,
                "unpaged": false
            },
            "last": true,
            "totalElements": 2,
            "totalPages": 1,
            "first": true,
            "size": 10,
            "number": 0,
            "sort": {
                "empty": false,
                "unsorted": false,
                "sorted": true
            },
            "numberOfElements": 2,
            "empty": false
        }
        ```

        
- 게시물로 신고된 유저 정지 시키기
    - **API** : `/api/admin/manager/postban`
    - **Method : POST**
    - **Request**
    
        ```jsonc
        {
            "reportedUserId" : "ban@naver.com",
            "reason" : "테스트",
            "endDate" : "2024-03-31T23:59:59"    //시간 관련 프론트에서 어떻게 넘길지 고려
        }
        ```
    
    - **Response**
        - ***200 OK***
        
        ```jsonc
        사용자를 정지 시켰습니다. 
        ```

- 정지된 유저 리스트
    - **API** : `/api/admin/manager/banuserlist`
    - **Method : GET**
    - **Response**
        - ***200 OK***
        
        ```jsonc
        {
            "content": [
                {
                    "id": "ban@naver.com",  //정지된 유저 정보
                    "password": null,
                    "name": "ban",
                    "nickname": "ban",
                    "phone": "01012345679"
                }
            ],
            "pageable": {
                "pageNumber": 0,    //현재 페이지
                "pageSize": 10,     //한 페이지당 가능한 게시글 수
                "sort": {
                    "empty": false,    //정렬 정보가 비어있는지 여부
                    "unsorted": false, //페이징 결과 정렬 여부
                    "sorted": true     //페이징 결과 정렬 여부
                },
                "offset": 0,           //현재 페이지의 게시글 시작 위치
                "paged": true,         //페이징 여부
                "unpaged": false       //페이징 여부
            },
            "last": true,              //현재 페이지가 마지막 페이지 인지
            "totalElements": 1,        //총 페이지의 개수
            "totalPages": 1,           //게시글 총 개수
            "first": true,             //첫 게시글인지 여부
            "size": 10,                //페이지 당 표시 가능한 게시글 수
            "number": 0,               //현재 페이지 번호
            "sort": {
                "empty": false,        //정렬 정보가 비어 있는지 여부
                "unsorted": false,     //페이징 결과 정렬 여부
                "sorted": true         //페이징 결과 정렬 여부
            },
            "numberOfElements": 1,     //현재 페이지에 포함된 게시글의 수
            "empty": false             //현재 페이지의 결과가 비어 있는지 여부
        }
        ```
