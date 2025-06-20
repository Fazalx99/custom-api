# Bookstore API

A RESTful API for managing a book collection, built with Node.js, Express, and MongoDB, with an optional frontend interface for interaction.

## APIs and Functionality

The API provides four endpoints for CRUD operations on books:

1. **GET /api/books**
   - **Functionality**: Retrieves a list of all books in the database.
   - **Response**: JSON array of book objects (each with `_id`, `title`, `author`, `year`, `genre`).

2. **POST /api/books**
   - **Functionality**: Creates a new book.
   - **Request Body**: JSON with `title` (string), `author` (string), `year` (number), `genre` (string).
   - **Response**: JSON of the created book.

3. **PUT /api/books/:id**
   - **Functionality**: Updates an existing book by its `_id`. Only provided fields are updated.
   - **Request Body**: JSON with optional fields (`title`, `author`, `year`, `genre`).
   - **Response**: JSON of the updated book.

4. **DELETE /api/books/:id**
   - **Functionality**: Deletes a book by its `_id`.
   - **Response**: JSON confirmation message.

For detailed endpoint information, see `API-Documentation.md`.

## Database Integration

- **Database**: MongoDB, a NoSQL database, is used to store book data.
- **Schema**: Books are stored in a `books` collection with fields: `title` (string, required), `author` (string, required), `year` (number, required), `genre` (string, required).
- **Integration**:
  - The `mongoose` library connects the Express server to MongoDB (running locally on `mongodb://localhost:27017/bookstore`).
  - Mongoose models define the book schema and handle CRUD operations.
  - The server connects to MongoDB on startup, logging success or errors.

## How to Run the Server

### Prerequisites
- Node.js (v14 or higher)
- MongoDB (running locally on port 27017)
- Git (optional, for cloning)

### Setup
1. Clone or download the repository:
   ```bash
   git clone https://github.com/Fazalx99/bookstore-api.git
   cd bookstore-api
   ```
2. Install dependencies:
   ```bash
   npm install
   ```
3. Start MongoDB:
   ```bash
   mongod
   ```
4. Start the server:
   ```bash
   npm start
   ```
   - The server runs on `http://localhost:3000`.
   - Logs will confirm MongoDB connection and server startup.

## How to Run the Frontend Locally (Optional)

The frontend is a single-page HTML application served by the Express server.

1. Ensure the server is running (see above).
2. Open a browser and navigate to `http://localhost:3000`.
3. Use the interface to:
   - Add books via the form (calls `POST /api/books`).
   - View books in the list (calls `GET /api/books`).
   - Edit books using the "Edit" button (calls `PUT /api/books/:id`).
   - Delete books using the "Delete" button (calls `DELETE /api/books/:id`).

The frontend uses Tailwind CSS for styling and JavaScript (`fetch`) for API calls.

## How to Interact with the API

### Tools
- **Postman**: For testing API requests.
- **cURL**: For command-line testing.
- **Browser Console**: For JavaScript-based testing with `fetch`.

### Sample Requests and Responses

1. **GET /api/books**
   - **cURL**:
     ```bash
     curl http://localhost:3000/api/books
     ```
   - **Sample Response**:
     ```json
     [
       {
         "_id": "60c72b2f9b1e8a1f5c8b4567",
         "title": "The Great Gatsby",
         "author": "F. Scott Fitzgerald",
         "year": 1925,
         "genre": "Fiction",
         "__v": 0
       }
     ]
     ```

2. **POST /api/books**
   - **cURL**:
     ```bash
     curl -X POST http://localhost:3000/api/books -H "Content-Type: application/json" -d '{"title":"1984","author":"George Orwell","year":1949,"genre":"Dystopian"}'
     ```
   - **Sample Response**:
     ```json
     {
       "_id": "60c72b2f9b1e8a1f5c8b4568",
       "title": "1984",
       "author": "George Orwell",
       "year": 1949,
       "genre": "Dystopian",
       "__v": 0
     }
     ```

3. **PUT /api/books/:id**
   - **cURL** (replace `:id` with actual `_id`):
     ```bash
     curl -X PUT http://localhost:3000/api/books/60c72b2f9b1e8a1f5c8b4567 -H "Content-Type: application/json" -d '{"title":"The Great Gatsby (Updated)","year":1926}'
     ```
   - **Sample Response**:
     ```json
     {
       "_id": "60c72b2f9b1e8a1f5c8b4567",
       "title": "The Great Gatsby (Updated)",
       "author": "F. Scott Fitzgerald",
       "year": 1926,
       "genre": "Fiction",
       "__v": 0
     }
     ```

4. **DELETE /api/books/:id**
   - **cURL** (replace `:id` with actual `_id`):
     ```bash
     curl -X DELETE http://localhost:3000/api/books/60c72b2f9b1e8a1f5c8b4567
     ```
   - **Sample Response**:
     ```json
     { "message": "Book deleted" }
     ```

### Testing Workflow
1. Use `GET /api/books` to list books and note an `_id`.
2. Use `POST /api/books` to add a new book.
3. Use `PUT /api/books/:id` to update a book.
4. Use `DELETE /api/books/:id` to delete a book.
5. Verify changes via `GET /api/books` or the frontend.

For detailed endpoint specifications, see `API-Documentation.md`.

## Folder Structure
- `server.js`: Main server file with API logic.
- `public/`: Frontend files.
  - `index.html`: Frontend interface.
  - `styles.css`: Custom CSS styles.
- `package.json`: Project dependencies and scripts.
- `README.md`: This file.
- `API-Documentation.md`: Detailed API documentation.

## Notes
- Ensure MongoDB is running before starting the server.
- The API has no authentication; add it for production use.
- Error responses include a `message` field (e.g., `{ "message": "Book not found" }`).

For issues or contributions, see the GitHub repository: `https://github.com/Fazalx99/bookstore-api`.
