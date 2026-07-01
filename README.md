# gorest-api-assessment
GoRest API Testing Assessement using Postman


# Overview

This repository contains a Postman API test collection developed for the GoRest API assessment.

The collection automates the required API test scenarios and includes an additional bonus cleanup scenario that demonstrates request chaining and test data cleanup.

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# Project Structure

```

GoRest-API-Assessment
│
├── GoRest_API.postman_collection.json
├── GoRest.postman_environment.json
└── README.md

```

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# Prerequisites

Before running the collection, ensure you have:

- Postman (Latest Version)
- Internet connection
- A valid GoRest Access Token

You can generate a free access token from:

https://gorest.co.in/

<img width="1660" height="897" alt="image" src="https://github.com/user-attachments/assets/4b7e921c-4306-49ed-a133-09043c7af5ef" />


--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# Environment Setup

## Step 1 - Import Environment

1. Open Postman.
2. Click **Import**.
3. Select:


GoRest.postman_environment.json

Import the environment.

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Step 2 - Configure Environment Variables

Open the **GoRest** environment.

Update the following variables:

| Variable | Value |
|----------|--------------------------------|
| baseUrl | https://gorest.co.in/public/v2 |
| token | YOUR_GOREST_ACCESS_TOKEN |
| userId | Leave blank (Automatically populated after Scenario 1) |

Example:

```

baseUrl = https://gorest.co.in/public/v2
token = YOUR_GOREST_ACCESS_TOKEN
userId =

```


Click **Save**.

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


# Import Collection

1. Click **Import**.
2. Select:

GoRest_API.postman_collection.json


3. Import the collection.

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# Collection Structure

```

GoRest API Assessment
│
├── Scenario 1 - Create User (POST)
├── Scenario 2 - Get Users (GET)
├── Bonus - Delete User (DELETE)
├── Bonus - Verify Deleted User (GET)
└── Bonus - Get All Users (GET) *Just to verify another whether the deleted user exists in the list of users or not

```



--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


# Request Details

## Scenario 1 - Create User

**Method**

```
POST
```

**Endpoint**

```
{{baseUrl}}/users
```

**Authorization**

Bearer Token

```
{{token}}
```

**Description**

Creates a new user and automatically stores the returned user ID into the environment variable:

```
userId
```

### Validations

- Status Code = 201
- ID is numeric
- Name is string
- Gender is either male or female
- Status is either active or inactive

---

## Scenario 2 - Get Users

**Method**

```
GET
```

**Endpoint**

```
{{baseUrl}}/users
```

**Authorization**

Bearer Token

```
{{token}}
```

### Validations

- Status Code = 200
- Response is an array
- First user's status is either active or inactive

---

## Bonus - Delete User

**Method**

```
DELETE
```

**Endpoint**

```
{{baseUrl}}/users/{{userId}}
```

**Authorization**

Bearer Token

```
{{token}}
```

### Validations

- Status Code = 204
- Response body is empty

---

## Bonus - Verify Deleted User

**Method**

```
GET
```

**Endpoint**

```
{{baseUrl}}/users/{{userId}}
```

### Validations

- Status Code = 404
- Response message equals:

```
Resource not found
```

This confirms that the user created during Scenario 1 has been successfully deleted.


--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


# Execution Instructions

## Option 1 - Run Entire Collection (Recommended)

1. Open Postman.
2. Select the **GoRest** environment.
3. Verify:
   - `baseUrl` is configured.
   - `token` contains a valid GoRest Access Token.
4. Click **Run Collection**.
5. Execute the collection in the following order:

```
1. Scenario 1 - Create User
2. Scenario 2 - Get Users
3. Bonus - Delete User
4. Bonus - Verify Deleted User
5. Bonus - Get All Users (GET) *Just to verify another whether the deleted user exists in the list of users or not
```


## Option 2 - Run Requests Individually

Execute each request manually in the following sequence:

1. Scenario 1 - Create User
2. Scenario 2 - Get Users
3. Bonus - Delete User
4. Bonus - Verify Deleted User
5. 5. Bonus - Get All Users (GET) *Just to verify another whether the deleted user exists in the list of users or not


--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# Expected Results

```

| Request | Expected Status |
|---------|-----------------|
| Scenario 1 - Create User | 201 Created |
| Scenario 2 - Get Users | 200 OK |
| Bonus - Delete User | 204 No Content |
| Bonus - Verify Deleted User | 404 Not Found |

```

All Postman test assertions should pass successfully.

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# Notes

- A unique email address is generated during user creation to prevent duplicate email errors.
- The `userId` environment variable is automatically populated after the user is created and reused in the bonus requests.
- The bonus scenarios demonstrate API request chaining and cleanup of test data.

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


# Author

**Derrick Abbasy**

QA Engineer
