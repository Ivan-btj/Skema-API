
## 1. Authentication

* User object
```
{
  id: integer
  name: string
  username: string
  email: string
  password: string
  role: string
  created_at: datetime()
  created_by: datetime()
  updated_at: datetime()
  updated_by: string
  deactivated_at: datetime()
  deactivated_by: string
}
```
User-data object
```
{
  id: integer
  name: string
  username: string
  created_at: datetime()
  created_by: datetime()
  updated_at: datetime()
  updated_by: string
  deactivated_at: datetime()
  deactivated_by: string
}
```

### POST /v1/auth/register
----
  Creates a new User and returns the new object. Only admin that can register user
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
 Login User and returns the refresh key. Only admin that can register user
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
	  id: integer
	  name: string
	  username: string
	  created_at: datetime()
	  created_by: datetime()
	  updated_at: datetime()
	  updated_by: string
	  deactivated_at: datetime()
	  deactivated_by: string
	  access_token": string
	  refresh_token": string
}
```
* **Error Response:**  
  * **Code:** 404  
  **Content:** `{ message : "Username or password error" }`  

### POST /v1/auth/change-password
----
  Creates a new User and returns the new object.
* **URL Params**  
  None
* **Headers**  
  Content-Type: application/json
  Authorization:  `<Bearer Token (JWT)>`
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
  **Content:** `{ message : "Password error" }`  
  OR  
  * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

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
  Authorization:  `<Bearer Token (JWT)>`
* **Success Response:**  
* **Code:** 200  
  **Content:**  
	```
	{
	  users: 
	  [
          {<user-data_object>},
          {<user-data_object>},
          {<user-data_object>}
	  ]
	}
	```
* **Error Response:**  
  * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

### GET /v1/user/{user_id}

  Returns user base on user id in the system.

* **URL Params**  
  *Required:* `user_id=[integer]`
* **Data Params**  
  None
* **Headers**  
  Content-Type: application/json  
  Authorization:  `<Bearer Token (JWT)>`
* **Success Response:** 
* **Code:** 200  
  **Content:**  `{ <user-data_object> }` 
* **Error Response:**  
  * **Code:** 404  
  **Content:** `{ message : "User doesn't exist" }`  
  OR  
  * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

### POST /v1/user/{user_id}
----
  Creates a new User and returns the new object.
* **URL Params**  
  *Required:* `id=[integer]`
* **Headers**  
  Content-Type: application/json
  Authorization:  `<Bearer Token (JWT)>`
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
  **Content:** `{ message : "User doesn't exist" }`  
  * **Code:** 409 
  **Content:** `{ message : "username had been used" }`  
  OR  
   * **Code:** 409  
  **Content:** `{ message : "email had been used" }`  
  OR  
  * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

### DELETE /v1/user/{user_id}
----
  Creates a new User and returns the new object.
* **URL Params**  
  *Required:* `id=[integer]`
* **Headers**  
  Content-Type: application/json
  Authorization:  `<Bearer Token (JWT)>`  
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
  **Content:** `{ message : "User doesn't exist" }`  
  OR  
  * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

## 3. Subscription

subscription object:
{
	image (.jpg or.png)
}


### GET /v1/subscription/

  Returns image base on image name in the system.

* **URL Params**  
  *Required:* `image_id=[integer]`
* **Data Params**  
  None
* **Headers**  
  Content-Type: file/image 
* **Success Response:** 
* **Code:** 200  
  **Content:**  

	```
	{
		belum ada
	}
	```
* **Error Response:**  
  * **Code:** 404  
  **Content:** `{ message : "Subscription not found" }`  
   * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

### GET /v1/subscription/{subscription_id}

  Returns image base on image name in the system.

* **URL Params**  
  *Required:* `subscription_id=[integer]`
* **Data Params**  
  None
* **Headers**  
  Content-Type: file/image 
* **Success Response:** 
* **Code:** 200  
  **Content:**
	```
	{
		belum ada
	}
	```

* **Error Response:**  
  * **Code:** 404  
  **Content:** `{ message : "Subscription not found" }` 
   * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

### POST /v1/subscription/{subscription_id}
----
  Creates a new User and returns the new object.
* **URL Params**  
  *Required:* `subscription_id=[integer]`
* **Headers**  
  Content-Type: file/image 
  Authorization:  `<Bearer Token (JWT)>`
* **Data Params**  
`{ <image_object> }`
* **Success Response:**  
* **Code:** 200  
  **Content:**  
  
	```
	{
		belum ada
	}
	```
* **Error Response:**  
  * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`


## 4. Images

image object: 

image: (.jpg or.png)


### GET /v1/images/{image_folder}/

  Returns image base on image name in the system.

* **URL Params**  
	*Required:* `image_folder=[string]`
* **Data Params**  
  None
* **Headers**  
  Content-Type: file/image 
* **Success Response:** 
* **Code:** 200  
  **Content:**  

	```
	{
	  images 
	  [
		  { <image_object> },
		  { <image_object> },
		  { <image_object> }
	  ]
	}
	```
* **Error Response:**  
  * **Code:** 404  
  **Content:** `{ message : "Image not found" }`  

### GET /v1/images/{image_folder}/{image_name}

  Returns image base on image name in the system.

* **URL Params**
   *Required:* `image_folder=[string]`  
   *Required:* `image_name=[string]`
* **Data Params**  
  None
* **Headers**  
  Content-Type: file/image 
* **Success Response:** 
* **Code:** 200  
  **Content:**  `{ <image_object> }` 
* **Error Response:**  
  * **Code:** 404  
  **Content:** `{ message : "Image not found" }`  

### POST /v1/images/{image_folder}/{image_name}
----
  Creates a new User and returns the new object.
* **URL Params**  
   *Required:* `image_folder=[string]`  
   *Required:* `image_name=[string]`
* **Headers**  
  Content-Type: file/image 
  Authorization:  `<Bearer Token (JWT)>`
* **Data Params**  
`{ <image_object> }`
* **Success Response:**  
* **Code:** 200  
  **Content:**  `{ <image_object> }`  
* **Error Response:**  
  * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

### PUT /v1/images/{image_folder}/{image_name}
----
  Creates a new User and returns the new object.
* **URL Params**  
   *Required:* `image_folder=[string]`  
   *Required:* `image_name=[string]`
* **Headers**  
  Content-Type: file/image
  Authorization:  `<Bearer Token (JWT)>`
* **Data Params**  
`{ <image_object> }`
* **Success Response:**  
* **Code:** 200  
  **Content:**  `{ <image_object> }`  
* **Error Response:**  
  * **Code:** 404  
  **Content:** `{ message : "Image not found" }`  
  OR  
  * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

### DELETE /v1/images/{image_folder}/{image_name}
----
  Creates a new User and returns the new object.
* **URL Params**  
   *Required:* `image_folder=[string]`  
   *Required:* `image_name=[string]`
* **Headers**  
  Content-Type: file/image
  Authorization:  `<Bearer Token (JWT)>`
* **Data Params**  
	None
* **Success Response:**  
* **Code:** 200  
  **Content:**  `{ <image_object> }`  
* **Error Response:**  
  * **Code:** 404  
  **Content:** `{ message : "Image not found" }`  
  OR  
  * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`
