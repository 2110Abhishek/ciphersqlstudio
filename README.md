# CipherSQLStudio

A browser-based SQL learning platform for practicing queries in real-time.

## Features
- **Assignment Listing**: View and select SQL assignments with difficulty levels.
- **SQL Editor**: Integrated Monaco Editor for writing complex SQL queries.
- **Real-time Execution**: Run queries against a PostgreSQL sandbox.
- **LLM Hints**: Get intelligent, conversational hints (not solutions) from an AI (Gemini).
- **Mobile Responsive**: Designed for mobile, tablet, and desktop views.

## Tech Stack
- **Frontend**: React.js, Vanilla SCSS, Axios, React Router.
- **Backend**: Node.js, Express.js.
- **Database**: 
  - MongoDB (for persistence of assignments)
  - PostgreSQL (for sandbox query execution)
- **AI**: Google Gemini API.

## Setup Instructions

### Prerequisites
- Node.js installed.
- MongoDB and PostgreSQL instances running.

### 1. Server Setup
```bash
cd server
npm install
cp .env.example .env
# Edit .env with your database URIs and Gemini API Key
npm run dev
```
To seed the initial assignments:
```bash
node src/seed.js
```

### 2. Client Setup
```bash
cd client
npm install
npm start
```

## Data-Flow Diagram
Below is the logic flow. 

```mermaid
graph TD
    A[User clicks 'Execute Query'] --> B[React State Updates: executing=true]
    B --> C[API Call: POST /api/query {query}]
    C --> D[Express Server receives request]
    D --> E[Query Validation: Check for forbidden keywords]
    E -- Valid --> F[Execute query in PostgreSQL Sandbox]
    E -- Invalid --> G[Return 403 Forbidden Error]
    F --> H[Return Query Results or Error]
    H --> I[Express sends JSON Response to Frontend]
    I --> J[React State Updates: results=data, executing=false]
    J --> K[Result Table renders in UI]
```

## Environment Variables
- `MONGO_URI`: MongoDB connection string.
- `PG_URI`: PostgreSQL connection string.
- `GEMINI_API_KEY`: Google Gemini API Key.
- `PORT`: Server port (default 5000).

