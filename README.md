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

   * Method: **POST**
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

   * Method: **POST**
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

   * Method: **POST**
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
           * Required: No (at least one field should be provided for an update).
           * Example:

                 William Shakepears

       - Parameter 3: title
           * Type: string
           * Description: New title of the book.
           * Required: No (at least one field should be provided for an update).
           * Example:

                 Romeo & Juliet

       - Parameter 4: genre
           * Type: string
           * Description: New genre of the book
           * Required: No (at least one field should be provided for an update).
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

           * new_token: string - A new JWT token generated upon successful update of the book. This new token is valid for 1 hour.
             
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

           - JWT Decoding Error
             * Status Code: 401
             * Error Message:
              
                   {
                       "status": "fail",
                       "data": {
                           "Message": "Failed to decode JWT token."
                       }
                   }

               
## Endpoint 5: /books/delete

   * Method: **DELETE**
   * Description: This endpoint allows an administrator to delete a book from the library database using the book's unique code. A valid admin JWT token is required for authorization.
   * Request Parameters:
   
       - Parameter 1: bookCode
           * Type: string
           * Description: The unique code of the book to be deleted.
           * Required: Yes
           * Example:

                 123ABC
        
       - Parameter 2: token
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

           * new_token: string - A new JWT token generated upon successful deletion of the book. This new token is valid for 1 hour.
             
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

   * Method: **GET**
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
        
                 * new_token: string - A new JWT token generated upon successful process. This new token is valid for 1 hour.

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

   * Method: **GET**
   * Description: This endpoint retrieves and displays all books written by a specified author from the library's collection. A valid JWT token is required for authorization.
   * Request Parameters:

     - Parameter 1: authorname
           * Type: string
           * Description: The name of the author whose books are to be retrieved.
           * Required: Yes
           * Example:

                 William Shakespeare

     - Parameter 2: token
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

        
                 * new_token: string - A new JWT token generated upon successful process. This new token is valid for 1 hour.

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


