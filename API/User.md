## User API List

- 회원가입
    - **API** : `/api/signup/user`
    - **Method : POST**
    - **Body :  raw (json)**
    - **Request**
    
    ```jsonc
    {
    	"user_id" : user의 ID (e-mail 형식)
    	"password" : user의 Password
    	"name" : user의 Name
    	"nickname" : user의 NickName
    	"phone" : user의 PhoneNumber
    }
    ```
    
    - **Response**
        - 200 OK
        
        ```jsonc
        회원으로 가입되었습니다.
        ```
        
        - 409 *CONFLICT*
        
        ```jsonc
        이미 가입된 ID 입니다.
        ```


- ID 중복 체크
    - **API** : `/api/check/userid/{user_id}`
    - **Method : GET**
    - **Body :  raw (json)**

   - **Request**
    
    ```jsonc
    {
    	"user_id" : 사용할 ID
    }
    ```
    
    - **Response**
        - 200 OK
        
        ```jsonc
        사용할 수 있는 ID 입니다.
        ```
        
        - 409 *CONFLICT*
        
        ```jsonc
        이미 가입된 ID 입니다.
        ```
        
- 닉네임 중복 체크
    - **API** : `/api/check/nickname/{nickname}`
    - **Method : GET**
    - **Body :  raw (json)**

   - **Request**
    
    ```jsonc
    {
    	"nickname" : 사용할 별명
    }
    ```
    
    - **Response**
        - 200 OK
        
        ```jsonc
        사용할 수 있는 별명 입니다.
        ```
        
        - 409 *CONFLICT*
        
        ```jsonc
        존재하는 별명입니다.
        ```
        
- 전화번호 중복 체크
    - **API** : `/api/check/phone/{phone}`
    - **Method : GET**
    - **Body :  raw (json)**

   - **Request**
    
    ```jsonc
    {
    	"phone" : 사용자 전화번호
    }
    ```
    
    - **Response**
        - 200 OK
        
        ```jsonc
        사용할 수 있는 전화번호입니다.
        ```
        
        - 409 *CONFLICT*
        
        ```jsonc
        이미 가입된 전화번호 입니다.
        ```
