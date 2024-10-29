# Libray API

## Introduction

  * Overview: An API Library used by library admins to add, modify books and monitor users.
  * Authentication: Explain the authentication methods used (e.g., API keys, OAuth, basic auth).
  * Error Handling: Describe the error codes and response formats for different error scenarios.
      
# Endpoints

## Endpoint 1: /users/register

   * Method: **POST**
   * Description: Registers a new user in the system by saving their email, username, and password in the database.
   * Request Parameters:
   
       - Parameter 1: email
           * Type: string
           * Description: The email address of the user.
           * Required: Yes
           * Example:

                 savannahjaneducusin@gmail.com
             
       - Parameter 2: username
           * Type: string
           * Description: The desired username of the user.
           * Required: Yes
           * Example:
           
                 Saviee

       - Parameter 3: password
           * Type: string
           * Description: The password chosen by the user, which will be securely hashed before.
           * Required: Yes
           * Example:

                 p@$$w0rd!
             
   * Response:
       - Success Response:
           * Status Code: 200
           * Response Body:
             
                 {
                     "status": "success",
                     "data": null
                 }
             
       - Error Response:
           - Missing Fields
             * Status Code: 400
             * Error Message:
               
                   {
                       "status": "fail",
                       "data": {
                           "Message": "Fields cannot be empty."
                       }
                   }
               
           - Email Already Exists
             * Status Code: 400
             * Error Message:
              
                   {
                       "status": "fail",
                       "data": {
                           "Message": "Invalid Email! Try another one."
                       }
                   }

            - Registration Failure
              * Status Code: 500
              * Error Message:
               
                    {
                        "status": "fail",
                        "data": {
                            "Message": "Registration failed."
                        }
                    }

                
## Endpoint 2: /users/login

   * Method: POST
   * Description: Authenticates a user by verifying their email and password. If successful, generates a JSON Web Token (JWT) for the user.
   * Request Parameters:
   
       - Parameter 1: email
           * Type: string
           * Description: The email address of the user.
           * Required: Yes
           * Example:

                 savannahjaneducusin@gmail.com

       - Parameter 2: password
           * Type: string
           * Description: The password for the user’s account.
           * Required: Yes
           * Example:

                 p@$$w0rd!
             
   * Response:
       - Success Response:
           * Status Code: 200
           * Response Body:
             
                 {
                     "status": "success",
                     "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOi8vbGlicmFyeS5vcmciLCJhdWQiOiJodHRwOi8vbGlicmFyeS5jb20iLCJpYXQiOjE3MzAxNjUwMjMsImV4cCI6MTczMDE2ODYyMywiZGF0YSI6eyJ1c2VyaWQiOiIxIiwibmFtZSI6ImFkbWluIiwiYWNjZXNzX2xldmVsIjoiYWRtaW4ifX0.Yyw03t-aNg_dY8Q0sA0QqFWH5L6DKwqz8_75ln7GlXo"
                 }

           * token: string - A JWT token generated for the user. Valid for 1 hour for admin users and 2 hours for regular users.
             
       - Error Response:
           - Invalid Credentials
             * Status Code: 401
             * Error Message:
               
                   {
                       "status": "fail",
                       "data": {
                           "Message": "Invalid email or password."
                       }
                   }
               
           - Login Failure
             * Status Code: 500
             * Error Message:
              
                   {
                       "status": "fail",
                       "data": {
                           "Message": "Login failed."
                       }
                   }
               


