# LiveTable API Specification

This repository contains the OpenAPI 3.0 specification for the LiveTable API server.

## Overview

LiveTable is a YouTube live stream timetable application with a polyrepo architecture:

- **Frontend**: Next.js application (separate repository)
- **Backend**: API server (separate repository)
- **API Spec**: This repository - shared specification

## API Specification

The API specification is defined in OpenAPI 3.0 format and describes all endpoints, request/response schemas, and authentication requirements for the LiveTable API server.

### Key Features

- JWT Bearer token authentication via NextAuth
- User management with Google OAuth integration
- YouTube channel subscription management
- Live stream and video data endpoints
- Comprehensive error handling

### Endpoints Overview

- **User Management**: User lookup, Google OAuth data, subscriptions
- **Channel Management**: Channel information and bulk operations
- **Video Management**: Live streams, upcoming videos, video details

## Files

- `openapi.yaml` - Complete OpenAPI 3.0 specification
- `schemas/` - Individual schema definitions (if needed for modular approach)
- `examples/` - Request/response examples
- `docs/` - Generated documentation

## Usage

### For Frontend Developers

Use this specification to understand expected API contracts and implement API client services.

### For Backend Developers

Implement the API server according to this specification to ensure compatibility with the frontend.

### Generating Documentation

```bash
# Using Swagger UI
npx swagger-ui-serve openapi.yaml

# Using Redoc
npx redoc-cli build openapi.yaml --output docs/index.html
```

### Validation

```bash
# Validate the OpenAPI spec
npx swagger-parser validate openapi.yaml
```

## Development Workflow

1. **Specification Changes**: Update `openapi.yaml` first
2. **Review Process**: All changes require review from both frontend and backend teams
3. **Implementation**: Backend and frontend implement changes based on updated spec
4. **Testing**: Ensure implementations match the specification

## Versioning

This project follows semantic versioning:

- **Major**: Breaking changes to existing endpoints
- **Minor**: New endpoints or backward-compatible changes
- **Patch**: Documentation fixes, clarifications

## Integration

### With Frontend (Next.js)

Frontend TypeScript types and API client can be generated from this specification.

### With Backend

Backend validation and route generation can use this specification.

## Contributing

1. Create a feature branch
2. Update the OpenAPI specification
3. Add examples if introducing new endpoints
4. Update this README if needed
5. Create pull request with changes reviewed by both teams
