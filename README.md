# Madar Dijla - Application Payment Api

## Postman Collection

- I have uploaded the Postman collection here:
The name of Collection `APP_API_PAY.postman_collection.json`.
[Download the Postman Collection](https://drive.google.com/file/d/1lFKOf-tiEwFeFCXFn8iiHJO_sYeEH2Fy/view?usp=sharing)
- After download it, open it with Postman.
- Test all endpoint below.

## Authentication and Authorization:

### 1. Username and Password to Generate Token
   - Send the username and password to the authentication endpoint to receive a bearer token.
   - The token is used to authenticate subsequent requests.

### 2. Bearer Token Sent with Requests:
   - Include the bearer token in the Authorization header for subsequent requests to access the application data.

## Endpoints

### 1. Login and Get Bearer Token
   - **Endpoint:** `POST http://172.28.1.120:8050/api/auth/login`
   - **Request:**
     ```json
     {
       "username": "Adminpay",
       "password": "adminpay0"
     }
     ```
   - **Response:**
     - **Success (200):**
       ```json
       {
         "isSuccess": true,
         "results": {
           "token": "***********************************************************
             ************************************************"
         },
         "errors": []
       }
       ```
     - **Error (401):**
       ```json
       {
         "isSuccess": false,
         "results": null,
         "errors": ["Invalid credentials"]
       }
       ```
   

### 2. Get Application Data
   - **Endpoint:** `GET http://172.28.1.120:8050/api/user/:appid`
   - **Request Parameters:**
     - `appid`: Application ID (send in long format).
   - **Headers:**
    

| Header          | Description                                        |
|:--------------- |:-------------------------------------------------- |
| `UserName`      | Your username                                      |
| `Password`      | Your password                                      |
| `Token`         | Bearer token generated from login (SHA256 hashed). |
| `Accept`        | `application/json, text/plain, */*`                |
| `Authorization` | `Bearer <Token>` from login.                       |
| `Content-Type`  | `application/json`.                                |


   - **Response:**
     - **Success (200):**
       ```json
       {
         "isSuccess": true,
         "results": {
           "application_ID": "101010213971",
           "created": "2018-01-10T09:34:18.329",
           "useCase": "NEW_VR",
           "brand": "هونداي",
           "licenseNumber": "٤٣٣٣٣ج",
           "licenseNumberLatin": "J43333",
           "appChassisNumber": "JMXSDCS3ALL700437",
           "vehicleType": "النترا"
         },
         "errors": []
       }
       ```
     - **Error (404):**
       ```json
       {
         "isSuccess": false,
         "results": null,
         "errors": ["Application not found"]
       }
       ```

---
## Notes:

- You must include the Bearer token in the `Authorization` header when requesting application data.
- The Bearer token will expire 24 hours after creation. 
