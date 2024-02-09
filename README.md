

## 1. Authentication

* User object
```
{
  user_id: integer
  role_id: integer
  username: string
  email: string
  password: string
  created_at: datetime()
  updated_at: datetime()
  deactivated_at: datetime()
}
```
User-data object
```
{
  user_id: integer
  role_id: integer
  username: string
  created_at: datetime()
  updated_at: datetime()
  deactivated_at: datetime()
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
	  role_id: string
	  role_name: string
	  access_to_user_management: boolean
	  access_to_product: boolean
	  access_to_case_studies: boolean
	  access_to_blog: boolean
  }
```
* **Success Response:**  
* **Code:** 200  
  **Content:**  `{ message : "Success create roles" }`
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
		subscription_at
		category_id: integer 
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

### GET /v1/subscribers/?page_number={integer}&item_per_page={integer}

  Returns all subscriber with pagination.

* **URL Params**  
	None
* **Data Params**  
  Query Parameter: 
	  page_number: `<page_number>` 
	  item_per_page: `<page_size>`
* **Headers**  
  Content-Type: application/json 
* **Success Response:** 
* **Code:** 200  
  **Content:**  `{ message : "Success get subscriber" }` 
	```
	{
	  page_number: integer 
	  item_per_page: integer
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


## 5. Blogs

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
		image_path: JSON
	}
```

### GET /v1/blogs/

  Returns all blog

* **URL Params**  
	None
* **Data Params**  
  None
* **Headers**  
  Content-Type: application/json
* **Success Response:** 
* **Code:** 200  
  **Content:**  `{ message : "Success get blog" }`
    `{ <blog_object> }`    
* **Error Response:**  
   * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

### GET /v1/blogs?page_number={integer}&item_per_page={integer}&filter_by_id={boolean}

   Returns all blogs with pagination.

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
	  data: 
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

  Returns blog base on blog id.

* **URL Params**  
  *Required:* `blog_id=[integer]`
* **Data Params**  
  None
* **Headers**  
  Content-Type: application/json
* **Success Response:** 
* **Code:** 200  
  **Content:**   `{ message : "Success get blog" }`
    `{ <blog_object> }`  
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
    `{ <blog_object> }`
* **Error Response:** 
  * **Code:** 404  
  **Content:** `{ message : "Blog not found" }` 
  OR 
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
		image_path: JSON
	}
```
* **Success Response:**  
* **Code:** 200  
  **Content:**  `{ message : "Success create blog content" }`
    `{ <blog_object> }`
* **Error Response:**
  * **Code:** 404  
  **Content:** `{ message : "Blog not found" }` 
  OR  
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
    `{ <blog_object> }`
* **Error Response:**
  * **Code:** 404  
  **Content:** `{ message : "Blog not found" }` 
  OR  
  * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

## 6. Case-studies

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
		category_id: integer
		image_path: JSON
	}
```

### GET /v1/case_studies/

  Returns all case study

* **URL Params**  
	None
* **Data Params**  
  None
* **Headers**  
  Content-Type: application/json
* **Success Response:** 
* **Code:** 200  
  **Content:**  `{ message : "Success get case study" }`
```
	{
	  data: 
	  [
          {<case_study_object>},
          {<case_study_object>},
          {<case_study_object>}
	  ]
	}
```  
  
* **Error Response:**  
   * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`


### GET /v1/case_studies?page_number={integer}&item_per_page={integer}

  Returns all case study with pagination

* **URL Params**  
	None
* **Data Params**  
	  page_number: `<page_number>` 
	  item_per_page: `<page_size>`
* **Headers**  
  Content-Type: application/json
* **Success Response:** 
* **Code:** 200  
  **Content:**  `{ message : "Success get case study" }`
```
	{
	  page_number: integer 
	  item_per_page: integer
	  data: 
	  [
          {<case_study_object>},
          {<case_study_object>},
          {<case_study_object>}
	  ]
	}
