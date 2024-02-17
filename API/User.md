## User API List

- 회원가입
    - **API** : `/api/signup/user`
    - **Method : POST**
    - **Body :  raw (json)**
    - **Request**
    
    ```jsonc
    {
    	"user_id" : user의 ID에 해당
    	"password" : user의 Password
    	"name" : user의 Name
    	"nickname" : user의 NickName
    	"phone" : user의 PhoneNumber
      "email" : user의 E-mail
      
    }
    ```
    
    - **Response**
        - 200 OK
        
        ```jsonc
        회원가입 완료
        ```
        
        - 401 *UNAUTHORIZED*
        
        ```jsonc
        회원가입 시도중 오류가 발생했습니다. 아이디 중복을 확인해주세요.
        ```