## Endpoint 3: /books/add

   * Method: POST
   * Description: Allows an admin to add a new book to the library. Requires a valid admin JWT token for authorization.
   * Request Parameters:
   
       - Parameter 1: author
           * Type: string
           * Description: The name of the author of the book. If the author does not exist, a new entry will be created.
           * Required: Yes
           * Example:

                 William Shakespear

       - Parameter 2: title
           * Type: string
           * Description: The title of the book.
           * Required: Yes
           * Example:

                 Romeo and Juliet

       - Parameter 3: genre
           * Type: string
           * Description: The genre of the book.
           * Required: Yes
           * Example:

                 Fantasy/Romantic/Tragic
        
       - Parameter 4: token
           * Type: string
           * Description: A JWT token required for authentication. Only admins can add books.
           * Required: Yes
           * Example:

                 eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOi8vbGlicmFyeS5vcmciLCJhdWQiOiJodHRwOi8vbGlicmFyeS5jb20iLCJpYXQiOjE3MzAxNjUwMjMsImV4cCI6MTczMDE2ODYyMywiZGF0YSI6eyJ1c2VyaWQiOiIxIiwibmFtZSI6ImFkbWluIiwiYWNjZXNzX2xldmVsIjoiYWRtaW4ifX0.Yyw03t-aNg_dY8Q0sA0QqFWH5L6DKwqz8_75ln7GlXo
             
   * Response:
       - Success Response:
           * Status Code: 200
           * Response Body:
             
                 {
                     "status": "success",
                     "new_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOi8vbGlicmFyeS5vcmciLCJhdWQiOiJodHRwOi8vbGlicmFyeS5jb20iLCJpYXQiOjE3MzAxNjUwMjMsImV4cCI6MTczMDE2ODYyMywiZGF0YSI6eyJ1c2VyaWQiOiIxIiwibmFtZSI6ImFkbWluIiwiYWNjZXNzX2xldmVsIjoiYWRtaW4ifX0.Yyw03t-aNg_dY8Q0sA0QqFWH5L6DKwqz8_75ln7GlXo"
                 }

           * new_token: string - A new JWT token generated upon successful addition of the book. This new token is valid for 1 hour.
             
       - Error Response:
           - Access Denied (Non-Admin User)
             * Status Code: 403
             * Error Message:
               
                   {
                       "status": "fail",
                       "data": {
                           "Message": "Access Denied. Only admins can add books."
                       }
                   }
               
           - Invalid Token
             * Status Code: 401
             * Error Message:
              
                   {
                       "status": "fail",
                       "data": {
                           "Message": "Token is invalid or outdated."
                       }
                   }
               
           - Database Error
             * Status Code: 500
             * Error Message:
              
                   {
                       "status": "fail",
                       "data": {
                           "Message": "Error message from the database."
                       }
                   }

           - JWT Decoding Error
             * Status Code: 401
             * Error Message:
              
                   {
                       "status": "fail",
                       "data": {
                           "Message": "Failed to decode JWT token."
                       }
                   }  


## Endpoint 4: /books/update

   * Method: POST
   * Description: Allows an admin to update the details of an existing book in the library, including author, title, and genre. Requires a valid admin JWT token for authorization.
   * Request Parameters:

       - Parameter 1: bookCode
           * Type: string
           * Description: Unique identifier for the book to be updated
           * Required: Yes
           * Example: 

                 123AB
   
       - Parameter 2: author
           * Type: string
           * Description: New author of the book. If the author does not exist, a new entry will be.
           * Required: Yes
           * Example:

                 William Shakepears

       - Parameter 3: title
           * Type: string
           * Description: New title of the book.
           * Required: Yes
           * Example:

                 Romeo & Juliet

       - Parameter 4: genre
           * Type: string
           * Description: New genre of the book
           * Required: Yes
           * Example:

                 Fantasy
        
       - Parameter 5: token
           * Type: string
           * Description: A JWT token required for authentication. Only admins can update books.
           * Required: Yes
           * Example:

                 eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOi8vbGlicmFyeS5vcmciLCJhdWQiOiJodHRwOi8vbGlicmFyeS5jb20iLCJpYXQiOjE3MzAxNjUwMjMsImV4cCI6MTczMDE2ODYyMywiZGF0YSI6eyJ1c2VyaWQiOiIxIiwibmFtZSI6ImFkbWluIiwiYWNjZXNzX2xldmVsIjoiYWRtaW4ifX0.Yyw03t-aNg_dY8Q0sA0QqFWH5L6DKwqz8_75ln7GlXo
             
   * Response:
       - Success Response:
           * Status Code: 200
           * Response Body:
             
                 {
                     "status": "success",
                     "new_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOi8vbGlicmFyeS5vcmciLCJhdWQiOiJodHRwOi8vbGlicmFyeS5jb20iLCJpYXQiOjE3MzAxNjUwMjMsImV4cCI6MTczMDE2ODYyMywiZGF0YSI6eyJ1c2VyaWQiOiIxIiwibmFtZSI6ImFkbWluIiwiYWNjZXNzX2xldmVsIjoiYWRtaW4ifX0.Yyw03t-aNg_dY8Q0sA0QqFWH5L6DKwqz8_75ln7GlXo"
                 }

           * new_token: string - A new JWT token generated upon successful addition of the book. This new token is valid for 1 hour.
             
       - Error Response:
           - Access Denied (Non-Admin User)
             * Status Code: 403
             * Error Message:
               
                   {
                       "status": "fail",
                       "data": {
                           "Message": "Access Denied. Only admins can update books."
                       }
                   }
               
           - Invalid Token
             * Status Code: 401
             * Error Message:
              
                   {
                       "status": "fail",
                       "data": {
                           "Message": "Token is invalid or outdated."
                       }
                   }
               
           - Invalid Book Code
             * Status Code: 404
             * Error Message:
              
                   {
                       "status": "fail",
                       "data": {
                           "Message": "Invalid Book Code."
                       }
                   }

           - No Fields to Update
             * Status Code: 400
             * Error Message:
              
                   {
                       "status": "fail",
                       "data": {
                           "Message": "No fields to update."
                       }
                   }
               
           - Database Error
             * Status Code: 500
             * Error Message:
              
                   {
                       "status": "fail",
                       "data": {
                           "Message": "Error message from the database."
                       }
                   }

           - Database Error
             * Status Code: 401
             * Error Message:
              
                   {
                       "status": "fail",
                       "data": {
                           "Message": "Failed to decode JWT token."
                       }
                   }
