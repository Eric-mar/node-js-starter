# Step 3: Introduction to Express.js

Now that you understand how to build servers with Node.js core modules, let's learn Express.js - a powerful framework that makes building web applications much easier!

## Learning Objectives

By the end of this step, you will:

- Understand what Express.js is and why we use it
- Install Express.js and set up a project
- Create a basic Express application
- Understand Express routing
- Learn the difference between Node.js HTTP and Express

## What is Express.js?

Express.js is a minimal and flexible Node.js web application framework that provides a robust set of features for building web and mobile applications. It simplifies the process of creating HTTP servers and handling routes.

## Getting Started

### Setting Up Your Project

1. **Initialize npm project** (if you haven't already):

   ```bash
   npm init -y
   ```

2. **Install Express:**

   ```bash
   npm install express
   ```

3. **Create your first Express app file** - `app.js`

## Exercises

### Exercise 1: Basic Express Server

**Task:** Create a simple Express server that responds with "Hello from Express!".

**Instructions:**

1. Create a file `app.js`
2. Import Express using `require('express')`
3. Create an Express app instance by calling `express()`
4. Set up a route for the root path `/` that sends a response
5. Make the app listen on port 3000
6. Add a console.log to confirm the server is running

**What to explore:**

- How is this different from the Node.js HTTP server you built?
- Notice how much simpler the code is!

### Exercise 2: Multiple Routes

**Task:** Create an Express app with multiple routes.

**Instructions:**

1. Create routes for:
   - `/` - Home page with a welcome message
   - `/about` - About page with information about your project
   - `/contact` - Contact page with contact information
2. Each route should return HTML content
3. Test all routes in your browser

**Think about:**

- How does Express handle routing compared to Node.js HTTP?
- Notice you don't need to manually parse URLs!

### Exercise 3: Route Parameters

**Task:** Create routes that use dynamic parameters.

**Instructions:**

1. Create a route `/user/:id` that displays the user ID
2. Create a route `/product/:name` that displays the product name
3. Access the parameters using `req.params`
4. Make the responses dynamic based on the parameters

**What to learn:**

- How to use `:parameterName` syntax in routes
- How to access route parameters with `req.params`

### Exercise 4: Different HTTP Methods

**Task:** Create routes that handle different HTTP methods.

**Instructions:**

1. Create a GET route `/api/data` that returns some data
2. Create a POST route `/api/data` that accepts data
3. Create a PUT route `/api/data/:id` for updating
4. Create a DELETE route `/api/data/:id` for deleting
5. Use `app.get()`, `app.post()`, `app.put()`, `app.delete()`

**Explore:**

- How Express handles different HTTP methods
- The difference between GET and POST requests

### Exercise 5: Sending JSON Responses

**Task:** Create API endpoints that return JSON data.

**Instructions:**

1. Create a route `/api/products` that returns an array of products (as JSON)
2. Create a route `/api/users` that returns an array of users (as JSON)
3. Use `res.json()` instead of `res.send()`
4. Each product/user should have at least 3 properties

**Important:**

- Express automatically sets Content-Type to `application/json` when using `res.json()`
- Notice how clean this is compared to manually setting headers!

## Hints and Tips

### For Exercise 1: Basic Express Server

- Import Express: `const express = require('express')`
- Create app: `const app = express()`
- Create route: `app.get('/', (req, res) => { ... })`
- Send response: `res.send('Your message here')`
- Start server: `app.listen(port, callback)`

### For Exercise 2: Multiple Routes

- Use `app.get()` for each route
- Each route handler receives `(req, res)` parameters
- You can send HTML strings directly with `res.send()`
- Try using template literals for multi-line HTML

### For Exercise 3: Route Parameters

- Use `:parameterName` in your route path, e.g., `/user/:id`
- Access parameters with `req.params.parameterName`
- Parameters are always strings, convert to number if needed

### For Exercise 4: Different HTTP Methods

- `app.get()` - Handle GET requests
- `app.post()` - Handle POST requests
- `app.put()` - Handle PUT requests
- `app.delete()` - Handle DELETE requests
- For POST, you'll need to handle request body (we'll learn this in next steps)

### For Exercise 5: Sending JSON

- Use `res.json(object)` to send JSON responses
- Create JavaScript objects/arrays and pass them to `res.json()`
- Express handles the JSON.stringify automatically

## Testing Your Express App

1. **Start your server:**

   ```bash
   node app.js
   ```

2. **Test routes in browser:**

   - Open http://localhost:3000
   - Try all your routes

3. **Test with curl or Postman:**
   ```bash
   curl http://localhost:3000
   curl -X POST http://localhost:3000/api/data
   ```

## Checklist

Before moving to Step 4, make sure you can:

- [ ] Install Express using npm
- [ ] Create a basic Express application
- [ ] Set up multiple routes
- [ ] Use route parameters
- [ ] Handle different HTTP methods (GET, POST, PUT, DELETE)
- [ ] Send JSON responses
- [ ] Understand the difference between Express and Node.js HTTP

## Key Concepts

### Express Basics

- `express()` - Create Express application
- `app.get()`, `app.post()`, etc. - Define routes
- `req` - Request object (contains request data)
- `res` - Response object (used to send responses)
- `res.send()` - Send response
- `res.json()` - Send JSON response
- `app.listen()` - Start server

### Request Object (`req`)

- `req.params` - Route parameters
- `req.query` - Query string parameters
- `req.body` - Request body (needs middleware)
- `req.method` - HTTP method
- `req.url` - Request URL

### Response Object (`res`)

- `res.send()` - Send response
- `res.json()` - Send JSON response
- `res.status()` - Set status code
- `res.sendFile()` - Send file

## Express vs Node.js HTTP

**Node.js HTTP:**

- Manual URL parsing
- Manual routing logic
- Manual header setting
- More boilerplate code

**Express:**

- Automatic routing
- Built-in parameter parsing
- Simplified response methods
- Middleware support
- Less code, more features

## Next Steps

Once you've completed all exercises and understand Express basics, you're ready for:
**[Step 4: Express Routes and Middleware](../step-04-routes-middleware/README.md)**

## Common Issues

**Issue:** `Cannot find module 'express'`

- **Solution:** Make sure you ran `npm install express` in the correct directory

**Issue:** Port already in use

- **Solution:** Change the port number or stop other servers

**Issue:** Route not working

- **Solution:** Check the route path matches exactly, including slashes

---

