# Libray API

## Introduction

  * Overview: An API Library used by library admins to add, modify books and monitor users.
  * Authentication: Explain the authentication methods used (e.g., API keys, OAuth, basic auth).
  * Error Handling: Describe the error codes and response formats for different error scenarios.
      
# Endpoints

## Endpoint 1:     /user/register

   * Method: POST
   * Description: Registers a new user in the system by saving their email, username, and password in the database.
   * Request Parameters:
   
       - Parameter 1: email
           * Type: string
           * Description: The email address of the user.
           * Required: Yes
           * Example: savannahjaneducusin@gmail.com
             
       - Parameter 2: username
           * Type: string
           * Description: The desired username of the user.
           * Required: Yes
           * Example: Saviee

       - Parameter 3: password
           * Type: string
           * Description: The password chosen by the user, which will be securely hashed before.
           * Required: Yes
           * Example: p@$$w0rd!
             
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
## Endpoint 1:     /user/login

   * Method: POST
   * Description: Authenticates a user by verifying their email and password. If successful, generates a JSON Web Token (JWT) for the user.
   * Request Parameters:
   
       - Parameter 1: email
           * Type: string
           * Description: The email address of the user.
           * Required: Yes
           * Example: savannahjaneducusin@gmail.com

       - Parameter 2: password
           * Type: string
           * Description: The password for the user’s account.
           * Required: Yes
           * Example: p@$$w0rd!
             
   * Response:
       - Success Response:
           * Status Code: 200
           * Response Body:
             
                 {
                     "status": "success",
                     "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
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
               
