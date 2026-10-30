# Express.js REST API — Modular MVC (No Database)

## Requirements / downloads
1. Install **Node.js LTS** from https://nodejs.org/ (npm is included).
2. Install **Postman Desktop** from https://www.postman.com/downloads/.
3. Optional: Install **Visual Studio Code** from https://code.visualstudio.com/.
4. A GitHub account is needed only for GitHub submission.

## Run the project
1. Extract this ZIP.
2. Open the extracted `rest-api-assignment` folder in VS Code.
3. Open Terminal in that folder.
4. Run `npm install`.
5. Run `npm start`.
6. Open `http://localhost:3000` in a browser. You should see `REST API is running`.

The data store is in memory (no MongoDB/MySQL required). Data is cleared whenever the server restarts.

## Postman setup and test order
Import `postman/REST_API_Assignment.postman_collection.json` into Postman.
Keep the server running. Run requests in this order:

1. `POST http://localhost:3000/api/auth/register`
   ```json
   { "name": "Student", "email": "student@example.com", "password": "123456" }
   ```
2. `POST http://localhost:3000/api/auth/login`
   ```json
   { "email": "student@example.com", "password": "123456" }
   ```
   Copy the returned `token`.
3. In Postman, open collection Authorization, choose **Bearer Token**, paste token. All category/course routes require this token.
4. `POST /api/categories` body:
   ```json
   { "name": "Programming", "description": "Programming courses" }
   ```
5. `GET /api/categories`
6. Validation test: `POST /api/categories` with `{}`. Expected **400 Bad Request**.
7. Not found test: `GET /api/categories/9999` (or `GET /api/not-a-route`). Expected **404 Not Found**.
8. Course create body (after creating category id 1):
   ```json
   { "title": "Express Basics", "description": "Intro course", "categoryId": "1" }
   ```

## Routes
### Authentication (public)
- `POST /api/auth/register`
- `POST /api/auth/login`

### Categories (Bearer token required)
- `POST /api/categories`
- `GET /api/categories`
- `GET /api/categories/:id`
- `PUT /api/categories/:id`
- `DELETE /api/categories/:id`

### Courses (Bearer token required)
- `POST /api/courses`
- `GET /api/courses`
- `GET /api/courses/:id`
- `PUT /api/courses/:id`
- `DELETE /api/courses/:id`

## Required evidence for printout
Take real screenshots in Postman after sending each request. Each screenshot must show:
- Student name and roll number/ID written at the top (add these in a Word page or annotate the screenshot).
- Postman request method, full URL, and Headers tab (show Authorization header for protected routes).
- Response status and response body at the bottom.

Required five screenshots:
1. Successful Register and Login responses (you may place both on one page if both are readable).
2. POST categories — 201 Created.
3. GET categories — 200 OK.
4. POST categories with `{}` — 400 Bad Request.
5. GET `/api/categories/9999` — 404 Not Found.

Do not submit sample/fake screenshots as evidence; capture them from your own Postman run.

## GitHub submission
Create a new empty GitHub repository. In this extracted project folder run:
```bash
git init
git add .
git commit -m "Complete Express REST API assignment"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPOSITORY.git
git push -u origin main
```
Replace the URL with your own repository URL. Do not upload `node_modules`.
