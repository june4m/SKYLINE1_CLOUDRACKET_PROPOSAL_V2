---
title: "Solution Architecture"
date: "2025-11-09"
weight: 4
chapter: false
pre: " <b> 4. </b> "
---



The platform adopts an AWS Serverless architecture for stable operations, scalability, and cost efficiency.

User, court, and booking data are stored in Amazon DynamoDB. Components communicate via Amazon API Gateway and AWS Lambda functions. The web and mobile interfaces are deployed on AWS Amplify, while Amazon Cognito ensures secure access control.

Amazon Personalize recommends courts based on user history, and Amazon Comprehend performs sentiment analysis on reviews. A Custom Dashboard visualizes operational data for both users and court owners.

All activities are monitored through Amazon CloudWatch and automated with Amazon EventBridge.


![Cloud Racket Platform Architecture](\images\2-Proposal\Skyline1_CloudRacket.jpg)

## AWS Services Used
- **AWS Amplify Hosting**: Web/mobile hosting and deployment.
- **Amazon API Gateway**: Connects client and backend services.
- **AWS Lambda**: Handles business logic and service integration.
- **Amazon DynamoDB**: Stores user, court, and booking data.
- **Amazon Cognito**: Manages authentication and authorization.
- **Amazon SES**: Sends automated booking and notification emails.
- **Amazon S3**: Stores court images and analytical data.
- **Amazon Personalize**: Provides personalized court recommendations.
- **Amazon Comprehend (Optional)**: Sentiment analysis on Vietnamese reviews to enhance overall ratings.
- **Amazon Location Service + DynamoDB GeoLib**: Finds nearby courts based on user location.
- **Custom Dashboard**: Built with AWS Amplify, AWS Lambda, and Chart.js for data visualization using DynamoDB/S3 data.
- **Amplify Admin UI (Admin Portal)**: Manages CRUD operations for courts, moderates reviews, and tracks logs.
- **Amplify CI/CD**: Automates deployment and updates.
- **Amazon CloudWatch**: Monitors logs, performance, and alerts.
- **Amazon EventBridge (Scheduler)**: Automates notifications and data cleanup.
- **AWS IAM + KMS + WAF**: Security management, data encryption, and web attack prevention.

## Component Design
- **User Module**: Amazon Cognito manages registration, login, and profiles; user data (bookings, favorites, history) stored in DynamoDB.
- **Court Module**: Court owners manage court info and images; data stored in DynamoDB and S3; updates via API Gateway + Lambda.
- **Booking Flow**: API Gateway → Lambda → DynamoDB → SES handles booking, checks conflicts, and sends confirmation emails.
- **Recommendation System**: Amazon Personalize analyzes behavior and ratings to suggest courts (70% behavioral + 30% rating-based model).
- **Geo Search**: DynamoDB Geo Library or Amazon Location Service locates nearby courts; integrated with Google Maps for directions.
- **Admin Dashboard**: Visualizes revenue, bookings, and reviews using AWS Amplify + Chart.js, powered by DynamoDB/S3 data through Lambda.
- **Automation Layer**: EventBridge triggers scheduled Lambdas for reminders, retraining models, and data cleanup.