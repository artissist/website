---
layout: page
title: Documentation
published: false
---

# Documentation

Welcome to the Mosaic documentation. Here you'll find guides and references for using the platform.

## Architecture Documentation

{% for doc in site.docs %}
- [{{ doc.title }}]({{ doc.url | relative_url }})
{% endfor %}

## Quick Links

- [Project Overview](#project-overview)
- [Getting Started](#getting-started)
- [API Reference](#api-reference)

## Project Overview

Mosaic is designed around core entities and workflows:

- **Projects**: Central organizing units for artistic endeavors
- **Logs**: Conversational entries that capture the creative process
- **Assets**: Media files linked to projects and logs
- **Inspiration**: Ideas and references for future work

## Getting Started

1. **Authentication**: Sign in via Amazon Cognito
2. **Create a Project**: Set up your first artistic project
3. **Start Logging**: Begin capturing your creative process
4. **Organize Assets**: Upload and link your creative materials

## API Reference

The platform uses GraphQL via AWS AppSync for all data operations. Key query and mutation patterns are documented in our API guides.