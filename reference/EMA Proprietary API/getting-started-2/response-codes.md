---
title: Response Codes
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
| Code | Description                                                                                   |
| :--- | :-------------------------------------------------------------------------------------------- |
| 200  | OK - Successful Response                                                                      |
| 201  | CREATED - Resource was created successfully                                                   |
| 400  | BAD REQUEST - The request was bad, often due to a missing required parameter                  |
| 401  | NOT AUTHORIZED- Authentication error, this token is not allowed access to the API.            |
| 403  | FORBIDDEN                                                                                     |
| 404  | NOT FOUND                                                                                     |
| 422  | UNPROCESSABLE ENTITY- Request could not be processed, typically indicates a validation error. |
| 429  | TOO MANY REQUESTS- Request was rate limited, please retry                                     |
| 500  | SERVER ERROR- Internal Server Error                                                           |