## Endpoint 5: /books/delete

   * Method: DELETE
   * Description: This endpoint allows an administrator to delete a book from the library database using the book's unique code. A valid admin JWT token is required for authorization.
   * Request Parameters:
   
       - Parameter 1: bookCode
           * Type: string
           * Description: The unique code of the book to be deleted.
           * Required: Yes
           * Example:

                 123ABC
        
       - Parameter 4: token
           * Type: string
           * Description: A JWT token required for authentication. Only admins can delete books.
           * Required: Yes
           * Example:

                 eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOi8vbGlicmFyeS5vcmciLCJhdWQiOiJodHRwOi8vbGlicmFyeS5jb20iLCJpYXQiOjE3MzAxNjUwMjMsImV4cCI6MTczMDE2ODYyMywiZGF0YSI6eyJ1c2VyaWQiOiIxIiwibmFtZSI6ImFkbWluIiwiYWNjZXNzX2xldmVsIjoiYWRtaW4ifX0.Yyw03t-aNg_dY8Q0sA0QqFWH5L6DKwqz8_75ln7GlXo
             
   * Response:
       - Success Response:
           * Status Code: 200
           * Response Body:
             
                 {
                     "status": "success",
                     "new_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOi8vbGlicmFyeS5vcmciLCJhdWQiOiJodHRwOi8vbGlicmFyeS5jb20iLCJpYXQiOjE3MzAxNjUwMjMsImV4cCI6MTczMDE2ODYyMywiZGF0YSI6eyJ1c2VyaWQiOiIxIiwibmFtZSI6ImFkbWluIiwiYWNjZXNzX2xldmVsIjoiYWRtaW4ifX0.Yyw03t-aNg_dY8Q0sA0QqFWH5L6DKwqz8_75ln7GlXo"
                 }

           * new_token: string - A new JWT token generated upon successful addition of the book. This new token is valid for 1 hour.
             
       - Error Response:
           - Access Denied (Non-Admin User)
             * Status Code: 403
             * Error Message:
               
                   {
                       "status": "fail",
                       "data": {
                           "Message": "Access Denied. Only admins can add books."
                       }
                   }
               
           - Invalid Token
             * Status Code: 401
             * Error Message:
              
                   {
                       "status": "fail",
                       "data": {
                           "Message": "Token is invalid or outdated."
                       }
                   }
    
           - Invalid Book Code
             * Status Code: 404
             * Error Message:
              
                   {
                       "status": "fail",
                       "data": {
                           "Message": "Invalid Book Code."
                       }
                   }
  
           - Database Error
             * Status Code: 500
             * Error Message:
              
                   {
                       "status": "fail",
                       "data": {
                           "Message": "Error message from the database."
                       }
                   }

           - JWT Decoding Error
             * Status Code: 401
             * Error Message:
              
                   {
                       "status": "fail",
                       "data": {
                           "Message": "Failed to decode JWT token."
                       }
                   }


