---
layout: page
title: "Architecture Overview"
published: false
---

# Architecture Overview

Mosaic follows a modern AWS-first architecture designed for scalability, reliability, and cost-effectiveness.

## High-Level Architecture

```
Frontend (Next.js) 
    ↓
AWS AppSync (GraphQL API)
    ↓
AWS Lambda (Business Logic)
    ↓
Amazon DynamoDB (Primary Database)
Amazon S3 (Asset Storage)
Amazon Bedrock (AI Processing)
```

## Core Components

### Frontend Layer
- **Next.js** with App Router and TypeScript
- **shadcn/ui** + Tailwind CSS for design system
- **React Query** for REST API state management
- **Apollo Client** for GraphQL operations

### API Layer
- **AWS AppSync** provides GraphQL API with real-time subscriptions
- **VTL/JS Resolvers** handle business logic
- **Amazon EventBridge** for event-driven architecture

### Data Layer
- **Amazon DynamoDB** with single-table design for performance
- **Amazon OpenSearch** Serverless for search capabilities
- **Amazon S3** with intelligent tiering for asset storage

### AI/ML Services
- **Amazon Bedrock** for content extraction and analysis
- **Amazon Nova Sonic** for speech-to-text conversion
- **Custom embedding models** for semantic search

### Analytics Pipeline
- **AWS Step Functions** orchestrate data processing
- **AWS Glue** for ETL operations
- **Amazon Athena** for analytics queries

## Data Model

The system uses a single-table DynamoDB design with hierarchical sort keys:

```
PK: TENANT#<ownerId|orgId>
SK: PROJECT#<projectId>
SK: PROJECT#<projectId>#LOG#<logId>  
SK: PROJECT#<projectId>#ASSET#<assetId>
SK: INSPIRATION#<inspId>
```

This design enables efficient queries while maintaining ACID properties across related entities.

## Security Model

- **AWS IAM** with least-privilege access
- **Amazon Cognito** for user authentication
- **Row-level security** scoped by ownerId/orgId
- **KMS encryption** for all data stores
- **Signed URLs** for secure S3 access