
# **API Documentation**

## **Base URL**
The API is hosted at:
```
http://<your-ip>:5000
```

---

## **Endpoints**

### 1. **Create Server**
**URL**: `/create`  
**Method**: `POST`  
**Description**: Creates a new server instance.  

#### **Request Body**
Send a JSON object with the following fields:

| Field Name        | Type    | Description                                    |
|--------------------|---------|------------------------------------------------|
| `lobby_code`       | `string`| Unique identifier for the server.              |
| `lobby_name`       | `string`| Name of the server lobby.                      |
| `current_players`  | `int`   | Current number of players in the lobby.        |
| `max_players`      | `int`   | Maximum number of players allowed in the lobby.|
| `18plus`           | `bool`  | Indicates if the lobby is 18+ only.            |

#### **Example Request**
```json
{
    "lobby_code": "123ABC",
    "lobby_name": "Cool Lobby",
    "current_players": 2,
    "max_players": 10,
    "18plus": true
}
```

#### **Response**
| HTTP Status | Response Example                  | Description                       |
|-------------|-----------------------------------|-----------------------------------|
| `201`       | `{"message": "Server created successfully"}` | Server created.                   |
| `400`       | `{"error": "Missing required fields"}`        | Invalid or incomplete input.       |
| `400`       | `{"error": "Lobby code already exists"}`      | Lobby code is not unique.          |

---

### 2. **Update Server**
**URL**: `/update`  
**Method**: `POST`  
**Description**: Updates the details of an existing server.  

#### **Request Body**
Send a JSON object with the following fields:

| Field Name        | Type    | Description                                         |
|--------------------|---------|-----------------------------------------------------|
| `lobby_code`       | `string`| Unique identifier for the server to update.         |
| `current_players`  | `int`   | Updated number of current players in the lobby.     |
| `lobby_name`       | `string`| *(Optional)* Updated name of the lobby.             |
| `18plus`           | `bool`  | *(Optional)* Updated 18+ status for the lobby.      |

#### **Example Request**
```json
{
    "lobby_code": "123ABC",
    "current_players": 5,
    "lobby_name": "Updated Cool Lobby",
    "18plus": false
}
```

#### **Response**
| HTTP Status | Response Example                        | Description                      |
|-------------|-----------------------------------------|----------------------------------|
| `200`       | `{"message": "Server updated successfully"}` | Server updated.                  |
| `400`       | `{"error": "Missing required fields"}`         | Invalid or incomplete input.      |
| `404`       | `{"error": "Lobby code does not exist"}`       | Lobby code not found.             |

---

### 3. **Close Server**
**URL**: `/close`  
**Method**: `POST`  
**Description**: Removes a server instance from the list.  

#### **Request Body**
Send a JSON object with the following field:

| Field Name        | Type    | Description                                |
|--------------------|---------|--------------------------------------------|
| `lobby_code`       | `string`| Unique identifier for the server to close. |

#### **Example Request**
```json
{
    "lobby_code": "123ABC"
}
```

#### **Response**
| HTTP Status | Response Example                        | Description                      |
|-------------|-----------------------------------------|----------------------------------|
| `200`       | `{"message": "Server closed successfully"}` | Server closed.                   |
| `400`       | `{"error": "Missing required fields"}`         | Invalid or incomplete input.      |
| `404`       | `{"error": "Lobby code does not exist"}`       | Lobby code not found.             |

---

### 4. **Get Servers**
**URL**: `/servers`  
**Method**: `GET`  
**Description**: Retrieves the list of all active server instances.  

#### **Response**
| HTTP Status | Response Example                                           | Description                         |
|-------------|------------------------------------------------------------|-------------------------------------|
| `200`       | `{"servers": [{"lobby_code": "123ABC", "lobby_name": "Cool Lobby", "current_players": 5, "max_players": 10, "18plus": true}]}` | List of servers. |

---

## **Error Responses**
| Error Code | Meaning                     |
|------------|-----------------------------|
| `400`      | Bad request: Missing or invalid fields in the request. |
| `404`      | Resource not found: Server with the specified lobby code does not exist. |

---

## **Testing Notes**
- Replace `<your-ip>` with the actual IP address of the host machine running the API. 
- Ensure the port (`5000`) is open and accessible from the testing device.
- Use tools like Postman or `curl` to test the endpoints.

--- 
