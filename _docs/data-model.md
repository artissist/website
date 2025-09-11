---
layout: page
title: "Data Model"
published: true
---

# Data Model

Artissist uses a single-table DynamoDB design optimized for access patterns and cost efficiency.

## Table Structure

**Table Name**: `Artissist`
**Partition Key**: `TENANT#<ownerId|orgId>`
**Sort Key**: Hierarchical patterns for different entity types

## Entity Patterns

### Projects
```
PK: TENANT#usr_123
SK: PROJECT#proj_abc
```

Attributes:
- `projectId`: Unique identifier
- `title`: Project name
- `medium`: Art medium (oil, digital, etc.)
- `status`: planning|production|complete
- `client`: Optional client information
- `deadline`: Target completion date
- `budget`: Financial constraints
- `customFields`: Flexible metadata object

### Project Planning Briefs
```
PK: TENANT#usr_123  
SK: PROJECT#proj_abc#BRIEF#v2
```

Attributes:
- `requirements[]`: List of project requirements
- `deliverables[]`: Expected outputs
- `approvals[]`: Approval workflow states
- `version`: Version number
- `changelog[]`: Version history

### Milestones
```
PK: TENANT#usr_123
SK: PROJECT#proj_abc#MILESTONE#ms_1
```

Attributes:
- `name`: Milestone description
- `due`: Due date
- `criteria`: Success criteria
- `status`: pending|in_progress|complete

### Logs
```
PK: TENANT#usr_123
SK: PROJECT#proj_abc#LOG#log_xyz
```

Attributes:
- `rawText`: Original transcription
- `transcriptMeta`: Audio metadata
- `extracted`: Structured AI extraction results
- `confidence`: AI confidence scores
- `attributionStatus`: confirmed|pending|rejected
- `mediaRefs[]`: Linked media files
- `materials[]`: Extracted material usage
- `timeSpentMinutes`: Extracted time information
- `tags[]`: Classification tags

### Assets
```
PK: TENANT#usr_123
SK: PROJECT#proj_abc#ASSET#asset_123
```

Attributes:
- `type`: image|audio|document
- `s3Key`: S3 object location
- `exif`: Image metadata
- `ocr`: Extracted text content
- `alt`: Accessibility description
- `linkedProjectId`: Associated project
- `linkedLogId`: Associated log entry

### Inspiration
```
PK: TENANT#usr_123
SK: INSPIRATION#insp_456
```

Attributes:
- `type`: text|image|audio|file
- `s3Key`: S3 object location (if applicable)
- `tags[]`: Classification tags
- `linkedProjectId`: Optional project association

## Access Patterns

### Primary Access Patterns
1. **Get all projects for user**: Query PK=TENANT#usr_123, SK begins_with PROJECT#
2. **Get project details**: Get item PK=TENANT#usr_123, SK=PROJECT#proj_abc
3. **Get project logs**: Query PK=TENANT#usr_123, SK begins_with PROJECT#proj_abc#LOG#
4. **Get project assets**: Query PK=TENANT#usr_123, SK begins_with PROJECT#proj_abc#ASSET#

### Secondary Patterns with GSI
- **Search by status**: GSI on status attribute
- **Time-based queries**: GSI on creation timestamp
- **Material usage**: GSI on extracted materials

## Indexes

### GSI1: Status Index
- **PK**: `status`
- **SK**: `createdAt`
- Use case: Find all projects by status across users

### GSI2: Search Index  
- **PK**: `entityType` 
- **SK**: `searchableText`
- Use case: Full-text search capabilities

## Data Consistency

- **Strong consistency** for user-scoped queries
- **Eventually consistent** for cross-user analytics
- **Atomic transactions** for related entity updates
- **Optimistic locking** via version attributes

## Transactions and Concurrency
- DynamoDB transactions ensure related entities update atomically
- Version attributes provide optimistic locking for conflicting writes

## TTL and Archival
- Items support `expiresAt` timestamps for automatic expiration
- Archived records are moved to cold storage for long-term reference

## Example Query
```graphql
query GetProjectLogs($projectId: ID!) {
  logs(projectId: $projectId) {
    logId
    materials
    timeSpentMinutes
  }
}
```