## Endpoint 8: /books/displaytitlebooks

   * Method: **GET**
   * Description: This endpoint retrieves and displays all books from the library's collection that match a specified title. A valid JWT token is required for authorization.
   * Request Parameters:

     - Parameter 1: booktitle
           * Type: string
           * Description: The title of the book to be retrieved.
           * Required: Yes
           * Example:

                 Hamlet

     - Parameter 2: token
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
                                 "title": "Hamlet",
                                 "genre": "Tragedy",
                                 "bookCode": "002",
                                 "authorid": 1,
                                 "authorname": "S. J. Dy"
                             }
                         ]
                     }

        
                 * new_token: string - A new JWT token generated upon successful process. This new token is valid for 1 hour.

               - When Books are not found
                  
                     {
                         "status": "fail",
                         "data": {
                             "Message": "No such book title exists."
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


## Endpoint 9: /books/displaygenrebooks

   * Method: **GET**
   * Description: Retrieves and displays all books in the collection that match a specified genre. A valid JWT token is required for authorization.
   * Request Parameters:

     - Parameter 1: bookgenre
           * Type: string
           * Description: The genre of books to retrieve.
           * Required: Yes
           * Example:

                 Tragedy

     - Parameter 2: token
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
                                 "title": "Hamlet",
                                 "genre": "Tragedy",
                                 "bookCode": "002",
                                 "authorid": 1,
                                 "authorname": "S. J. Dy"
                             }
                         ]
                     }

        
                 * new_token: string - A new JWT token generated upon successful process. This new token is valid for 1 hour.

               - When Books are not found
                  
                     {
                         "status": "fail",
                         "data": {
                             "Message": "No such book genre exists."
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


## Endpoint 10: /authors/add

   * Method: **POST**
   * Description: Retrieves and displays all books in the collection that match a specified genre. A valid JWT token is required for authorization.
   * Request Parameters:

     - Parameter 1: authorname
           * Type: string
           * Description: The name of the author to add to the library.
           * Required: Yes
           * Example:

                 Mark Twain

     - Parameter 2: token
           * Type: string
           * Description: A JWT token required for authentication.
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

        
                 * new_token: string - A new JWT token generated upon successful addition of the author. This new token is valid for 1 hour.
             
       - Error Response:
           - Access Denied (Non-Admin User)
             * Status Code: 403
             * Error Message:
               
                   {
                       "status": "fail",
                       "data": {
                           "Message": "Access Denied. Only admins can add authors."
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
    
           - Author Already Exists
             * Status Code: 409
             * Error Message:
              
                   {
                       "status": "fail",
                       "data": {
                           "Message": "Author already exists."
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


## Endpoint 11: /authors/update

   * Method: **POST**
   * Description: This endpoint allows an admin user to update an author's details in the library database. It requires a valid JWT token with admin access to authorize the update.
   * Request Parameters:

       - Parameter 1: authorid
           * Type: integer
           * Description: The unique ID of the author to update.
           * Required: Yes
           * Example: 

                 123
   
       - Parameter 2: authorname
           * Type: string
           * Description: The new name of the author.
           * Required: No (at least one field should be provided for an update).
           * Example:

                 William Shakepears
        
       - Parameter 3: token
           * Type: string
           * Description: A JWT token required for authentication. Only admins can update authors.
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

           * new_token: string - A new JWT token generated upon successful update of the author. This new token is valid for 1 hour.
             
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
               
           - Invalid Author ID
             * Status Code: 404
             * Error Message:
              
                   {
                       "status": "fail",
                       "data": {
                           "Message": "Invalid Author ID."
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

## Endpoint 12: /authors/delete

   * Method: **DELETE**
   * Description: This endpoint allows an admin user to delete an author from the library database. It requires a valid JWT token with admin access to authorize the deletion.
   * Request Parameters:
   
       - Parameter 1: authorid
           * Type: integer
           * Description: The unique ID of the author to update.
           * Required: Yes
           * Example: 

                 123
        
       - Parameter 2: token
           * Type: string
           * Description: A JWT token required for authentication. Only admins can delete authors.
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

           * new_token: string - A new JWT token generated upon successful deletion of the author. This new token is valid for 1 hour.
             
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
    
           - Invalid Author ID
             * Status Code: 404
             * Error Message:
              
                   {
                       "status": "fail",
                       "data": {
                           "Message": "Invalid Author ID."
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


 ## Endpoint 13: /authors/display

   * Method: **GET**
   * Description: This endpoint displays all authors from the library database. Only authenticated users can access it with a valid JWT token.
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
     
                 {
                      "status": "success",
                      "new_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOi8vbGlicmFyeS5vcmciLCJhdWQiOiJodHRwOi8vbGlicmFyeS5jb20iLCJpYXQiOjE3MzAxNjUwMjMsImV4cCI6MTczMDE2ODYyMywiZGF0YSI6eyJ1c2VyaWQiOiIxIiwibmFtZSI6ImFkbWluIiwiYWNjZXNzX2xldmVsIjoiYWRtaW4ifX0.Yyw03t-aNg_dY8Q0sA0QqFWH5L6DKwqz8_75ln7GlXo",
                      "data": [
                          {
                              "authorid": 1,
                              "name": "William Shakespear"
                      ]
                  }
        
                 * new_token: string - A new JWT token generated upon successful process. This new token is valid for 1 hour.
             
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
    
           - No Authors Found
             * Status Code: 404
             * Error Message:
              
                   {
                       "status": "fail",
                       "Message": "No authors found."
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


## Endpoint 14: /users/delete

   * Method: **DELETE**
   * Description: This endpoint allows an admin to delete a user account by specifying the userid. Only users with admin access level are permitted to perform this action. Admin accounts cannot be deleted.
   * Request Parameters:
   
       - Parameter 1: userid
           * Type: integer
           * Description: The ID of the user to be deleted.
           * Required: Yes
           * Example: 

                 5
        
       - Parameter 2: token
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

           * new_token: string - A new JWT token generated upon successful deletion of a user. This new token is valid for 1 hour.
             
       - Error Response:
           - Access Denied (Non-Admin User)
             * Status Code: 403
             * Error Message:
               
                   {
                       "status": "fail",
                       "data": {
                           "Message": "Access Denied. Only admins can delete accounts."
                       }
                   }
    
           - Admin Account Deletion Attempt
             * Status Code: 403
             * Error Message:
              
                   {
                       "status": "fail",
                       "data": {
                           "Message": "Admin accounts cannot be deleted."
                       }
                   }
               
           - Invalid User ID
             * Status Code: 404
             * Error Message:
              
                   {
                       "status": "fail",
                       "data": {
                           "Message": "Invalid User ID."
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


## Endpoint 15: /users/displayAll

   * Method: **GET**
   * Description: This endpoint allows an admin to retrieve a list of all user accounts. Only users with admin access level are permitted to access this information.
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
        
              - When user accounts are successfully retrieved
             
                    {
                        "status": "success",
                        "new_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOi8vbGlicmFyeS5vcmciLCJhdWQiOiJodHRwOi8vbGlicmFyeS5jb20iLCJpYXQiOjE3MzAxNjUwMjMsImV4cCI6MTczMDE2ODYyMywiZGF0YSI6eyJ1c2VyaWQiOiIxIiwibmFtZSI6ImFkbWluIiwiYWNjZXNzX2xldmVsIjoiYWRtaW4ifX0.Yyw03t-aNg_dY8Q0sA0QqFWH5L6DKwqz8_75ln7GlXo",
                        "data": [
                            {
                                "username": "Sav Ducusin",
                                "email": "sav@example.com",
                                "created_at": "2023-01-01 12:34:56"
                            },
                            {
                                "username": "Rome Celeb",
                                "email": "rome@example.com",
                                "created_at": "2023-01-01 12:34:56"
                            },
                            {
                                "username": "Clint Agumo",
                                "email": "clint@example.com",
                                "created_at": "2023-01-01 12:34:56"
                            }
                        ]
                    }

        
                 * new_token: string - A new JWT token generated upon successful process. This new token is valid for 1 hour.

               - When there are no user accounts to display
                  
                     {
                          "status": "success",
                          "new_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOi8vbGlicmFyeS5vcmciLCJhdWQiOiJodHRwOi8vbGlicmFyeS5jb20iLCJpYXQiOjE3MzAxNjUwMjMsImV4cCI6MTczMDE2ODYyMywiZGF0YSI6eyJ1c2VyaWQiOiIxIiwibmFtZSI6ImFkbWluIiwiYWNjZXNzX2xldmVsIjoiYWRtaW4ifX0.Yyw03t-aNg_dY8Q0sA0QqFWH5L6DKwqz8_75ln7GlXo",
                          "Message": "No user account found."
                      }
             
       - Error Response:
           - Invalid Token
             * Status Code: 403
             * Error Message:
              
                   {
                       "status": "fail",
                       "data": {
                           "Message": "Access Denied. Only admins can view all the users information."
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


## Endpoint 16: /users/profileupdate

   * Method: **POST**
   * Description: This endpoint allows a user (excluding admin accounts) to update their profile information, including their username and password. An old password is required to verify the update request. If no new data is provided, the request will return an error. A new JWT token is issued upon successful update.
   * Request Parameters:

       - Parameter 1: newusername
           * Type: string
           * Description: The new username for the user’s account. If omitted, the username will remain unchanged.
           * Required: No (at least one field should be provided for an update).
           * Example: 

                 Savi D
   
       - Parameter 2: newpassword
           * Type: string
           * Description: The new password for the user’s account. If omitted, the password will remain unchanged.
           * Required: No (at least one field should be provided for an update).
           * Example:

                 PaSsWoRd!?

       - Parameter 3: oldpassword
           * Type: string
           * Description: The current password of the user’s account, used for verification.
           * Required: Yes
           * Example:

                 p@$$w0rd!
        
       - Parameter 4: token
           * Type: string
           * Description: A JWT token required for authentication.
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

           * new_token: string - A new JWT token generated upon successful update of users profile. This new token is valid for 1 hour.
             
       - Error Response:
           - Access Denied (Non-Admin User)
             * Status Code: 403
             * Error Message:
               
                   {
                       "status": "fail",
                       "data": {
                           "Message": "Admin profile cannot be updated."
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
               
           - Incorrect Old Password
             * Status Code: 403
             * Error Message:
              
                   {
                       "status": "fail",
                       "data": {
                           "Message": "Old password is incorrect."
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

           - JWT Decoding Error
             * Status Code: 401
             * Error Message:
              
                   {
                       "status": "fail",
                       "data": {
                           "Message": "Failed to decode JWT token."
                       }
                   }



##
         <center>Savannah Jane Ducusin made with Love.<center>
##
