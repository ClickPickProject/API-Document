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
        

