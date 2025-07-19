# ProjectHub

#### A responsive project management web app inspired by Jira.

- **Client**: TypeScript, React, React Query, Mantine
- **Server**: TypeScript, Node, Express, MongoDB/Mongoose

## Features

- Project
  - Create/edit/delete an issue within a project (Task, Story, or Bug)
  - Drag and drop an issue within a column or between two columns to change its status
  - Filter issues by title or assigned user(s)
  - Search for issues across all projects
- User Account
  - Register, login and logout
  - Edit user profile
- Project Management
  - Create/edit/delete a project
- Admin Settings
  - Edit a member's role (Admin, Project Manager, or Member)

## Further Improvements

- Allow users to create/edit/delete a column
- Add drag and drop for columns
- Make all tables sortable
- Add end-to-end and integration tests

## Run Locally

- Clone repo

```bash
  git clone https://github.com/Om-Shankar-191019/projecthub.git
```

- Client
  - env variable: REACT_APP_API_URL
  - ```
      cd client
      npm install
      npm start
    ```
- Server
  - env variables: PORT, MONGO_URI, ORIGIN, ACCESS_TOKEN_SECRET, TOKEN_EXPIRE_TIME, DEMO_PASSWORD
  - ```
      cd server
      npm install
      npm run dev
    ```
