
# 🧪 API Testing Project – Rahul Shetty Academy

This project showcases API testing using Postman to interact with the Rahul Shetty Academy eCommerce platform. It demonstrates how to authenticate users, manage products, create and delete orders, and validate full backend functionality through API calls.

## 🔗 Website Under Test

- Web UI: (https://rahulshettyacademy.com/client/)
- Base API: `https://rahulshettyacademy.com/api/ecom/`

---

## 🔐 Authentication & Token Management

This project begins by logging in to the API to retrieve a valid token:

- **Endpoint**:  
  `POST /auth/login`

- The response includes a JWT token used for authenticating further requests.

- The token is stored dynamically using a script in the **Tests** tab:
  ```javascript
  let response = pm.response.json();
  pm.environment.set("authToken", response.token);
  ```

- All secured requests use this token in the `Authorization` header:
  ```http
  Authorization: Bearer {{authToken}}
  ```

This approach simulates real-world API login flows and avoids manual token reuse.

---

## 🛍️ Product Management

### ➕ Add Product

- **Endpoint**:  
  `POST /product/add-product`

- Includes `form-data` and an image file.
- The response returns the `productId`, which is stored for later use:
  ```javascript
  let response = pm.response.json();
  pm.environment.set("productId", response.productId);
  ```

### 🗑️ Delete Product

- **Endpoint**:  
  `DELETE /product/delete-product/{{productId}}`

- Authenticated using the saved token.
- Used to remove test products or clean up after order deletion.

---

## 📦 Order Lifecycle via API

### 🛒 Create Order

- **Endpoint**:  
  `POST /order/create-order`

- Takes product ID(s) and user information in the body.

- The response includes an `orderId`, saved using:
  ```javascript
  let response = pm.response.json();
  pm.environment.set("orderId", response.orders[0]);
  ```

### 📄 View Order Details

- **Endpoint**:  
  `GET /order/get-orders-details`

- Returns order details using the stored `orderId`.

### 🗑️ Delete Order

- **Endpoint**:  
  `DELETE /order/delete-order`

- Used to simulate order cancellation or system cleanup.

---

## 🔁 Chained Workflow

This collection uses **chained requests** with Postman environment variables to automate:

1. 🔐 Login → get `authToken`
2. 🛍️ Add Product → store `productId`
3. 🛒 Create Order → store `orderId`
4. 📄 View Order → validate
5. 🗑️ Delete Order → clean up
6. 🧹 Delete Product → clean up

This helps in testing secure flows, state dependencies, and complete business logic.

---

## 🔄 End-to-End API Scenario

This project represents a **complete end-to-end testing scenario** simulating an eCommerce flow via backend API calls:

- Authenticated login
- Product creation and deletion
- Order creation, viewing, and deletion

### ✅ Benefits:

- Covers backend business logic without UI interaction
- Ensures secure token-based communication
- Tests integration between product and order modules
- Validates system behavior under realistic conditions

---

## 📁 Project Structure

| File/Folder                  | Description                                  |
|-----------------------------|----------------------------------------------|
| `My_API_Collection.json`    | Postman collection with all test requests    |
| `README.md`                 | Full project documentation and workflow      |

---

## 👩‍💻 Author

**Rozan Abukweek**  
QA Engineer | API Testing | Postman Automation