```  
* **Error Response:**  
   * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

### GET /v1/case_studies/{work_id}

  Returns case study base on case study id

* **URL Params**  
  *Required:* `work_id=[integer]`
* **Data Params**  
  None
* **Headers**  
  Content-Type: application/json
* **Success Response:** 
* **Code:** 200  
  **Content:**   `{ message : "Success get case study" }`
	    `{ <case_study_object> }`  
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
None
* **Headers**  
  Content-Type: application/json
  Authorization:  `<Bearer Token (JWT)>`  
* **Data Params**  
`{ <case_study_object> }`
* **Success Response:**  
* **Code:** 200  
  **Content:**  `{ message : "Success create case study content" }`
    `{ <case_study_object> }`
* **Error Response:**  
  * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

### PUT /v1/case_studies/{case_study_id}
----
Update case study base on id
* **URL Params**  
  *Required:*`work_id=[integer]`
* **Headers**  
  Content-Type: application/json
  Authorization:  `<Bearer Token (JWT)>`  
* **Data Params**  
```
	{
		title: string
		body_text: string
		visibility: boolean
		image_path: JSON
	}
```
* **Success Response:**  
* **Code:** 200  
  **Content:**  `{ message : "Success create case study content" }`
    `{ <case_study_object> }`
* **Error Response:**
  * **Code:** 404  
  **Content:** `{ message : "case study not found" }` 
  OR  
  * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

### DELETE /v1/case_studies/{case_study_id}
----
Delete case study base on id
* **URL Params**  
  *Required:* `work_id=[integer]`
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
  * **Code:** 404  
  **Content:** `{ message : "case study not found" }` 
  OR
  * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

## 7. Products

product object
```
	{
		product_id: integer
		title: string
		body_goals: string
		body_features: string
		visibility: boolean
		created_at: datetime()
		updated_at: datetime()
		deleted_at: datetime()
		created_by: string
		updated_by: string
		deleted_by: string
		image_path: JSON
	}
```

### GET /v1/products/

  Returns all page information

* **URL Params**  
	None
* **Data Params**  
  None
* **Headers**  
  Content-Type: application/json
* **Success Response:** 
* **Code:** 200  
  **Content:**  `{ message : "Success get products information" }`
```
	{
	  data: 
	  [
          {<product_object>},
          {<product_object>},
          {<product_object>}
	  ]
	}
```   
* **Error Response:**  
   * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`


### GET /v1/products?page_number={integer}&item_per_page={integer}

  Returns all page information with pagination

* **URL Params**  
	None
* **Data Params**  
	  page_number: `<page_number>` 
	  item_per_page: `<page_size>`
* **Headers**  
  Content-Type: application/json
* **Success Response:** 
* **Code:** 200  
  **Content:**  `{ message : "Success get product information" }`

```
	{
	  page_number: integer 
	  item_per_page: integer
	  data: 
	  [
          {<product_object>},
          {<product_object>},
          {<product_object>}
	  ]
	}
```   
* **Error Response:**  
   * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

### GET /v1/products/{product_id}

  Returns page information base on page id

* **URL Params**  
  *Required:* `product_id=[integer]`
* **Data Params**  
  None
* **Headers**  
  Content-Type: application/json
* **Success Response:** 
* **Code:** 200  
  **Content:**   `{ message : "Success get product information" }`
    `{ <product_object> }`  
* **Error Response:**  
  * **Code:** 404  
  **Content:** `{ message : "product information not found" }` 
  OR
   * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

### POST /v1/products/
----
Create page information study
* **URL Params**  
None
* **Headers**  
  Content-Type: application/json
  Authorization:  `<Bearer Token (JWT)>`  
* **Data Params**  
`{ <product_object> }`
* **Success Response:**  
* **Code:** 200  
  **Content:**  `{ message : "Success create product information" }`
    `{ <product_object> }`
* **Error Response:**  
  * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

### PUT /v1/products/{product_id}
----
Update page information base on id
* **URL Params**  
  *Required:*`product_id=[integer]`
* **Headers**  
  Content-Type: application/json
  Authorization:  `<Bearer Token (JWT)>`  
* **Data Params**  
```
	{
		product_id: integer
		title: string
		body_goals: string
		body_features: string
		visibility: boolean
		image_path: JSON
	}
```
* **Success Response:**  
* **Code:** 200  
  **Content:**  `{ message : "Success update product" }`
    `{ <product_object> }`
* **Error Response:**  
  * **Code:** 404  
  **Content:** `{ message : "product information not found" }` 
  OR
  * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

### DELETE /v1/products/{product_id}
----
Delete case study base on id
* **URL Params**  
  *Required:* `product_id=[integer]`
* **Headers**  
  Content-Type: application/json
  Authorization:  `<Bearer Token (JWT)>`  
