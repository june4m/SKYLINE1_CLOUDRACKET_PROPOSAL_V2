---
title: "Budget Estimation"
date: "2025-11-09"
weight: 7
chapter: false
pre: " <b> 7. </b> "
---

You can find the budget estimation on the [AWS Pricing Calculator](https://calculator.aws/#/estimate?id=621f38b12a1ef026842ba2ddfe46ff936ed4ab01).  
Or you can download the [Budget Estimation File](../attachments/budget_estimation.pdf).

## Infrastructure Costs

### AWS Services:
- **AWS Amplify Hosting**: Free Tier: 500 build mins, 5 GB served. After Free Tier: ~$0.01/min × 500 = $5.00/month
- **AWS Lambda**: $0.00/month (20,000 requests/day, 128 MB, 200 ms average)
- **Amazon API Gateway**: $0.00/month (600,000 requests/month, under Free Tier)
- **Amazon DynamoDB**: $0.00/month (5 GB data, 100K read/write per day)
- **Amazon S3 (Image Storage)**: $0.12/month (10 GB storage, 5,000 GET/PUT requests)
- **Amazon SES (Email)**: $0.00/month (2,000 emails/month within Free Tier)
- **Amazon Personalize**: Free for 2 months (20 GB data, 5 M interactions). After that: ~$8.00/month with batch inference (small dataset + retrain weekly).
- **Custom Dashboard (Amplify + Chart.js)**: $0.00/month (uses existing Amplify, data from S3/DynamoDB)
- **Amazon Location Service**: $0.00/month (10,000 map requests, 1,000 location requests)
- **Amazon EventBridge (Scheduler)**: $0.00/month (10 trigger rules daily/hourly)
- **AWS IAM + KMS + WAF**: $0.00/month (authentication, encryption, and basic security)

### Total Cost Breakdown:
- **Month 1**: $0.12/month (All within Free Tier)
- **Month 2**: $5.12/month (Personalize still in Free Tier, Amplify begins charging)
- **After Free Tier expires**: $13.12/month, ≈ $157.44/year

**Overall**: $0.7/month during development, $8.40/12 months initial cost