## Map API List

- 지도 범위 게시글 조회
    - **API** : `/api/map/marker`
    - **Method : POST**
    - **Body :  raw (json)**
    - **Request**
    
    ```jsonc
    {
        "south" : getbounds로 얻은 지도 범위 남쪽 좌표 (소수점),
        "west" : getbounds로 얻은 지도 범위 서쪽 좌표 (소수점),
        "north" : getbounds로 얻은 지도 범위 북쪽 좌표 (소수점),
        "east" : getbounds로 얻은 지도 범위 동쪽 좌표 (소수점)
    }
    ```
    
    - **Response**
        - ***200 OK***
        
        ```jsonc
        [
          {
            "postId" : 해당 게시글 id,
            "xposition": 게시글의 x좌표,
            "yposition": 게시글의 y좌표,
            "position" : 게시글 주소
          },
          {
            ...        
          }
        ]
        ```
        
- 동일 좌표 게시글 리스트 조회
    - **API** : `/api/map/post/{xPosition}/{yPosition}`
    - **Method : GET**    
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
        
- 장소 즐겨찾기
    - **API** : `/api/member/map/bookmark`
    - **Method : POST**
    - **Body :  raw (json)**
    - **Request**
    
    ```jsonc
    {
        "xposition" : 즐겨찾기 할 장소의 x좌표(소수점),
        "yposition" : 즐겨찾기 할 장소의 y좌표(소수점),
        "status" : 즐겨찾기 상태 (좋아요 : LIKE,  갈 곳 : WISH, 간 곳 : VISITED) ex) "status" : "LIKE"
    }
    ```
    
    - **Response**
        - ***200 OK***

- 즐겨찾기 리스트 조회
    - **API** : `/api/member/map/bookmark/list`
    - **Method : POST**
    - **Body :  raw (json)**
    - **Request**
    
    ```jsonc
    {
        "south" : getbounds로 얻은 지도 범위 남쪽 좌표 (소수점),
        "west" : getbounds로 얻은 지도 범위 서쪽 좌표 (소수점),
        "north" : getbounds로 얻은 지도 범위 북쪽 좌표 (소수점),
        "east" : getbounds로 얻은 지도 범위 동쪽 좌표 (소수점)
    }
    ```
    
    - **Response**
        - ***200 OK***
        
        ```jsonc
        [
          {
            "status" : 즐겨찾기 종류 (좋아요 -> LIKE, 갈 곳 -> WISH, 간 곳 -> VISITED),
            "xposition" : 해당 장소 x좌표,
            "yposition" : 해당 장소 y좌표
          },
          {
            ...        
          }
        ]
        ```
        