* **Data Params**  
	None
* **Success Response:**  
* **Code:** 200  
  **Content:**  `{ message : "Success delete product information" }`
    `{ <product_object> }`
* **Error Response:**  
  * **Code:** 404  
  **Content:** `{ message : "product information not found" }` 
  OR
  * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`
 
## 8. FAQ

FAQ object
```
	{
		product_faq_id: string
		product_id: string
		faq_content: JSON
		key_technology: JSON
	}
```

### GET /v1/products/faq

  Returns all page information

* **URL Params**  
	None
* **Data Params**  
  None
* **Headers**  
  Content-Type: application/json
* **Success Response:** 
* **Code:** 200  
  **Content:**  `{ message : "Success get FAQ information" }`
```
	{
	  data: 
	  [
          {<product_object>},
          {<product_object>},
          {<product_object>}
	  ]
	}
```   
* **Error Response:**  
   * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

### POST /v1/products/faq
----
Create page information study
* **URL Params**  
None
* **Headers**  
  Content-Type: application/json
  Authorization:  `<Bearer Token (JWT)>`  
* **Data Params**  
`{ <product_object> }`
* **Success Response:**  
* **Code:** 200  
  **Content:**  `{ message : "Success create FAQ information" }`
    `{ <faq_object> }`
* **Error Response:**  
  * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

### PUT /v1/products/faq/
----
Update page information base on id
* **URL Params**  
	None
* **Headers**  
  Content-Type: application/json
  Authorization:  `<Bearer Token (JWT)>`  
* **Data Params**  
    `{ <faq_object> }`
* **Success Response:**  
* **Code:** 200  
  **Content:**  `{ message : "Success FAQ product" }`
    `{ <faq_object> }`
* **Error Response:**  
  * **Code:** 404  
  **Content:** `{ message : "FAQ not found" }` 
  OR
  * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

### DELETE /v1/products/faq
----
Delete page information base on id
* **URL Params**  
	None
* **Headers**  
  Content-Type: application/json
  Authorization:  `<Bearer Token (JWT)>`  
* **Data Params**  
	None
* **Success Response:**  
* **Code:** 200  
  **Content:**  `{ message : "Success delete FAQ" }`
    `{ <faq_object> }`
* **Error Response:** 
  * **Code:** 404  
  **Content:** `{ message : "FAQ not found" }` 
  OR 
  * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

## 9. Features

product_feature object
```
	{
		product_feature_id: string
		product_id : string
		feature_id: string
		title: string
		content: string
	}
```


feature object
```
	{
		feature_id: string
		title: string
		content: string
	}
```

### GET /v1/products/feature/{product_id}

  Returns all feature information with product id

* **URL Params**  
	None
* **Data Params**  
  None
* **Headers**  
  Content-Type: application/json
* **Success Response:** 
* **Code:** 200  
  **Content:**  `{ message : "Success get key technology information" }`
```
	{
	  data: 
	  [
          {<feature_object>},
          {<feature_object>},
          {<feature_object>}
	  ]
	}
```   
* **Error Response:**  
   * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

### POST /v1/products/featuers/{product_id}
----
Create page information study
* **URL Params**  
None
* **Headers**  
  Content-Type: application/json
  Authorization:  `<Bearer Token (JWT)>`  
* **Data Params**  
`{ <keyt_object> }`
* **Success Response:**  
* **Code:** 200  
  **Content:**  `{ message : "Success create key technology information" }`
    `{ <keyt_object> }`
* **Error Response:**  
  * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

### PUT /v1/products/feature/{product_id}/{feature_id}
----
Update page information base on id
* **URL Params**  
	None
* **Headers**  
  Content-Type: application/json
  Authorization:  `<Bearer Token (JWT)>`  
* **Data Params**  
    `{ <feature_object> }`
* **Success Response:**  
* **Code:** 200  
  **Content:**  `{ message : "Success update product" }`
    `{ <keyt_object> }`
* **Error Response:**  
  * **Code:** 404  
  **Content:** `{ message : "product information not found" }` 
  OR
  * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

### DELETE /v1/products/{product_id}/{feature_id}
----
Delete page information base on id
* **URL Params**  
	None
* **Headers**  
  Content-Type: application/json
  Authorization:  `<Bearer Token (JWT)>`  
* **Data Params**  
	None
* **Success Response:**  
* **Code:** 200  
  **Content:**  `{ message : "Success delete key technology information" }`
    `{ <feature_object> }`
* **Error Response:** 
  * **Code:** 404  
  **Content:** `{ message : "key technology not found" }` 
  OR 
  * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

## 10. Page information (AllPages)

Save data about static page information.

page object (buat schema ini dengan menggabungkan seluruh table yang berhubungan dengan AllPage)

page object
```
   {
        page_id: integer
        page_name : string
        content: JSON
        created_by: string
        updated_by: string
    }
