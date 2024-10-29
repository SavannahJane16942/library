# Libray API

## Introduction

  * Overview: A brief description of your API and its purpose.
  * Authentication: Explain the authentication methods used (e.g., API keys, OAuth, basic auth).
  * Error Handling: Describe the error codes and response formats for different error scenarios.
      
## Endpoints

## Endpoint 1: /user/register

   * Method: POST
   * Description: Registers a new user in the system by saving their email, username, and password in the database.
   * Request Parameters:
   
       - Parameter 1: email
           * Type: string
           * Description: The email address of the user
           * Required: Yes
           * Example: savannahjaneducusin@gmail.com
             
       - Parameter 2: username
           * Type: string
           * Description: The desired username of the user
           * Required: Yes
           * Example: Saviee

       - Parameter 3: password
           * Type: string
           * Description: The password chosen by the user, which will be securely hashed before
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