## Endpoint 6: /books/displayAll

   * Method: GET
   * Description: This endpoint retrieves and displays all books from the library's collection. A valid JWT token is required for authorization.
   * Request Parameters:

       - Parameter: token
           * Type: string
           * Description: A JWT token required for authentication.
           * Required: Yes
           * Example:

                 eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOi8vbGlicmFyeS5vcmciLCJhdWQiOiJodHRwOi8vbGlicmFyeS5jb20iLCJpYXQiOjE3MzAxNjUwMjMsImV4cCI6MTczMDE2ODYyMywiZGF0YSI6eyJ1c2VyaWQiOiIxIiwibmFtZSI6ImFkbWluIiwiYWNjZXNzX2xldmVsIjoiYWRtaW4ifX0.Yyw03t-aNg_dY8Q0sA0QqFWH5L6DKwqz8_75ln7GlXo
             
   * Response:
       - Success Response:
           * Status Code: 200
           * Response Body:
        
              - When Books are found
             
                    {
                         "status": "success",
                         "new_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOi8vbGlicmFyeS5vcmciLCJhdWQiOiJodHRwOi8vbGlicmFyeS5jb20iLCJpYXQiOjE3MzAxNjUwMjMsImV4cCI6MTczMDE2ODYyMywiZGF0YSI6eyJ1c2VyaWQiOiIxIiwibmFtZSI6ImFkbWluIiwiYWNjZXNzX2xldmVsIjoiYWRtaW4ifX0.Yyw03t-aNg_dY8Q0sA0QqFWH5L6DKwqz8_75ln7GlXo",
                         "data": [
                             {
                                 "bookid": 1,
                                 "title": "Romeo and Juliet",
                                 "genre": "Romantic",
                                 "bookCode": "123ABC",
                                 "authorid": 1,
                                 "authorname": "William Shakespear"
                             },
                             {
                                 "bookid": 2,
                                 "title": "The Dawn",
                                 "genre": "Romantic",
                                 "bookCode": "541XYZ",
                                 "authorid": 2,
                                 "authorname": "S. J. Ducusin"
                             }
                         ]
                     }
        
                 * new_token: string - A new JWT token generated upon successful addition of the book. This new token is valid for 1 hour.

               - When Books are not found
                  
                     {
                         "status": "success",
                         "data": "No books found."
                     }
             
       - Error Response:          
           - Invalid Token
             * Status Code: 401
             * Error Message:
              
                   {
                       "status": "fail",
                       "data": {
                           "Message": "Token is invalid or outdated."
                       }
                   }
    
           - Database Error
             * Status Code: 500
             * Error Message:
              
                   {
                       "status": "fail",
                       "data": {
                           "Message": "Error message from the database."
                       }
                   }

           - JWT Decoding Error
             * Status Code: 401
             * Error Message:
              
                   {
                       "status": "fail",
                       "data": {
                           "Message": "Failed to decode JWT token."
                       }
                   }


## Endpoint 7: /books/displayauthorsbooks

   * Method: GET
   * Description: This endpoint retrieves and displays all books written by a specified author from the library's collection. A valid JWT token is required for authorization.
   * Request Parameters:

     - Parameter 1: authorname
           * Type: string
           * Description: The name of the author whose books are to be retrieved.
           * Required: Yes
           * Example:

                 William Shakespeare

       - Parameter 1: token
           * Type: string
           * Description: A JWT token required for authentication.
           * Required: Yes
           * Example:

                 eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOi8vbGlicmFyeS5vcmciLCJhdWQiOiJodHRwOi8vbGlicmFyeS5jb20iLCJpYXQiOjE3MzAxNjUwMjMsImV4cCI6MTczMDE2ODYyMywiZGF0YSI6eyJ1c2VyaWQiOiIxIiwibmFtZSI6ImFkbWluIiwiYWNjZXNzX2xldmVsIjoiYWRtaW4ifX0.Yyw03t-aNg_dY8Q0sA0QqFWH5L6DKwqz8_75ln7GlXo
             
   * Response:
       - Success Response:
           * Status Code: 200
           * Response Body:
        
              - When Books are found
             
                    {
                         "status": "success",
                         "new_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOi8vbGlicmFyeS5vcmciLCJhdWQiOiJodHRwOi8vbGlicmFyeS5jb20iLCJpYXQiOjE3MzAxNjUwMjMsImV4cCI6MTczMDE2ODYyMywiZGF0YSI6eyJ1c2VyaWQiOiIxIiwibmFtZSI6ImFkbWluIiwiYWNjZXNzX2xldmVsIjoiYWRtaW4ifX0.Yyw03t-aNg_dY8Q0sA0QqFWH5L6DKwqz8_75ln7GlXo",
                         "data": [
                             {
                                 "bookid": 1,
                                 "title": "Hamlet",
                                 "genre": "Tragedy",
                                 "bookCode": "001",
                                 "authorid": 1,
                                 "authorname": "William Shakespeare"
                             },
                             {
                                 "bookid": 2,
                                 "title": "Macbeth",
                                 "genre": "Tragedy",
                                 "bookCode": "002",
                                 "authorid": 1,
                                 "authorname": "William Shakespeare"
                             }
                         ]
                     }

        
                 * new_token: string - A new JWT token generated upon successful addition of the book. This new token is valid for 1 hour.

               - When Books are not found
                  
                     {
                         "status": "fail",
                         "data": {
                             "Message": "No such author exists."
                         }
                     }
             
       - Error Response:          
           - Invalid Token
             * Status Code: 401
             * Error Message:
              
                   {
                       "status": "fail",
                       "data": {
                           "Message": "Token is invalid or outdated."
                       }
                   }
    
           - Database Error
             * Status Code: 500
             * Error Message:
              
                   {
                       "status": "fail",
                       "data": {
                           "Message": "Error message from the database."
                       }
                   }

           - JWT Decoding Error
             * Status Code: 401
             * Error Message:
              
                   {
                       "status": "fail",
                       "data": {
                           "Message": "Failed to decode JWT token."
                       }
                   }                