```

AllComponent object
```
   {
        component_id: integer
        content: JSON
    }
```

### GET /v1/pages/

  Returns all page information

* **URL Params**  
	None
* **Data Params**  
  None
* **Headers**  
  Content-Type: application/json
* **Success Response:** 
* **Code:** 200  
  **Content:**  `{ message : "Success page information" }`
    `{ <page_object> }`    
* **Error Response:**  
   * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`


### GET /v1/pages?page_number={integer}&item_per_page={integer}

  Returns all page information with pagination

* **URL Params**  
	None
* **Data Params**  
	  page_number: `<page_number>` 
	  item_per_page: `<page_size>`
* **Headers**  
  Content-Type: application/json
* **Success Response:** 
* **Code:** 200  
  **Content:**  `{ message : "Success get case study" }`

```
	{
	  page_number: integer 
	  item_per_page: integer
	  data: 
	  [
          {<page_object>},
          {<page_object>},
          {<page_object>}
	  ]
	}
```   
* **Error Response:**  
   * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

### GET /v1/pages/{page_id}

  Returns page information base on page id

* **URL Params**  
  *Required:* `page_id=[integer]`
* **Data Params**  
  None
* **Headers**  
  Content-Type: application/json
* **Success Response:** 
* **Code:** 200  
  **Content:**   `{ message : "Success get page information" }`
    `{ <page_object> }`  
* **Error Response:**  
  * **Code:** 404  
  **Content:** `{ message : "page information not found" }` 
  OR
   * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

### POST /v1/pages/
----
Create page information study
* **URL Params**  
None
* **Headers**  
  Content-Type: application/json
  Authorization:  `<Bearer Token (JWT)>`  
* **Data Params**  
`{ <page_object> }`
* **Success Response:**  
* **Code:** 200  
  **Content:**  `{ message : "Success create page information" }`
    `{ <blogs_object> }`
* **Error Response:**  
  * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

### PUT /v1/pages/{page_id}
----
Update page information base on id
* **URL Params**  
  *Required:*`page_id=[integer]`
* **Headers**  
  Content-Type: application/json
  Authorization:  `<Bearer Token (JWT)>`  
* **Data Params**  
```
	{
        name : string
        content: JSON
	}
```
* **Success Response:**  
* **Code:** 200  
  **Content:**  `{ message : "Success update page information" }`
    `{ <page_object> }`
* **Error Response:**
  * **Code:** 404  
  **Content:** `{ message : "page information not found" }` 
  OR  
  * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

### PUT /v1/pages/component/{component_id}
----
Update component information base on id
* **URL Params**  
  *Required:*`page_id=[integer]`
* **Headers**  
  Content-Type: application/json
  Authorization:  `<Bearer Token (JWT)>`  
* **Data Params**  
```
	{
        content: JSON
	}
```
* **Success Response:**  
* **Code:** 200  
  **Content:**  `{ message : "Success update page information" }`
    `{ <component_object> }`
* **Error Response:**
  * **Code:** 404  
  **Content:** `{ message : "page information not found" }` 
  OR  
  * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

### DELETE /v1/pages/{page_id}
----
Delete page information base on id
* **URL Params**  
  *Required:* `page_id=[integer]`
* **Headers**  
  Content-Type: application/json
  Authorization:  `<Bearer Token (JWT)>`  
* **Data Params**  
	None
* **Success Response:**  
* **Code:** 200  
  **Content:**  `{ message : "Success delete page information" }`
    `{ <page_object> }`
* **Error Response:**
  * **Code:** 404  
  **Content:** `{ message : "page information not found" }` 
  OR  
  * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

## 11. Contact

contact object
```
	{
		contact_id: integer
		email: string
		name: string
		message: string
		category_name : string
	}
```

