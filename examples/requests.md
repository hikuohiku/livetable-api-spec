# API Request Examples

This document provides practical examples of API requests for the LiveTable API.

## Authentication

All requests require a JWT Bearer token obtained from NextAuth:

```bash
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```

## User Management

### Get User by Email

```bash
curl -X GET "http://localhost:3001/api/users/email/user@example.com" \
  -H "Authorization: Bearer YOUR_JWT_TOKEN" \
  -H "Content-Type: application/json"
```

### Get User with Complete Data

```bash
curl -X GET "http://localhost:3001/api/users/email/user@example.com/with-data" \
  -H "Authorization: Bearer YOUR_JWT_TOKEN" \
  -H "Content-Type: application/json"
```

### Get Google User Profile

```bash
curl -X GET "http://localhost:3001/api/users/123e4567-e89b-12d3-a456-426614174000/google" \
  -H "Authorization: Bearer YOUR_JWT_TOKEN" \
  -H "Content-Type: application/json"
```

## Channel Management

### Get Channel by ID

```bash
curl -X GET "http://localhost:3001/api/channels/UC_vMYWcDjmfdpH6r4TTn1MQ" \
  -H "Authorization: Bearer YOUR_JWT_TOKEN" \
  -H "Content-Type: application/json"
```

### Get Multiple Channels

```bash
curl -X POST "http://localhost:3001/api/channels/find-many" \
  -H "Authorization: Bearer YOUR_JWT_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "channelIds": ["UC_vMYWcDjmfdpH6r4TTn1MQ", "UC0TXe_LYZ4scaW2XMyi5_kw"]
  }'
```

## Video Management

### Get Videos by Channel

```bash
curl -X GET "http://localhost:3001/api/videos/channel/UC_vMYWcDjmfdpH6r4TTn1MQ" \
  -H "Authorization: Bearer YOUR_JWT_TOKEN" \
  -H "Content-Type: application/json"
```

### Get Live and Upcoming Videos

```bash
curl -X POST "http://localhost:3001/api/videos/live-and-upcoming" \
  -H "Authorization: Bearer YOUR_JWT_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "channelIds": ["UC_vMYWcDjmfdpH6r4TTn1MQ", "UC0TXe_LYZ4scaW2XMyi5_kw"]
  }'
```

### Get Video by ID

```bash
curl -X GET "http://localhost:3001/api/videos/7K5lUvMrjik" \
  -H "Authorization: Bearer YOUR_JWT_TOKEN" \
  -H "Content-Type: application/json"
```

## JavaScript/TypeScript Examples

### Using Fetch API

```typescript
const apiClient = {
  baseURL: "http://localhost:3001/api",

  async request<T>(endpoint: string, options: RequestInit = {}): Promise<T> {
    const token = await getSession()?.accessToken;

    const response = await fetch(`${this.baseURL}${endpoint}`, {
      ...options,
      headers: {
        "Content-Type": "application/json",
        Authorization: `Bearer ${token}`,
        ...options.headers,
      },
    });

    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }

    return response.json();
  },

  async getUserWithData(email: string) {
    return this.request(`/users/email/${email}/with-data`);
  },

  async getChannels(channelIds: string[]) {
    return this.request("/channels/find-many", {
      method: "POST",
      body: JSON.stringify({ channelIds }),
    });
  },
};
```

### Error Handling

```typescript
try {
  const userData = await apiClient.getUserWithData("user@example.com");
  console.log("User data:", userData.data);
} catch (error) {
  if (error.status === 401) {
    // Handle authentication error
    console.error("Authentication failed");
  } else if (error.status === 404) {
    // Handle not found
    console.error("User not found");
  } else {
    // Handle other errors
    console.error("API request failed:", error.message);
  }
}
```
