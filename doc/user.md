# User API Spec
## Register User

Endpoint : POST `/api/users`

Request Body :
```
{
    "username" : "bagas",
    "password" : "rahasia",
    "name" : "Bagas Uwaidha"
}
```

Response Body (Success) :
```
{ 
    "data" : {
        "username" : "bagas",
        "name" : "Bagas Uwaidha"
    }
}
```

Response Body (Failed - missing fields) :
```
{ 
    "errors" : "Username, password, name must be filled"
}
```
Response Body (Failed - username exists):
```
{
  "errors": "Username already taken"
}
```

- 🟩 ```201``` Created – Berhasil register

- 🟨 ```400``` Bad Request – Input tidak lengkap atau validasi gagal

- 🟥 ```409``` Conflict – Username sudah digunakan

## Login User

Endpoint: POST `/api/users/login`

Request Body:
```
{
    "username": "bagas",
    "password": "rahasia"
}
```

Response Body (Success):
```
{
    "data": {
        "token": "jwt_token_here",
        "username": "bagas",
        "name": "Bagas Uwaidha"
    }
}
```

Response Bosy (Failed):
```
{
    "errors": "Invalid username or password"
}
```

- 🟩 `200` OK – Berhasil login
- 🟥 `401` Unauthorized – Username atau password salah

## Get User

Endpoint: GET `/api/users/me`

Headers:
```
Authorization: Bearer <jwt_token_here>
```

Response Body (Success):
```
{
    "data": {
        "username": "bagas",
        "name": "Bagas Uwaidha"
    }
}
```

Response Body (Failed):
```
{
    "errors": "Unauthorized"
}
```

- 🟩 `200` OK – Profil berhasil diambil
- 🟥 `401` Unauthorized – Token tidak valid atau tidak disediakan

## Update User

Endpoint: PUT `/api/users`

Headers:
```
Authorization: Bearer <jwt_token_here>
```

Request Body 
```
{
    "name": "Bagas Updated",
    "password": "password_baru"
}
```
Response Body (Success):
```
{
    "data": {
        "username": "bagas",
        "name": "Bagas Updated"
    }
}
```

Response Body (Failed - no fields sent):
```
{
    "errors": "No fields to update"
}
```

Response Body (Failed - unauthorized):
```
{
    "errors": "Unauthorized"
}
```

- 🟩 `200` OK – Berhasil update data
- 🟨 `400` Bad Request – Tidak ada field yang dikirim
- 🟥 `401` Unauthorized – Token tidak valid

## Logout User

Endpoint: POST `/api/users/logout`

Headers: 
```
Authorization: Bearer <jwt_token_here>
```
Response Body (Success):
```
{
    "message": "Logout successful"
}
```
Response Body (Failed):
```
{
    "errors": "Unauthorized"
}
```

- 🟩 `200` OK – Logout berhasil
- 🟥 `401` Unauthorized – Token tidak valid atau sudah expired