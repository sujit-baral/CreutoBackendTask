# Books API — Node.js Interview Task

## Objective

Build a minimal **Books API** using **Node.js** with **MongoDB**.  
Supports adding books and exploring them via search, filters, pagination, and sorting.

---

## Tech Stack

- **Language:** JavaScript (Node.js)
- **Framework:** Express.js
- **Database:** MongoDB (Mongoose ODM)
- **Environment Variables:** dotenv
- **Dev Tools:** nodemon (optional)

---

## Prerequisites

- Node.js v16+
- MongoDB (local or Atlas)
- npm or yarn

---

## Setup

1. **Clone the repository**

```bash
git clone <your-repo-url>
cd <project-folder>

2.Install dependencies
npm install

3.Create .env file in the root folder
PORT=4000
DB_URL=mongodb://localhost:27017/booksdb(Replace DB_URL in .env with your MongoDB connection string )

4.Seed the database (adds 15+ example books)
run node seed.js
This will insert example books inside the MongoDB database.

Running the Server
Development (with auto-restart):
nodemon index.js

Production:
nodemon index.js
Server will run on http://localhost:4000 (or the port specified in .env).

API Endpoints
1. Create a Book
POST /storebook
Request Body (JSON):

{
  "name": "Node Basics",
  "description": "Intro to Node.js runtime",
  "author": "Sujit",
  "publishDate": "2022-01-10"
}

Response:

{
  "_id": "697f7765ee3a8f8b8200faf9",
  "name": "Node Basics",
  "description": "Intro to Node.js runtime",
  "author": "Sujit",
  "publishDate": "2022-01-10T00:00:00.000Z",
  "createdAt": "2026-02-03T10:00:00.000Z",
  "updatedAt": "2026-02-03T10:00:00.000Z",
  "__v": 0
}
Note: name, description, and author are required. publishDate is optional.

2. Explore Books
GET /books
Query Parameters:

Parameter	                Description
searchTerm	                Text search in name & description (case-insensitive)
author	                    Exact author name (case-insensitive)
from	                    Start publish date (ISO format)
to	                        End publish date (ISO format)
page	                    Page number (default: 1)
limit	                    Items per page (default: 10, max: 50)
sortBy	                    Field to sort by: name, author, publishDate (default: name)
order	                    Sorting order: asc or desc (default: asc)



Example Request:

GET/books?searchTerm=node&author=Sujit&from=2022-01-01&to=2024-01-01&page=1&limit=5&sortBy=publishDate&order=desc
                         

Example Response:

{
  "page": 1,
  "limit": 5,
  "total": 3,
  "totalPages": 1,
  "books": [
    {
      "_id": "64d2f99f6e7a1c0012345678",
      "name": "System Design",
      "description": "Design large systems",
      "author": "Sujit",
      "publishDate": "2024-01-20T00:00:00.000Z",
      "createdAt": "2026-02-01T10:00:00.000Z",
      "updatedAt": "2026-02-01T10:00:00.000Z",
      "__v": 0
    },
    {
      "_id": "64d2f99f6e7a1c0012345679",
      "name": "Node Basics",
      "description": "Intro to Node.js runtime",
      "author": "Sujit",
      "publishDate": "2022-01-10T00:00:00.000Z",
      "createdAt": "2026-02-01T10:00:00.000Z",
      "updatedAt": "2026-02-01T10:00:00.000Z",
      "__v": 0
    }
  ]
}

Behavior Notes
  . ISO date format is used in all requests/responses.
  . Search and author filters are case-insensitive.
  . Pagination includes page, limit, total, and totalPages.
  . Sorting is applied after filters.
  . Indexes exist on name, author, and publishDate for performance.
  . Text index on name & description enables full-text search.

Seed Data
The seed script adds ≥15 books with diverse:
   . Authors: Keshab, Ravi, Anita, Rohit, Robert 
   . Publish dates: 2017–2024

Notes
   Replace DB_URL in .env with your MongoDB connection string.
   You can test endpoints using Postman 

## Postman Collection

A Postman collection is provided to test the API easily.

### Steps to Use:

1. Open Postman.
2. Click **Import → File → Choose File**.
3. Select `BooksAPI.postman_collection.json` from the project.
4. The collection includes:
   - `POST /storebook` → pre-filled with sample fields (`name`, `description`, `author`, `publishDate`)
   - `GET /books` → with example query parameters (search, author, date range, pagination, sorting)
5. Optionally, select the **Books API environment** (if included) to use variables for auto-filling fields like `publishDate`.

 You can modify the fields in the pre-filled request body or environment variables before sending requests.

#
