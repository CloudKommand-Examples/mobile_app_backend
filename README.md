# CloudKommand Mobile App Backend Example
Mobile App Backend Example (w/ Postman collection for demonstrating API calls)

This repository was created to demostrate how to build a common use case of a mobile backend using CloudKommand.

Use this as a starting point for your own application development!

## High Level 
This is a backend for a Dog App, an app where you can browse and save dog pictures.

The backend created allows you to browse dog pictures and to save or list saved dogs if you have an account.
## Detailed Breakdown
The following repo, when deployed as an app within CloudKommand creates a full backend made up of the following fully-managed pieces:
- An api that has some authenticated and some unauthenticated endpoints including
    - Unauthenticated calls
        - Get more dogs
        - Create a new account
        - Exchange username and password for access token, refresh token, and account id 
    - Authenticated calls
        - Save dog picture
        - List saved dog pictures
        - Refresh access token
    - ALSO PROVIDED *
        - A Postman Collection that requires the api id of the deployed mobile dog app backend. 
        - Once the api id is provided, the entire collection can be run and will demonstrate every call in the api
- A Cognito User Pool and App Client
- A DynamoDB Table that tracks users and saved dogs
- A S3 Bucket that stores the pictures of the dogs the user has saved
- Multiple Lambda Functions to handle different use cases, with a Lambda Layer to store shared code
- A policy that locks down the Lambda Function access to the above-mentioned table, bucket, and user pool.

## How to try it out:
- Deploy this repo as an app within CloudKommand (using this repo's base url)
- Open the Postman collection at the base level of this repo in Postman
- In the Postman collection variables section (not the individual call level), paste the API ID from the "api" component in the api_id variable
- Also in the Postman collection, hit run and select that you want to run all of the calls
- You should see all of the calls run sequentially! It will run unauthenticated calls first, then authenticate and run authenticated calls next!
- In CloudKommand, in the Workspace section, once you've deployed the backend, you will see links to the various actual infrastructure components. You can explore them to see the user, records, file, and logs created by the run of the various calls!
- NOTE: If you run the collection multiple times, you'll want to delete the user or remove the create_account_and_user call and reorder the grant_access_to_existing_user call to be before the authenticated calls. Otherwise, it will try to recreate the same user and fail. 


## The Plug-Ins Used
Using the kommand.json at the base level of the repo, combined with the folder structure, use this example to develop your own application, and check out the CloudKommand-managed plug-ins used in this example at:

- IAM (role and policy): https://github.com/cloudkommand/iam 
- Lambda (function and layer): https://github.com/cloudkommand/lambda
- S3: https://github.com/cloudkommand/s3
- API Gateway: https://github.com/cloudkommand/apigateway
- DynamoDB: https://github.com/cloudkommand/dynamodb
- Cognito (user pool and app client): https://github.com/cloudkommand/cognito