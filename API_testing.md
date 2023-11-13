
<h3>Product Listings API Endpoint:</h3>

List of products 
  - check if there are correct info (name, description, price..) 

```
GET /api/products
```

Filtering by category
  -  check filtering options and confirm that the response is expected result
```
GET https://automationteststore.com/api/products?category=fragrance
```

Sorting
  - test sorting options (Date Old > New, Price Low > High, Name A - Z) and verify that the order is correct in the response

```
GET https://automationteststore.com/api/products?sort=price_desc
```

Handling errors
  - Ensure that appropriate error codes and messages are returned

```
GET https://automationteststore.com/api/products/invalid_id
```
```
POST https://automationteststore.com/api/orders
{
  "user_id": "user1",
  "products": [
    {"product_id": "invalid_product_id", "quantity": 1}
  ]
}
```

<h3>Placing order </h3>

Placing new order
  - test placing new order 

```
POST https://automationteststore.com/api/orders
{
  "user_id": "user1",
  "products": [
    {"product_id": "prod1", "quantity": 2},
    {"product_id": "prod2", "quantity": 1}
  ]
}
```
Invalid Product in Order:

```
POST https://automationteststore.com/api/orders
{
  "user_id": "user123",
  "products": [
    {"product_id": "invalid_product_id", "quantity": 1}
  ]
}
```

<h4>User registration</h4>

Successful User Registration:

```
POST https://automationteststore.com/api/register
{
  "username": "user1",
  "email": "user1@gmail.com",
  "password": "SecureP@ssword123"
}
```

Attempting to register with an existing email

```
POST https://automationteststore.com/api/register
{
  "username": "user1",
  "email": "user1@gmail.com",
  "password": "SecureP@ssword123"
}
```

Input Validation (invalid email format)

```
POST https://automationteststore.com/api/register
{
  "username": "user1",
  "email": "user1mail",
  "password": "SecureP@ssword123"
}
```

Updating user profile 

```
PUT https://automationteststore.com/api/users/user123
{
  "username": "updated_user",
  "email": "updated_user@example.com"
}
```



Authentication Check:

  - test with an unauthenticated request and ensure it is denied.
