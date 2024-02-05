* User object
```
{
  id: integer
  username: string
  email: string
  password: string
  role: string
  created_at: datetime()
  updated_at: datetime()
  updated_by: string
  deactivated_at: datetime()
  deactivated_by: string
}
```
User-data object
```
{
  username: string
  email: string
  created_at: datetime()
  updated_at: datetime()
  updated_by: string
  deactivated_at: datetime()
  deactivated_by: string
}
```


## 1. Authentication

### POST /v1/auth/register
----
  Creates a new User and returns the new object.
* **URL Params**  
  None
* **Headers**  
  Content-Type: application/json  
* **Data Params**  
```
  {
    username: string,
    email: string
    password: string
  }
```
* **Success Response:**  
* **Code:** 200  
  **Content:**  `{ <user_object> }` 

### GET /v1/auth/login
----
  Login to CMS
* **URL Params**  
  None
* **Headers**  
  Content-Type: application/json  
* **Data Params**  
```
  {
    username: string,
    password: string
  }
```

* **Success Response:**  
* **Code:** 200  
  **Content:**  
```
{
  ubah dlu: [
           {<user_object>},
           {<user_object>},
           {<user_object>}
         ]
}
```
* **Error Response:**  
  * **Code:** 404  
  **Content:** `{ error : "Username or password error" }`  

### POST /v1/auth/change-password
----
  Creates a new User and returns the new object.
* **URL Params**  
  None
* **Headers**  
  Content-Type: application/json
  Authorization: Bearer `<OAuth Token>`  
* **Data Params**  
```
  {
    old-password: string,
    new-password: string
  }
```
* **Success Response:**  
* **Code:** 200  

* **Error Response:**  
  * **Code:** 404  
  **Content:** `{ error : "Password error" }`  
  OR  
  * **Code:** 401  
  **Content:** `{ error : "You are unauthorized to make this request." }`

## 2. User

### GET /v1/user
----
  Returns all users in the system.
* **URL Params**  
  None
* **Data Params**  
  None
* **Headers**  
  Content-Type: application/json  
  Authorization: Bearer `<OAuth Token>`
* **Success Response:**  
* **Code:** 200  
  **Content:**  
	```
	{
	  users: [
	           {<user-data_object>},
	           {<user-data_object>},
	           {<user-data_object>}
	         ]
	}
	```
* **Error Response:**  
  * **Code:** 401  
  **Content:** `{ error : "You are unauthorized to make this request." }`

### GET /v1/user/{user_id}

  Returns user base on user id in the system.

* **URL Params**  
  *Required:* `user_id=[integer]`
* **Data Params**  
  None
* **Headers**  
  Content-Type: application/json  
  Authorization: Bearer `<OAuth Token>`
* **Success Response:** 
* **Code:** 200  
  **Content:**  `{ <user-data_object> }` 
* **Error Response:**  
  * **Code:** 404  
  **Content:** `{ error : "User doesn't exist" }`  
  OR  
  * **Code:** 401  
  **Content:** `{ error : "You are unauthorized to make this request." }`

### POST /v1/user/{user_id}
----
  Creates a new User and returns the new object.
* **URL Params**  
  *Required:* `id=[integer]`
* **Headers**  
  Content-Type: application/json
  Authorization: Bearer `<OAuth Token>`  
* **Data Params**  
	```
	{
	  username: string
	  email: string
	}
	```
* **Success Response:**  
* **Code:** 200  
  **Content:**  `{ <user-data_object> }` 
* **Error Response:**  
  * **Code:** 409 
  **Content:** `{ error : "username had been used" }`  
  OR  
   * **Code:** 409  
  **Content:** `{ error : "email had been used" }`  
  OR  
  * **Code:** 401  
  **Content:** `{ error : "You are unauthorized to make this request." }`

### DELETE /v1/user/{user_id}
----
  Creates a new User and returns the new object.
* **URL Params**  
  *Required:* `id=[integer]`
* **Headers**  
  Content-Type: application/json
  Authorization: Bearer `<OAuth Token>`  
* **Data Params**  
	```
	{
	  username: string
	  email: string
	}
	```
* **Success Response:**  
* **Code:** 200  
  **Content:**  `{ <user-data_object> }` 
* **Error Response:**  
  * **Code:** 404  
  **Content:** `{ error : "User doesn't exist" }`  
  OR  
  * **Code:** 401  
  **Content:** `{ error : "You are unauthorized to make this request." }`
