# Step 2: Building HTTP Server with Node.js

In this step, you'll learn how to create HTTP servers using Node.js core modules - no frameworks needed!

## Learning Objectives

By the end of this step, you will:

- Understand how HTTP servers work
- Create HTTP servers using Node.js `http` module
- Handle different HTTP methods (GET, POST, etc.)
- Parse URLs and query parameters
- Create simple routing logic
- Handle different response types

## What You'll Build

You'll create a simple HTTP server that can:

- Handle different routes
- Respond to GET requests
- Parse URL parameters
- Return JSON responses
- Serve different content types

## Exercises

### Exercise 1: Basic HTTP Server

**Task:** Create a simple HTTP server that responds with "Hello, World!".

**Instructions:**

1. Create `basicServer.js`
2. Use the `http` module to create a server
3. Make it listen on port 3000
4. Respond with "Hello, World!" to all requests

### Exercise 2: Route Handling

**Task:** Create a server that handles different routes.

**Instructions:**

1. Create `routingServer.js`
2. Handle these routes:
   - `/` - Home page
   - `/about` - About page
   - `/contact` - Contact page
   - 404 for unknown routes

### Exercise 3: Query Parameters

**Task:** Create a server that reads and responds to query parameters.

**Instructions:**

1. Create `queryServer.js`
2. Handle `/greet?name=John` and respond with a greeting
3. Handle `/search?q=nodejs` and respond with search results

### Exercise 4: JSON API Endpoint

**Task:** Create a simple JSON API endpoint.

**Instructions:**

1. Create `apiServer.js`
2. Create `/api/products` endpoint that returns JSON
3. Set proper Content-Type headers
4. Return a list of products

### Exercise 5: Complete Server (Challenge)

**Task:** Build a complete server with multiple features.

**Instructions:**

1. Create `completeServer.js`
2. Combine all previous exercises
3. Add error handling
4. Add proper status codes

## Hints and Tips

### For Exercise 1: Basic HTTP Server
- Import the http module: `const http = require('http')`
- Use `http.createServer()` with a callback function that receives `(req, res)`
- Set response headers with `res.writeHead(statusCode, headersObject)`
- Use `res.end()` to send the response and close the connection
- Call `server.listen(port, callback)` to start listening on a port

### For Exercise 2: Route Handling
- Parse the URL using `url.parse(req.url, true)` - the second parameter makes it parse query strings
- Access the pathname with `parsedUrl.pathname`
- Use `if/else` or `switch` statements to handle different routes
- Remember to set appropriate status codes: 200 for success, 404 for not found
- Set Content-Type header to `'text/html'` for HTML responses

### For Exercise 3: Query Parameters
- After parsing the URL with `url.parse(req.url, true)`, access query parameters with `parsedUrl.query`
- Query parameters come as an object, e.g., `{ name: 'John' }` for `?name=John`
- Check if query parameters exist before using them
- You can create dynamic responses based on query values

### For Exercise 4: JSON API Endpoint
- Set Content-Type header to `'application/json'`
- Use `JSON.stringify()` to convert JavaScript objects to JSON strings
- Create an array of product objects with properties like `id`, `name`, `price`
- Return proper JSON format with appropriate status code (200)

### For Exercise 5: Complete Server
- Combine routing logic from all previous exercises
- Add try-catch blocks for error handling
- Use different status codes appropriately (200, 404, 500)
- Consider using a function to handle different routes cleanly
- Add console.log statements to help debug

## Testing Your Server

1. **Start your server:**

   ```bash
   node basicServer.js
   ```

2. **Test in browser:**

   - Open http://localhost:3000
   - Try different routes

3. **Test with curl (if available):**
   ```bash
   curl http://localhost:3000
   ```

## Checklist

Before moving to Step 3, make sure you can:

- [ ] Create an HTTP server using `http.createServer()`
- [ ] Handle different routes
- [ ] Parse URL and query parameters
- [ ] Set proper HTTP headers
- [ ] Return different content types (text, HTML, JSON)
- [ ] Handle errors and 404 responses
- [ ] Understand request and response objects

## Key Concepts

### HTTP Module

- `http.createServer()` - Create HTTP server
- `req` (request) - Incoming request object
- `res` (response) - Response object
- `res.writeHead()` - Set status code and headers
- `res.end()` - Send response and end connection

### URL Module

- `url.parse()` - Parse URL string
- `parsedUrl.pathname` - Get path
- `parsedUrl.query` - Get query parameters

### HTTP Methods

- `req.method` - Get HTTP method (GET, POST, etc.)

### Status Codes

- `200` - OK
- `404` - Not Found
- `500` - Internal Server Error

## 🔍 Understanding Request and Response

### Request Object (`req`)

- `req.url` - Request URL
- `req.method` - HTTP method
- `req.headers` - Request headers

### Response Object (`res`)

- `res.writeHead(status, headers)` - Set status and headers
- `res.write(data)` - Write response data
- `res.end(data)` - End response (can include data)

## Next Steps

Once you've completed all exercises and understand the concepts, you're ready for:
**[Step 3: Introduction to Express.js](../step-03-intro-express/README.md)**

## Common Issues

**Issue:** Port already in use

- **Solution:** Change the port number or stop the other server

**Issue:** Cannot access server

- **Solution:** Make sure the server is running and check the port number

**Issue:** CORS errors (when testing from browser)

- **Solution:** This is normal for now. We'll handle CORS in Express steps.

---

