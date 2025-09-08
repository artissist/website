---
layout: page
title: About
published: false
---

# About Mosaic

Mosaic is an Artist's Personal Assistant platform - an online-only AWS-first application that provides conversational logging, project planning, asset management, and insights for artists.

## Key Features

### Conversational Logging
The system captures natural conversations about artwork and automatically extracts structured data about projects, materials, time spent, and techniques using AI-powered analysis.

### Project Planning & Management
- Dynamic planning briefs with versioning and changelog
- Milestone tracking with due dates and criteria
- Custom fields with Global Field Library
- Real-time updates via GraphQL subscriptions

### Asset Management
- Organized storage for images, audio, and documents
- EXIF data processing and OCR capabilities
- Linked assets to projects and logs
- S3-based storage with intelligent archiving

### AI-Powered Insights
- Amazon Bedrock integration for content extraction
- Amazon Nova Sonic for speech-to-text conversion
- Confidence-based attribution with user validation
- Analytics pipeline for creative insights

## Architecture

Mosaic is built on AWS with a modern, scalable architecture:

- **Frontend**: Next.js with TypeScript
- **API**: AWS AppSync (GraphQL) 
- **Database**: Amazon DynamoDB with single-table design
- **Storage**: Amazon S3 with intelligent tiering
- **AI/ML**: Amazon Bedrock and Nova Sonic
- **Analytics**: AWS Glue + Athena

## Development

The project is organized into milestone-based development phases, with detailed tracking in our [project documentation](https://github.com/artissist/mosaic).