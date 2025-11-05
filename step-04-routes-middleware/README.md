# Step 4: Express Routes and Middleware

Now that you understand Express basics, let's dive deeper into routing and learn about middleware - one of the most powerful features of Express!

## Learning Objectives

By the end of this step, you will:

- Understand what middleware is and how it works
- Create and use custom middleware
- Organize routes using Express Router
- Use built-in Express middleware
- Understand the middleware execution order
- Handle errors with middleware

## What is Middleware?

Middleware functions are functions that have access to the request object (`req`), the response object (`res`), and the `next` function in the application's request-response cycle. Middleware can execute code, make changes to the request and response objects, end the request-response cycle, or call the next middleware.

## Exercises

### Exercise 1: Understanding Middleware

**Task:** Create a simple logging middleware that logs every request.

**Instructions:**

1. Create a middleware function that logs the request method and URL
2. Use `app.use()` to apply it to all routes
3. Make sure to call `next()` to pass control to the next middleware
4. Test it by making requests to different routes

**What to learn:**
- How middleware functions receive `req`, `res`, and `next`
- The importance of calling `next()`
- How `app.use()` applies middleware to all routes

### Exercise 2: Route-Specific Middleware

**Task:** Create middleware that only runs for specific routes.

**Instructions:**

1. Create a middleware function that checks if a user is authenticated (simplified - just check for a header)
2. Apply this middleware only to `/api/protected` routes
3. If authenticated, allow access; if not, send a 401 error
4. Create both protected and unprotected routes to test

**Think about:**
- How to apply middleware to specific routes
- How to stop the request-response cycle when needed

### Exercise 3: Request Body Parsing

**Task:** Set up middleware to parse JSON request bodies.

**Instructions:**

1. Use `express.json()` middleware to parse JSON bodies
2. Apply it using `app.use()`
3. Create a POST route that accepts JSON data
4. Log and return the received data

**What to explore:**
- How `express.json()` works
- How to access parsed data in `req.body`
- Why this middleware must come before routes that need it

### Exercise 4: Organizing Routes with Router

**Task:** Organize your routes using Express Router.

**Instructions:**

1. Create a `routes` folder
2. Create separate route files:
   - `products.js` - for product routes
   - `users.js` - for user routes
3. Use `express.Router()` in each file
4. Export the routers and use them in `app.js` with `app.use()`

**Benefits:**
- Better code organization
- Easier to maintain
- Scalable structure

### Exercise 5: Error Handling Middleware

**Task:** Create error handling middleware.

**Instructions:**

1. Create middleware that catches errors
2. Error handling middleware has 4 parameters: `(err, req, res, next)`
3. Handle different types of errors appropriately
4. Create a route that intentionally throws an error to test

**Important:**
- Error handling middleware must be defined last
- It must have 4 parameters (err, req, res, next)

### Exercise 6: Custom Middleware for Validation

**Task:** Create middleware that validates request data.

**Instructions:**

1. Create middleware that validates POST requests
2. Check if required fields are present
3. Validate data types (e.g., name should be string, age should be number)
4. Send appropriate error messages if validation fails
5. Only call `next()` if validation passes

## Hints and Tips

### For Exercise 1: Understanding Middleware
- Middleware function signature: `(req, res, next) => { ... }`
- Use `app.use(middlewareFunction)` to apply to all routes
- Always call `next()` at the end (unless you're ending the response)
- You can log using `console.log(req.method, req.url)`

### For Exercise 2: Route-Specific Middleware
- You can pass middleware as the second argument to route methods: `app.get('/path', middleware, handler)`
- Or use `app.use('/path', middleware)` to apply to specific paths
- To end the request: `res.status(401).send('Unauthorized')`
- Access headers with `req.headers['header-name']`

### For Exercise 3: Request Body Parsing
- Use `app.use(express.json())` to parse JSON bodies
- This must be added before routes that need it
- After parsing, access data with `req.body`
- For POST requests, the body will be automatically parsed

### For Exercise 4: Organizing Routes with Router
- Create router: `const router = express.Router()`
- Define routes on router: `router.get('/path', handler)`
- Export: `module.exports = router`
- In main app: `const productsRouter = require('./routes/products')` then `app.use('/api/products', productsRouter)`

### For Exercise 5: Error Handling Middleware
- Error middleware signature: `(err, req, res, next) => { ... }`
- Must have 4 parameters (Express recognizes it by this)
- Place it after all routes and other middleware
- Throw errors: `throw new Error('Message')` or `next(new Error('Message'))`
- Access error: `err.message`

### For Exercise 6: Custom Validation Middleware
- Check `req.body` for required fields
- Use `typeof` to check data types
- Return early with error response if validation fails
- Call `next()` only if validation succeeds

## Testing Your Middleware

1. **Test logging middleware:**
   - Make requests to different routes
   - Check console for logs

2. **Test authentication middleware:**
   - Try accessing protected routes without auth header
   - Try with auth header

3. **Test body parsing:**
   - Send POST requests with JSON body
   - Check if `req.body` contains the data

4. **Test error handling:**
   - Trigger errors intentionally
   - Verify error responses

## Checklist

Before moving to Step 5, make sure you can:

- [ ] Create and use custom middleware
- [ ] Apply middleware to all routes or specific routes
- [ ] Use `express.json()` for body parsing
- [ ] Organize routes using Express Router
- [ ] Create error handling middleware
- [ ] Understand middleware execution order
- [ ] Create validation middleware

## Key Concepts

### Middleware Basics
- Middleware functions: `(req, res, next) => { ... }`
- `app.use()` - Apply middleware to all routes
- `app.use('/path', middleware)` - Apply to specific paths
- `next()` - Pass control to next middleware
- Order matters - middleware executes in order

### Built-in Middleware
- `express.json()` - Parse JSON request bodies
- `express.urlencoded()` - Parse URL-encoded bodies
- `express.static()` - Serve static files

### Express Router
- `express.Router()` - Create router instance
- Organize routes into separate files
- Mount routers with `app.use('/prefix', router)`

### Error Handling
- Error middleware: `(err, req, res, next) => { ... }`
- Must have 4 parameters
- Place after all routes
- Use `next(err)` to pass errors to error handler

## 🔍 Middleware Execution Order

1. Request comes in
2. Middleware defined with `app.use()` (in order)
3. Route-specific middleware
4. Route handler
5. Error handling middleware (if error occurs)

## Next Steps

Once you've completed all exercises and understand middleware, you're ready for:
**[Step 5: JSON and Data Handling](../step-05-json-data/README.md)**

## Common Issues

**Issue:** Middleware not running
- **Solution:** Check if you called `next()` in previous middleware

**Issue:** `req.body` is undefined
- **Solution:** Make sure `express.json()` middleware is added before routes

**Issue:** Error handler not catching errors
- **Solution:** Make sure error middleware has 4 parameters and is defined last

**Issue:** Routes not working after adding middleware
- **Solution:** Check middleware order and ensure `next()` is called

---


