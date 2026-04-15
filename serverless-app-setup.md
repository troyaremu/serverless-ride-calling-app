# Serverless Ride-Calling App — World Rydes — Configuration Steps

## Overview
A fully serverless web application built on AWS, allowing users to request rides
through a browser-based interface. No traditional servers used — all compute
runs on-demand via AWS Lambda.

---

## Step 1 — AWS Amplify (Frontend Hosting)
- Created Amplify app and connected to source code
- Configured build settings for static frontend deployment
- Deployed frontend HTML/CSS/JavaScript to Amplify hosting
- Obtained public URL for the application

## Step 2 — Amazon Cognito (User Authentication)
- Created Cognito User Pool for user registration and login
- Configured password policies and account verification via email
- Set up App Client within the User Pool for frontend integration
- Integrated Cognito hosted UI into the frontend for sign-in flow
- Tested user registration, login, and token generation

## Step 3 — AWS Lambda (Backend Logic)
- Created Lambda function to handle ride request logic
- Wrote function to receive ride request, select a unicorn, and return response
- Configured Lambda execution role with appropriate IAM permissions
- Set environment variables for configuration
- Tested Lambda function independently via the AWS console test feature

## Step 4 — AWS API Gateway (API Layer)
- Created REST API in API Gateway
- Configured POST method on /ride endpoint
- Integrated API method with Lambda function
- Enabled Cognito User Pool Authorizer on the API to secure the endpoint
- Deployed API to a named stage (prod)
- Retrieved the API invoke URL for frontend integration

## Step 5 — Frontend Integration
- Updated frontend JavaScript with the API Gateway invoke URL
- Updated frontend with Cognito User Pool configuration
- Tested full end-to-end flow: login → request ride → receive response
- Confirmed authentication token passed correctly to API Gateway
- Confirmed Lambda processed request and returned correct response

---

## Architecture Flow

```
User → Amplify (Frontend) → Cognito (Auth) → API Gateway → Lambda → Response
```

1. User visits the Amplify-hosted site and logs in via Cognito
2. After login, user submits a ride request from the map interface
3. Frontend sends authenticated POST request to API Gateway
4. API Gateway validates the Cognito token (rejects unauthenticated requests)
5. API Gateway triggers the Lambda function with the request payload
6. Lambda selects a unicorn and returns ride confirmation
7. Frontend displays the ride confirmation to the user

---

## Key Technical Decisions

| Decision | Reason |
|---|---|
| Serverless over EC2 | No server management, automatic scaling, zero idle cost |
| Cognito for auth | Managed auth service — secure, scalable, no custom auth code |
| API Gateway authorizer | Protects Lambda from unauthenticated requests |
| Amplify for hosting | Continuous deployment, CDN-backed, no server required |

---

## Skills Demonstrated
AWS Lambda | API Gateway | AWS Amplify | Amazon Cognito | Serverless Architecture |
REST APIs | IAM | Event-driven Computing | Cloud-Native Design
