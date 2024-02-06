
## 1. Authentication

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
  deactivated_at: datetime()
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
  **Content:**  `{ message : "Success create users" }`
  `{ <user_object> }` 

### POST /v1/auth/roles
----
  Creates a new roles and returns the new object.
* **URL Params**  
  None
* **Headers**  
  Content-Type: application/json  
* **Data Params**  
```
  {
	  ....
    access_to_POST/v1/users/
    access_to_GET/v1/users/{user_id}
    access_to_PUT/v1/users/{user_id}
    ....
  }
```
* **Success Response:**  
* **Code:** 200  
  **Content:**  `{ message : "Success create users" }`
  `{ <user_object> }` 

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
  `{ message : "Success login user" }`
```
{
	  id: integer
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

### POST /v1/auth/change-password/{user_id}
----
  Change users password base on id.
  
* **URL Params**  
  *Required:* `user_id=[integer]`
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
**Content:**  `{ message : "Failed change password" }`
* **Error Response:**  
  * **Code:** 404  
  **Content:** `{ message : "Password error" }`  
  OR  
  * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

## 2. User

### GET /v1/users
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
  `{ message : "Success update user" }` 
	```
	{
	  data: 
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

### GET /v1/users?page_number={integer}&item_per_page={integer}&filter_by_id={boolean}
----
  Returns all users in the system with pagination.
* **URL Params**  
  None
* **Data Params**  
  Query Parameter: 
	  page_number: `<page_number>` 
	  item_per_page: `<page_size>`
	  filter_by_id: `<filter_by_id>`
* **Headers**  
  Content-Type: application/json  
  Authorization:  `<Bearer Token (JWT)>`
* **Success Response:**  
* **Code:** 200  
  **Content:**  
  `{ message : "Success update user" }` 
	```
	{
	  page_number: integer 
	  item_per_page: integer
	  filter_by_id: boolean
	  data: 
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

### GET /v1/users/{user_id}

  Returns user base on id.

* **URL Params**  
  *Required:* `user_id=[integer]`
* **Data Params**  
  None
* **Headers**  
  Content-Type: application/json  
  Authorization:  `<Bearer Token (JWT)>`
* **Success Response:** 
* **Code:** 200  
  **Content:**  `{ message : "Success get user" }` 
  `{ <user-data_object> }` 
* **Error Response:**  
  * **Code:** 404  
  **Content:** `{ message : "User doesn't exist" }`  
  OR  
  * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

### PUT /v1/users/{user_id}
----
  Update one user base on id.
* **URL Params**  
  *Required:* `user_id=[integer]`
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
  **Content:**  `{ message : "Success update user" }` 
  `{ <user-data_object> }`  
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

### DELETE /v1/users/{user_id}
----
  Delete user base on id.
* **URL Params**  
  *Required:* `user_id=[integer]`
* **Headers**  
  Content-Type: application/json
  Authorization:  `<Bearer Token (JWT)>`  
* **Data Params**  
	None
* **Success Response:**  
* **Code:** 200  
  **Content:**  `{ message : "Success delete user" }` 
  `{ <user-data_object> }` 
* **Error Response:**  
  * **Code:** 404  
  **Content:** `{ message : "User doesn't exist" }`  
  OR  
  * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

## 3. Subscription/Subscriber

subscriber object
```
	{
		subscriber_id: integer
		email: string
		category: string
		subscribe_date
	}
```

### GET /v1/subscribers/

  Returns all subscriber.

* **URL Params**  
	None
* **Data Params**  
  None
* **Headers**  
  Content-Type: application/json 
* **Success Response:** 
* **Code:** 200  
  **Content:**  `{ message : "Success get subscriber" }` 
	```
	{
	  data: 
	  [
          {<subscriber_object>},
          {<subscriber_object>},
          {<subscriber_object>}
	  ]
	}
	```
* **Error Response:**  
  * **Code:** 404  
  **Content:** `{ message : "Subscriber not found" }`  
   * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

### GET /v1/subscribers/?page_number={integer}&item_per_page={integer}&filter_by_id={boolean}

  Returns all subscriber with pagination.

* **URL Params**  
	None
* **Data Params**  
  Query Parameter: 
	  page_number: `<page_number>` 
	  item_per_page: `<page_size>`
	  filter_by_id: `<filter_by_id>`
* **Headers**  
  Content-Type: application/json 
* **Success Response:** 
* **Code:** 200  
  **Content:**  `{ message : "Success get subscriber" }` 
	```
	{
	  page_number: integer 
	  item_per_page: integer
	  filter_by_id: boolean
	  data: 
	  [
          {<subscriber_object>},
          {<subscriber_object>},
          {<subscriber_object>}
	  ]
	}
	```
* **Error Response:**  
  * **Code:** 404  
  **Content:** `{ message : "Subscriber not found" }`  
   * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

### GET /v1/subscribers/{subscriber_id}

  Return subscriber base on subcriber id.

* **URL Params**  
  *Required:* `subscriber_id=[integer]`
* **Data Params**  
  None
* **Headers**  
  Content-Type: application/json
* **Success Response:** 
* **Code:** 200  
  **Content:**   `{ message : "Success get subscriber" }` 
  `{ <subscriber_object> }` 
* **Error Response:**  
  * **Code:** 404  
  **Content:** `{ message : "Subscriber not found" }` 
   * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

### POST /v1/subscribers/
----
  Create subscriber.
* **URL Params**  
	None
* **Headers**  
  Content-Type: file/image 
  Authorization:  `<Bearer Token (JWT)>`
* **Data Params**  
`{ <image_object> }`
* **Success Response:**  
* **Code:** 200  
  **Content:** `{ message : "Success add subscriber" }`  
   `{ <subscriber_object> }` 
* **Error Response:**  
  * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`


### DELETE /v1/subcribers/{subscriber_id}
----
  Delete subscriber base on id.
* **URL Params**  
  *Required:* `subscriber_id=[integer]`
* **Headers**  
  Content-Type: file/image
  Authorization:  `<Bearer Token (JWT)>`
* **Data Params**  
	None
* **Success Response:**  
* **Code:** 200  
  **Content:**  `{ message : "Success delete subscriber" }`  
  `{ <subscriber_object> }`  
* **Error Response:**  
  * **Code:** 404  
  **Content:** `{ message : "Subscriber not found" }`  
  OR  
  * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

## 4. Images

image object: 

image: (.jpg or.png)


### GET /v1/images/{image_folder}/

  Returns all image in the folder.

* **URL Params**  
	*Required:* `image_folder=[string]`
* **Data Params**  
  None
* **Headers**  
  Content-Type: file/image 
* **Success Response:** 
* **Code:** 200  
  **Content:**  
`{ message : "Success add image" }`  
	```
	{
	  data: 
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

### GET /v1/images/{image_folder}?page_number={integer}&item_per_page={integer}

  Returns all image in the folder.

* **URL Params**  
	*Required:* `image_folder=[string]`
* **Data Params**  
  Query Parameter: 
	  page_number: `<page_number>` 
	  item_per_page: `<page_size>`
* **Headers**  
  Content-Type: file/image 
* **Success Response:** 
* **Code:** 200  
  **Content:**  
`{ message : "Success add image" }`  
	```
	{
	  page_number: integer 
	  item_per_page: integer
	  filter_by_id: boolean
	  data: 
	  [
          {<image_object>},
          {<image_object>},
          {<image_object>}
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
  **Content:**  `{ message : "Success get image" }`  
  `{ <image_object> }`` 
* **Error Response:**  
  * **Code:** 404  
  **Content:** `{ message : "Image not found" }`  

### POST /v1/images/{image_folder}/{image_name}
----
  Creates a new image.
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
  **Content:**  `{ message : "Success add image" }`  
  `{ <image_object> }`    
* **Error Response:**  
  * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

### PUT /v1/images/{image_folder}/{image_name}
----
  Update image.
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
  **Content:**  `{ message : "Success update image" }`  
  `{ <image_object> }`    
* **Error Response:**  
  * **Code:** 404  
  **Content:** `{ message : "Image not found" }`  
  OR  
  * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

### DELETE /v1/images/{image_folder}/{image_name}
----
  Delete Image
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
  **Content:**  `{ message : "Success delete image" }`  
* **Error Response:**  
  * **Code:** 404  
  **Content:** `{ message : "Image not found" }`  
  OR  
  * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

## 5. Contact us

contact_us object
```
	{
		contact_us_id: integer
		email: string
		name: string
		address: string
		social_media: string
	}
```

### GET /v1/contact_us/

  Returns contact request.

* **URL Params**  
	None
* **Data Params**  
  None
* **Headers**  
  Content-Type: application/json
* **Success Response:** 
* **Code:** 200  
  **Content:**  `{ message : "Success get contact request content" }`  
	```
	{
	  data: 
	  [
          {<contact_us_object>},
          {<contact_us_object>},
          {<contact_us_object>}
	  ]
	}
	```     
* **Error Response:**  
   * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

### GET /v1/contact_us?page_number={integer}&item_per_page={integer}

  Returns contact request with pagination.

* **URL Params**  
	None
* **Data Params**  
  None
* **Headers**  
  Content-Type: application/json
* **Success Response:** 
* **Code:** 200  
  **Content:**  `{ message : "Success get contact request content" }`  
	```
	{
	  page_number: integer 
	  item_per_page: integer
	  data: 
	  [
          {<contact_us_object>},
          {<contact_us_object>},
          {<contact_us_object>}
	  ]
	}
	```  
* **Error Response:**  
   * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`


### GET /v1/contact_us/{contact_us_id}

  Returns contact request base on id

* **URL Params**  
  *Required:* `contact_us_id=[integer]`
* **Data Params**  
  None
* **Headers**  
  Content-Type: application/json
* **Success Response:** 
* **Code:** 200  
  **Content:**  `{ message : "Success get contact request content" }`  
  `{ <contact_us_object> }`    
* **Error Response:**  
  * **Code:** 404  
  **Content:** `{ message : "Contact request not found" }` 
  OR
   * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

### POST /v1/contact_us/
----
  Create contact request
* **URL Params**  
	None
* **Headers**  
  Content-Type: application/json
  Authorization:  `<Bearer Token (JWT)>`  
* **Data Params**  
`{ <image_object> }`
* **Success Response:**  
* **Code:** 200  
  **Content:** `{ message : "Success create contact request content" }`  
  `{ <contact_us_object> }`  
* **Error Response:**  
  * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

### Delete /v1/contact_us/{contact_us_id}

  Delete contact request base on id

* **URL Params**  
  *Required:* `contact_us_id=[integer]`
* **Data Params**  
  None
* **Headers**  
  Content-Type: application/json
* **Success Response:** 
* **Code:** 200  
  **Content:**  `{ message : "Success delete contact request content" }`  
  `{ <contact_us_object> }`    
* **Error Response:**  
  * **Code:** 404  
  **Content:** `{ message : "Contact request not found" }` 
  OR
   * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

## 6. Blogs

blog object
```
	{
		blog_id: integer
		title: string
		body_text: string
		visibility: boolean
		created_at: datetime()
		updated_at: datetime()
		deleted_at: datetime()
		created_by: string
		updated_by: string
		deleted_by: string
		image_path: string
	}
```

### GET /v1/blogs/

  Returns all blogs

* **URL Params**  
	None
* **Data Params**  
  None
* **Headers**  
  Content-Type: file/image 
* **Success Response:** 
* **Code:** 200  
  **Content:**  `{ message : "Success get blog" }`
    `{ <blogs_object> }`    
* **Error Response:**  
   * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

### GET /v1/blogs?page_number={integer}&item_per_page={integer}&filter_by_id={boolean}

  Returns image base on image name in the system.

* **URL Params**  
	None
* **Data Params**  
  Query Parameter: 
	  page_number: `<page_number>` 
	  item_per_page: `<page_size>`
	  filter_by_id: `<filter_by_id>`
* **Headers**  
  Content-Type: file/image 
* **Success Response:** 
* **Code:** 200  
  **Content:**  `{ message : "Success get blog" }`
	```
	{
	  page_number: integer 
	  item_per_page: integer
	  filter_by_id: boolean
	  users: 
	  [
          {<blog_object>},
          {<blog_object>},
          {<blog_object>}
	  ]
	}
	```
* **Error Response:**  
   * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`


### GET /v1/blogs/{blogs_id}

  Returns blog base on blog name.

* **URL Params**  
  *Required:* `blog_id=[integer]`
* **Data Params**  
  None
* **Headers**  
  Content-Type: file/image 
* **Success Response:** 
* **Code:** 200  
  **Content:**   `{ message : "Success get blog" }`
    `{ <blogs_object> }`  
* **Error Response:**  
  * **Code:** 404  
  **Content:** `{ message : "Blog not found" }` 
  OR
   * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

### POST /v1/blogs/
----
  Create blog content.
* **URL Params**  
None
* **Headers**  
  Content-Type: application/json
  Authorization:  `<Bearer Token (JWT)>`  
* **Data Params**  
`{ <blogs_object> }`
* **Success Response:**  
* **Code:** 200  
  **Content:**  `{ message : "Success create blog content" }`
    `{ <blogs_object> }`
* **Error Response:**  
  * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

### PUT /v1/blogs/{blog_id}
----
Update blog content base on blog id
 
* **URL Params**  
  *Required:* `blog_id=[integer]`
* **Headers**  
  Content-Type: application/json
  Authorization:  `<Bearer Token (JWT)>`  
* **Data Params**  
```
	{
		title: string
		body_text: string
		visibility: boolean
		image_path: string
	}
```
* **Success Response:**  
* **Code:** 200  
  **Content:**  `{ message : "Success create blog content" }`
    `{ <blogs_object> }`
* **Error Response:**  
  * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

### DELETE /v1/blogs/{blog_id}
----
Delete blog content base on blog id

* **URL Params**  
  *Required:* `blog_id=[integer]`
* **Headers**  
  Content-Type: application/json
  Authorization:  `<Bearer Token (JWT)>`  
* **Data Params**  
	None
* **Success Response:**  
* **Code:** 200  
  **Content:**  `{ message : "Success delete blog" }`
    `{ <blogs_object> }`
* **Error Response:**  
  * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

## 7. Case-studies

case_study object
```
	{
		work_id: integer
		title: string
		body_text: string
		visibility: boolean
		created_at: datetime()
		updated_at: datetime()
		deleted_at: datetime()
		created_by: string
		updated_by: string
		deleted_by: string
		image_path: string
	}
```

### GET /v1/case_studies/

  Returns image base on image name in the system.

* **URL Params**  
	None
* **Data Params**  
  None
* **Headers**  
  Content-Type: file/image 
* **Success Response:** 
* **Code:** 200  
  **Content:**  `{ message : "Success get case study" }`
    `{ <case_study_object> }`    
* **Error Response:**  
   * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`


### GET /v1/case_studies?page_number={integer}&item_per_page={integer}&filter_by_id={boolean}

  Returns image base on image name in the system.

* **URL Params**  
	None
* **Data Params**  
  None
* **Headers**  
  Content-Type: file/image 
* **Success Response:** 
* **Code:** 200  
  **Content:**  `{ message : "Success get case study" }`
    `{ <case_study_object> }`    
* **Error Response:**  
   * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

### GET /v1/case_studies/{case_study_id}

  Returns image base on image name in the system.

* **URL Params**  
  *Required:* `case_study_id=[integer]`
* **Data Params**  
  None
* **Headers**  
  Content-Type: file/image 
* **Success Response:** 
* **Code:** 200  
  **Content:**   `{ message : "Success get case study" }`
	```
	{
	  page_number: integer 
	  item_per_page: integer
	  filter_by_id: boolean
	  users: 
	  [
          {<case_study_object>},
          {<case_study_object>},
          {<case_study_object>}
	  ]
	}
	```  
* **Error Response:**  
  * **Code:** 404  
  **Content:** `{ message : "case study not found" }` 
  OR
   * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

### POST /v1/case_studies/
----
Create new case study
* **URL Params**  
  *Required:* `case_study_id=[integer]`
* **Headers**  
  Content-Type: application/json
  Authorization:  `<Bearer Token (JWT)>`  
* **Data Params**  
`{ <case_study_object> }`
* **Success Response:**  
* **Code:** 200  
  **Content:**  `{ message : "Success create case study content" }`
    `{ <blogs_object> }`
* **Error Response:**  
  * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

### PUT /v1/case_studies/{case_study_id}
----
Update case study base on id
* **URL Params**  
  *Required:*`case_study_id=[integer]`
* **Headers**  
  Content-Type: application/json
  Authorization:  `<Bearer Token (JWT)>`  
* **Data Params**  
```
	{
		title: string
		body_text: string
		visibility: boolean
		image_path: string
	}
```
* **Success Response:**  
* **Code:** 200  
  **Content:**  `{ message : "Success create case study content" }`
    `{ <case_study_object> }`
* **Error Response:**  
  * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

### DELETE /v1/case_studies/{case_study_id}
----
Delete case study base on id
* **URL Params**  
  *Required:* `case_study_id=[integer]`
* **Headers**  
  Content-Type: application/json
  Authorization:  `<Bearer Token (JWT)>`  
* **Data Params**  
	None
* **Success Response:**  
* **Code:** 200  
  **Content:**  `{ message : "Success delete case study" }`
    `{ <case_study_object> }`
* **Error Response:**  
  * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`
