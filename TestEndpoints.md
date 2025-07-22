Based on the codebase context from server/src/index.ts,
Postman testing examples:

API Routes for Testing

1. User Routes (/api/users)
   Example 1: Register User

POST http://localhost:3000/api/users/register
Content-Type: application/json

{
"firstName": "John",
"lastName": "Doe",
"email": "john.doe@example.com",
"password": "password123"
}

Copy

Apply

Example 2: Login User

POST http://localhost:3000/api/users/login
Content-Type: application/json

{
"email": "john.doe@example.com",
"password": "password123"
}

Copy

Apply

2. Organization Routes (/api/organizations) - Requires Authentication
   Example 1: Get Organizations

GET http://localhost:3000/api/organizations
Authorization: Bearer YOUR_JWT_TOKEN

Copy

Apply

Example 2: Create Organization

POST http://localhost:3000/api/organizations
Authorization: Bearer YOUR_JWT_TOKEN
Content-Type: application/json

{
"name": "Tech Corp",
"description": "A technology company"
}

Copy

Apply

3. Project Routes (/api/projects) - Requires Authentication
   Example 1: Get All Projects

GET http://localhost:3000/api/projects
Authorization: Bearer YOUR_JWT_TOKEN

Copy

Apply

Example 2: Create Project

POST http://localhost:3000/api/projects
Authorization: Bearer YOUR_JWT_TOKEN
Content-Type: application/json

{
"name": "E-commerce Platform",
"description": "Online shopping platform",
"category": "Web Development"
}

Copy

Apply

4. Organization-specific Project Routes (/api/org/:orgId/projects) - Requires Authentication
   Example 1: Get Projects by Organization

GET http://localhost:3000/api/org/64a1b2c3d4e5f6789012345/projects
Authorization: Bearer YOUR_JWT_TOKEN

Copy

Apply

Example 2: Create Project in Organization

POST http://localhost:3000/api/org/64a1b2c3d4e5f6789012345/projects
Authorization: Bearer YOUR_JWT_TOKEN
Content-Type: application/json

{
"name": "Mobile App",
"description": "Cross-platform mobile application",
"category": "Mobile Development"
}

Copy

Apply

5. Issue Routes (/api/issues) - Requires Authentication
   Example 1: Get All Issues

GET http://localhost:3000/api/issues?orgId=64a1b2c3d4e5f6789012345&userId=64a1b2c3d4e5f6789012346
Authorization: Bearer YOUR_JWT_TOKEN

Copy

Apply

Example 2: Create Issue

POST http://localhost:3000/api/issues
Authorization: Bearer YOUR_JWT_TOKEN
Content-Type: application/json

{
"title": "Fix login bug",
"description": "Users cannot login with valid credentials",
"type": "bug",
"status": "to do",
"priority": "high",
"projectId": "64a1b2c3d4e5f6789012347",
"assignee": "64a1b2c3d4e5f6789012346",
"reporter": "64a1b2c3d4e5f6789012345",
"dueDate": "2024-02-15T00:00:00.000Z"
}

Copy

Apply

6. Additional User Routes (Based on client-side API calls)
   Example 1: Update User Role

PATCH http://localhost:3000/api/users/64a1b2c3d4e5f6789012346/role
Authorization: Bearer YOUR_JWT_TOKEN
Content-Type: application/json

{
"role": "project manager"
}

Copy

Apply

Example 2: Update User Organization

PATCH http://localhost:3000/api/users/64a1b2c3d4e5f6789012346/org
Authorization: Bearer YOUR_JWT_TOKEN
Content-Type: application/json

{
"org": "64a1b2c3d4e5f6789012345",
"position": "Senior Developer",
"role": "member"
}

Copy

Apply

7. Specific Issue Routes
   Example 1: Get Single Issue

GET http://localhost:3000/api/issues/64a1b2c3d4e5f6789012348?projectId=64a1b2c3d4e5f6789012347
Authorization: Bearer YOUR_JWT_TOKEN

Copy

Apply

Example 2: Update Issue

PATCH http://localhost:3000/api/issues/64a1b2c3d4e5f6789012348
Authorization: Bearer YOUR_JWT_TOKEN
Content-Type: application/json

{
"status": "in progress",
"assignee": "64a1b2c3d4e5f6789012346"
}

Copy

Apply

8. Health Check Route
   Example 1: Basic Health Check

GET http://localhost:3000/

Copy

Apply

Example 2: API Status Check

GET http://localhost:3000/api/health

Copy

Apply

Important Notes for Testing:
Authentication: Most routes require a JWT token. First, register/login to get a token.

Object IDs: Replace the example ObjectIds (like 64a1b2c3d4e5f6789012345) with actual IDs from your database.

CORS: The server has CORS configured, so make sure your requests include proper headers.

Environment: The server runs on the port specified in your environment configuration.

Middleware: Routes use verifyToken() middleware, so ensure you include the Authorization: Bearer <token> header.

To get started with testing:

Start with user registration/login
Use the returned JWT token for authenticated routes
Create an organization first
Then create projects within that organization
Finally, create and manage issues within projects