### GET /v1/contact/

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
          {<contact_object>},
          {<contact_object>},
          {<contact_object>}
	  ]
	}
	```     
* **Error Response:**  
   * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

### GET /v1/contact?page_number={integer}&item_per_page={integer}

  Returns contact request with pagination.

* **URL Params**  
	None
* **Data Params**  
	  page_number: `<page_number>` 
	  item_per_page: `<page_size>`
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
          {<contact_object>},
          {<contact_object>},
          {<contact_object>}
	  ]
	}
	```  
* **Error Response:**  
   * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`


### GET /v1/contact/{contact_id}

  Returns contact request base on id

* **URL Params**  
  *Required:* `contact_id=[integer]`
* **Data Params**  
  None
* **Headers**  
  Content-Type: application/json
* **Success Response:** 
* **Code:** 200  
  **Content:**  `{ message : "Success get contact request content" }`  
  `{ <contact_object> }`    
* **Error Response:**  
  * **Code:** 404  
  **Content:** `{ message : "Contact request not found" }` 
  OR
   * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

### POST /v1/contact/
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
  `{ <contact_object> }`  
* **Error Response:**  
  * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

### Delete /v1/contact/{contact_id}

  Delete contact request base on id

* **URL Params**  
  *Required:* `contact_id=[integer]`
* **Data Params**  
  None
* **Headers**  
  Content-Type: application/json
* **Success Response:** 
* **Code:** 200  
  **Content:**  `{ message : "Success delete contact request content" }`  
  `{ <contact_object> }`    
* **Error Response:**  
  * **Code:** 404  
  **Content:** `{ message : "Contact request not found" }` 
  OR
   * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

## 12. Request Demo

request object
```
	{
		request_id: integer
		fullname: string
		company: string
		email: string
		phone_number: string
		message: string
	}
```

### GET /v1/request/

  Returns contact request.

* **URL Params**  
	None
* **Data Params**  
  None
* **Headers**  
  Content-Type: application/json
* **Success Response:** 
* **Code:** 200  
  **Content:**  `{ message : "Success get request demo content" }`  
	```
	{
	  data: 
	  [
          {<request_object>},
          {<request_object>},
          {<request_object>}
	  ]
	}
	```     
* **Error Response:**  
   * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

### GET /v1/request?page_number={integer}&item_per_page={integer}

  Returns contact request with pagination.

* **URL Params**  
	None
* **Data Params**  
	  page_number: `<page_number>` 
	  item_per_page: `<page_size>`
* **Headers**  
  Content-Type: application/json
* **Success Response:** 
* **Code:** 200  
  **Content:**  `{ message : "Success get request demo content" }`  
	```
	{
	  page_number: integer 
	  item_per_page: integer
	  data: 
	  [
          {<request_object>},
          {<request_object>},
          {<request_object>}
	  ]
	}
	```  
* **Error Response:**  
   * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`


### GET /v1/request/{request_id}

  Returns contact request base on id

* **URL Params**  
  *Required:* `request_id=[integer]`
* **Data Params**  
  None
* **Headers**  
  Content-Type: application/json
* **Success Response:** 
* **Code:** 200  
  **Content:**  `{ message : "Success get request demo content" }`  
  `{ <request_object> }`    
* **Error Response:**  
  * **Code:** 404  
  **Content:** `{ message : "request demo not found" }` 
  OR
   * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

### POST /v1/request/
----
  Create contact request
* **URL Params**  
	None
* **Headers**  
  Content-Type: application/json
  Authorization:  `<Bearer Token (JWT)>`  
* **Data Params**  
`{ <request_object> }`
* **Success Response:**  
* **Code:** 200  
  **Content:** `{ message : "Success create request demo content" }`  
  `{ <request_object> }`  
* **Error Response:**  
  * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`

### Delete /v1/request/{request_id}

  Delete contact request base on id

* **URL Params**  
  *Required:* `request_id=[integer]`
* **Data Params**  
  None
* **Headers**  
  Content-Type: application/json
* **Success Response:** 
* **Code:** 200  
  **Content:**  `{ message : "Success delete request demo content" }`  
  `{ <request_object> }`    
* **Error Response:**  
  * **Code:** 404  
  **Content:** `{ message : "request demo not found" }` 
  OR
   * **Code:** 401  
  **Content:** `{ message : "You are unauthorized to make this request." }`
