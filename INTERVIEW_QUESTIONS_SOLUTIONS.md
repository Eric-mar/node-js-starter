# Interview Questions Solutions - Node.js & Express.js

This document provides brief answers to all interview questions. Use these as a reference, but remember to explain concepts in your own words during interviews.

---

## Beginner Level Questions

### 1. What is Node.js and what problem does it solve?

**Answer:** Node.js is a JavaScript runtime built on Chrome's V8 engine that allows JavaScript to run on the server. It solves the problem of using JavaScript for backend development, enabling developers to use one language (JavaScript) for both frontend and backend. It's particularly good for I/O-intensive applications due to its non-blocking, event-driven architecture.

### 2. Explain the difference between JavaScript in the browser and Node.js.

**Answer:** Browser JavaScript runs in the browser and has access to DOM, window objects, and browser APIs. Node.js runs on the server and provides access to file system, HTTP modules, and other server-side capabilities. Node.js doesn't have DOM or window objects, but has `global` object and modules like `fs`, `http`, etc.

### 3. What is npm and what is it used for?

**Answer:** npm (Node Package Manager) is the default package manager for Node.js. It's used to install, manage, and share JavaScript packages/libraries. It maintains a registry of packages and handles dependencies through `package.json` file.

### 4. What is the difference between `var`, `let`, and `const`?

**Answer:** `var` is function-scoped and can be redeclared. `let` and `const` are block-scoped. `let` can be reassigned, `const` cannot be reassigned after declaration. `const` doesn't make objects immutable, only prevents reassignment of the variable itself.

### 5. What is `module.exports` and how do you use it?

**Answer:** `module.exports` is used to export functions, objects, or values from a Node.js module so they can be imported in other files using `require()`. Example: `module.exports = function() {}` or `module.exports = { function1, function2 }`.

### 6. What is the difference between `require()` and `import`?

**Answer:** `require()` is CommonJS (Node.js default) - synchronous, returns module.exports. `import` is ES6 modules - asynchronous, must use `.mjs` extension or `"type": "module"` in package.json. `import` is static (analyzed at compile time), `require()` is dynamic.

### 7. What is Express.js and why would you use it instead of plain Node.js?

**Answer:** Express.js is a minimal web framework for Node.js. It simplifies building web applications by providing routing, middleware, template engines, and easier request/response handling. It reduces boilerplate code compared to using Node.js HTTP module directly.

### 8. What is middleware in Express.js?

**Answer:** Middleware are functions that execute during the request-response cycle. They have access to `req`, `res`, and `next`. They can execute code, modify request/response, end the cycle, or call the next middleware. Examples: authentication, logging, body parsing.

### 9. How do you create a route in Express?

**Answer:** Use `app.METHOD(path, handler)` where METHOD is get, post, put, delete, etc. Example: `app.get('/users', (req, res) => { res.send('Users') })`. Or use Express Router: `router.get('/path', handler)`.

### 10. What is the difference between `app.get()` and `app.use()`?

**Answer:** `app.get()` handles only GET requests for a specific route. `app.use()` applies middleware to all HTTP methods and routes matching the path (or all routes if no path specified). `app.use()` is for middleware, `app.get()` is for route handlers.

### 11. How do you send JSON responses in Express?

**Answer:** Use `res.json(object)`. Express automatically sets Content-Type to `application/json` and calls `JSON.stringify()`. Example: `res.json({ message: 'Success' })`. Alternative: `res.send({ data })` also works for JSON.

### 12. What is `req.params` used for?

**Answer:** `req.params` contains route parameters (URL path parameters). Example: For route `/users/:id`, accessing `/users/123` gives `req.params.id = '123'`. Used for dynamic route segments.

### 13. What is `req.query` used for?

**Answer:** `req.query` contains query string parameters from the URL. Example: For `/search?q=nodejs&page=1`, `req.query.q = 'nodejs'` and `req.query.page = '1'`. Used for optional filtering, pagination, search terms.

### 14. What is `req.body` and how do you access it?

**Answer:** `req.body` contains parsed request body data (from POST/PUT requests). Requires `express.json()` middleware for JSON bodies. Access: `req.body.fieldName`. Example: `app.use(express.json())` then `req.body.name` for JSON `{ "name": "John" }`.

### 15. What is a callback function?

**Answer:** A callback is a function passed as an argument to another function, executed after the first function completes. In Node.js, used for asynchronous operations. Example: `fs.readFile('file.txt', (err, data) => { /* callback */ })`.

### 16. What is a Promise?

**Answer:** A Promise represents the eventual completion (or failure) of an asynchronous operation. It has states: pending, fulfilled, rejected. Provides `.then()`, `.catch()`, `.finally()` methods. Better than callbacks for handling async code.

### 17. What is async/await?

**Answer:** `async/await` is syntactic sugar for Promises. `async` functions return Promises. `await` pauses execution until Promise resolves. Makes asynchronous code look synchronous. Must use `try/catch` for error handling.

### 18. What are HTTP status codes? Give examples.

**Answer:** HTTP status codes indicate response status. 2xx = success (200 OK, 201 Created), 4xx = client error (400 Bad Request, 401 Unauthorized, 404 Not Found), 5xx = server error (500 Internal Server Error).

### 19. What is REST and what makes an API RESTful?

**Answer:** REST (Representational State Transfer) is an architectural style. RESTful APIs use: resource-based URLs (`/users`, `/products`), HTTP methods (GET, POST, PUT, DELETE), stateless requests, JSON responses, proper status codes.

### 20. What is the difference between GET and POST requests?

**Answer:** GET requests data (idempotent, safe, parameters in URL, cached). POST submits data (not idempotent, creates/updates resources, data in body, not cached). Use GET to retrieve, POST to create.

---

## Intermediate Level Questions

### 21. Explain the Node.js event loop. How does it work?

**Answer:** The event loop monitors the call stack and callback queue. When call stack is empty, it moves callbacks from queue to stack. It has phases: timers, pending callbacks, idle/prepare, poll, check, close callbacks. Enables non-blocking I/O.

### 22. What is the difference between blocking and non-blocking code?

**Answer:** Blocking code stops execution until operation completes (e.g., `fs.readFileSync()`). Non-blocking code continues execution, uses callbacks/Promises (e.g., `fs.readFile()`). Node.js is non-blocking by default, which enables high concurrency.

### 23. How do you handle errors in Express applications?

**Answer:** Use try-catch blocks in async functions, error-handling middleware (4 parameters: `err, req, res, next`), consistent error format, appropriate status codes. Error middleware must be defined last. Use `next(error)` to pass errors to handler.

### 24. What is the order of middleware execution in Express?

**Answer:** Middleware executes in order of definition: application-level middleware (`app.use()`), route-specific middleware, route handler, error-handling middleware (if error occurs). Order matters - define middleware before routes that need it.

### 25. How do you structure a Node.js/Express project?

**Answer:** Organize into folders: `routes/` (route definitions), `controllers/` (business logic), `models/` (data models), `middleware/` (custom middleware), `utils/` (helpers), `config/` (configuration). Keep `app.js` as entry point. Separate concerns.

### 26. What are environment variables and why use them?

**Answer:** Environment variables store configuration outside code (API keys, database URLs, ports). Accessed via `process.env`. Use `.env` file with `dotenv` package. Benefits: security (no secrets in code), different configs for dev/prod, easy changes.

### 27. How do you implement authentication in an Express app?

**Answer:** User provides credentials (username/password), server validates, generates token (JWT), returns token. Client sends token in Authorization header. Server validates token on protected routes using middleware. Can use sessions or tokens.

### 28. What is JWT and how does it work?

**Answer:** JWT (JSON Web Token) is a token-based authentication. Contains header, payload (user data), signature. Generated on login, sent to client, stored client-side. Client includes in Authorization header. Server validates signature and extracts user info.

### 29. Why should you never store passwords in plain text?

**Answer:** Security risk - if database is breached, all passwords exposed. Users often reuse passwords. Legal/compliance issues. Solution: Hash passwords using bcrypt with salt. Never return password hashes in API responses.

### 30. What is CORS and how do you handle it in Express?

**Answer:** CORS (Cross-Origin Resource Sharing) allows browsers to make requests to different origins. Browsers block cross-origin by default. In Express: `app.use(cors())` or configure allowed origins. Required when frontend and backend are on different domains.

### 31. What is the difference between authentication and authorization?

**Answer:** Authentication verifies WHO the user is (login process). Authorization verifies WHAT the user can do (permissions, roles). Authentication comes first, then authorization checks if user can access specific resources.

### 32. How do you validate input data in Express?

**Answer:** Use validation middleware or libraries (joi, express-validator). Check required fields, data types, constraints (positive numbers, email format). Return clear error messages. Validate before processing data.

### 33. What is the difference between PUT and PATCH?

**Answer:** PUT replaces entire resource (must send complete resource, idempotent). PATCH partially updates resource (only send fields to update, not necessarily idempotent). Use PUT for full updates, PATCH for partial updates.

### 34. How do you organize routes in Express?

**Answer:** Use Express Router: create separate route files, use `express.Router()`, define routes on router, export router, mount in `app.js` with `app.use('/prefix', router)`. Organize by resource (users, products, orders).

### 35. What is Express Router and when should you use it?

**Answer:** Express Router is a mini Express app for routing. Use it to organize routes into separate files, create modular route handlers, apply middleware to route groups, improve code organization. Better for larger applications.

### 36. How do you handle file uploads in Express?

**Answer:** Use `multer` middleware. Configure storage (disk or memory), set file size limits, validate file types. Access uploaded file via `req.file` (single) or `req.files` (multiple). Can store locally or upload to cloud storage.

### 37. What is rate limiting and why is it important?

**Answer:** Rate limiting restricts number of requests from a client/IP in a time window. Prevents brute force attacks, DDoS, API abuse. Use `express-rate-limit`. Configure window size and max requests. Can be IP-based or user-based.

### 38. How do you implement pagination in an API?

**Answer:** Accept `page` and `limit` query parameters. Calculate `skip = (page - 1) * limit`. Use database `LIMIT` and `OFFSET` or array `slice()`. Return paginated data with metadata (total, totalPages, currentPage). Improves performance and UX.

### 39. What is the difference between `req.params`, `req.query`, and `req.body`?

**Answer:** `req.params` - route parameters from URL path (`/users/:id`). `req.query` - query string parameters (`?page=1`). `req.body` - request body data (POST/PUT, requires `express.json()`). Each serves different purpose in request handling.

### 40. How do you handle async errors in Express?

**Answer:** Wrap async route handlers in try-catch, use `next(error)` to pass to error middleware. Or create wrapper function: `const asyncHandler = (fn) => (req, res, next) => Promise.resolve(fn(req, res, next)).catch(next)`. Use wrapper for cleaner code.

### 41. What is separation of concerns in backend development?

**Answer:** Dividing code into logical layers: Routes handle HTTP, Controllers contain business logic, Models handle data access, Services provide reusable logic, Middleware handles cross-cutting concerns. Each layer has single responsibility. Improves maintainability.

### 42. How do you implement search functionality in an API?

**Answer:** Accept search query parameter. Use database full-text search or array filtering. Search across multiple fields using `$or` or `filter()`. Support fuzzy search, case-insensitive matching. Can use search libraries (Elasticsearch) for advanced features.

### 43. What is the purpose of `process.env` in Node.js?

**Answer:** `process.env` is an object containing environment variables. Access configuration values (port, database URL, API keys). Set by OS or `.env` file (with dotenv). Use `process.env.PORT` or `process.env.DATABASE_URL`. Always provide defaults.

### 44. How do you test Express APIs?

**Answer:** Use testing frameworks: Jest, Mocha, Supertest. Test endpoints with HTTP assertions. Test different scenarios: success, errors, validation. Use Supertest: `request(app).get('/api/users').expect(200)`. Write unit tests for functions, integration tests for routes.

### 45. What is input validation and why is it important?

**Answer:** Input validation checks if data meets requirements before processing. Important for: security (prevent injection attacks), data integrity (correct format), user experience (clear errors), system stability (prevent crashes). Validate types, required fields, constraints.

### 46. How do you implement error handling middleware?

**Answer:** Create middleware with 4 parameters: `(err, req, res, next) => {}`. Must have 4 parameters for Express to recognize as error handler. Place after all routes. Handle different error types, return appropriate status codes, log errors, return consistent format.

### 47. What is the difference between `throw` and `next(error)`?

**Answer:** `throw error` throws in current execution context, must be caught with try-catch. `next(error)` passes error to Express error-handling middleware. In Express, prefer `next(error)` to properly trigger error middleware. Both work, but `next()` is Express-specific.

### 48. How do you create a CRUD API in Express?

**Answer:** Create routes for each operation: GET (read), POST (create), PUT/PATCH (update), DELETE (delete). Use appropriate HTTP methods and status codes. Implement in controllers, use proper validation, handle errors. Follow RESTful conventions.

### 49. What is the difference between SQL and NoSQL databases?

**Answer:** SQL (relational): structured tables, relationships, ACID compliance, fixed schema (PostgreSQL, MySQL). NoSQL: flexible schema, document/key-value/graph, horizontal scaling, simpler queries (MongoDB, Redis). Choose based on data structure and requirements.

### 50. What security best practices should you follow in Express?

**Answer:** Use HTTPS, validate/sanitize inputs, hash passwords, use environment variables, implement rate limiting, use Helmet.js for security headers, prevent SQL injection, handle CORS properly, don't expose internal errors, keep dependencies updated, use authentication/authorization.

---

## Advanced Level Questions

### 51. Explain the Node.js event loop phases in detail.

**Answer:** Phases: 1) Timers - execute setTimeout/setInterval callbacks, 2) Pending callbacks - execute I/O callbacks deferred, 3) Idle/prepare - internal use, 4) Poll - fetch new I/O events, execute I/O callbacks, 5) Check - execute setImmediate callbacks, 6) Close - execute close callbacks. Process repeats.

### 52. How do you implement database transactions in Node.js?

**Answer:** Use database libraries that support transactions (Sequelize, TypeORM). Start transaction, execute operations, commit on success, rollback on error. Example: `await sequelize.transaction(async (t) => { await Model.create({}, { transaction: t }) })`. Ensures data consistency.

### 53. What is connection pooling and why is it important?

**Answer:** Connection pooling reuses database connections instead of creating new ones for each request. Improves performance, efficient resource usage, manages connection limits. Most database drivers support it automatically. Configure pool size based on application needs.

### 54. How do you optimize Node.js application performance?

**Answer:** Use caching (Redis, in-memory), optimize database queries (indexes), use compression middleware, implement connection pooling, use CDN for static files, code optimization (avoid blocking operations), load balancing, monitoring, profiling, async operations.

### 55. What is the difference between `process.nextTick()` and `setImmediate()`?

**Answer:** `process.nextTick()` executes before any other async operation (highest priority, can starve event loop). `setImmediate()` executes in next iteration of event loop (lower priority, better for I/O). Use `setImmediate()` unless you need highest priority.

### 56. How do you handle memory leaks in Node.js applications?

**Answer:** Use memory profiling tools, check for: unclosed connections, global variables growing, event listeners not removed, closures keeping references, circular references. Use `--inspect` flag, Chrome DevTools, heap snapshots. Fix by removing listeners, closing connections, avoiding global accumulation.

### 57. What is the cluster module in Node.js and when would you use it?

**Answer:** Cluster module allows creating child processes that share server ports. Utilizes multiple CPU cores. Master process creates workers, distributes connections. Use for CPU-intensive tasks, scaling across cores. Better than single process for multi-core systems.

### 58. How do you implement caching in a Node.js application?

**Answer:** Use in-memory cache (simple objects), Redis (distributed cache), Memcached, or Node-cache. Cache frequently accessed data, API responses, database queries. Implement cache invalidation strategies. Set TTL (time-to-live). Use for performance optimization.

### 59. What is the difference between child_process and worker_threads?

**Answer:** `child_process` spawns separate processes (isolated memory, IPC communication, heavier). `worker_threads` creates threads in same process (shared memory, faster communication, lighter). Use child_process for isolation, worker_threads for CPU-intensive tasks in Node.js.

### 60. How do you implement real-time features (WebSockets) in Express?

**Answer:** Use Socket.io library. Install, create Socket.io server, handle connections, emit/receive events. Example: `io.on('connection', (socket) => { socket.on('message', (data) => {}) })`. Enables bidirectional communication, real-time updates, chat applications.

### 61. How do you handle database migrations in Node.js?

**Answer:** Use migration tools (Sequelize CLI, Knex.js, TypeORM). Create migration files, define schema changes (up/down), run migrations in order, version control migrations. Migrations track schema changes, enable rollbacks, maintain consistency across environments.

### 62. What is the difference between an ORM and ODM?

**Answer:** ORM (Object-Relational Mapping) maps database tables to objects (SQL databases - Sequelize, TypeORM). ODM (Object-Document Mapping) maps documents to objects (NoSQL - Mongoose for MongoDB). Both provide abstraction, easier queries, relationships, migrations.

### 63. How do you implement microservices architecture with Node.js?

**Answer:** Break application into independent services, each with own database, communicate via APIs/message queues, use service discovery, implement API gateway, handle distributed transactions, implement circuit breakers, use containers (Docker), orchestrate with Kubernetes.

### 64. How do you handle distributed transactions?

**Answer:** Use patterns: Saga pattern (choreography/orchestration), Two-Phase Commit (2PC), Event Sourcing, Compensating transactions. Saga coordinates transactions across services, handles failures with compensating actions. More complex than single-database transactions.

### 65. What is the purpose of message queues and when would you use them?

**Answer:** Message queues enable asynchronous communication between services. Use for: decoupling services, handling spikes in traffic, background job processing, event-driven architecture. Examples: RabbitMQ, AWS SQS, Redis. Services produce/consume messages.

### 66. How do you implement API versioning?

**Answer:** Version in URL (`/api/v1/users`), headers (`Accept: application/vnd.api+json;version=1`), or query parameter (`?version=1`). URL versioning is most common. Update routes, maintain backward compatibility, deprecate old versions gradually.

### 67. How do you handle large file uploads in Node.js?

**Answer:** Use streaming (`fs.createReadStream()`), chunked uploads, multipart handling, progress tracking, resumable uploads. Use libraries like `multer` with streaming, `formidable`. Store in chunks, validate size limits, handle errors gracefully, consider cloud storage.

### 68. What is the difference between horizontal and vertical scaling?

**Answer:** Horizontal scaling: add more servers/machines (scale out). Vertical scaling: add more resources to existing server (scale up). Horizontal is preferred for cloud, better for high availability. Vertical has limits, easier initially.

### 69. How do you implement observability (logging, monitoring, tracing) in Node.js?

**Answer:** Logging: Winston, Pino, structured logging. Monitoring: Prometheus, Grafana, APM tools. Tracing: OpenTelemetry, distributed tracing. Metrics: collect performance data, error rates, response times. Use tools: New Relic, DataDog, Elastic Stack.

### 70. How do you secure an Express API against common vulnerabilities?

**Answer:** Use Helmet.js (security headers), validate inputs, sanitize data, use parameterized queries (SQL injection), implement rate limiting, use HTTPS, secure authentication, CORS configuration, keep dependencies updated, use security linters, implement proper error handling.

### 71. How do you implement GraphQL in Node.js?

**Answer:** Use GraphQL libraries (Apollo Server, GraphQL.js). Define schema (types, queries, mutations), create resolvers, set up server. GraphQL provides single endpoint, flexible queries, type system. Alternative to REST for flexible data fetching.

### 72. What is the difference between server-side rendering and API-based architecture?

**Answer:** SSR: server renders HTML, sends complete page (Next.js, EJS). API-based: server provides JSON API, client renders (React, Vue with Express API). SSR: better SEO, faster initial load. API: better separation, scalability, flexibility.

### 73. How do you implement rate limiting with different strategies?

**Answer:** Fixed window: limit per time window. Sliding window: smoother distribution. Token bucket: allows bursts. Leaky bucket: smooths bursts. Implement with Redis for distributed systems. Can be IP-based, user-based, route-specific. Use libraries: express-rate-limit, rate-limiter-flexible.

### 74. How do you handle graceful shutdown in Node.js applications?

**Answer:** Listen for termination signals (SIGTERM, SIGINT), stop accepting new requests, finish current requests, close database connections, cleanup resources, then exit. Use `process.on('SIGTERM', gracefulShutdown)`. Important for zero-downtime deployments.

### 75. What is the difference between event-driven and request-response architectures?

**Answer:** Request-response: client sends request, waits for response (synchronous, REST). Event-driven: services emit/consume events (asynchronous, decoupled). Event-driven: better for real-time, microservices, loose coupling. Request-response: simpler, better for direct queries.

---

## Scenario-Based Questions

### 76. How would you design an ecommerce API with products, users, and orders?

**Answer:** Separate resources: Products API (CRUD), Users API (registration, login, profile), Orders API (create, track, update). Use RESTful conventions, authentication middleware, relationships (orders belong to users, contain products). Implement proper validation, error handling, pagination.

### 77. How would you implement a social media API with posts, comments, and likes?

**Answer:** Posts API (CRUD), Comments API (nested, belongs to posts), Likes API (toggle likes). Use relationships, nested routes (`/posts/:id/comments`), real-time updates (WebSockets), pagination, search. Implement permissions (users can edit own posts).

### 78. How would you build a real-time chat application backend?

**Answer:** Use Socket.io for WebSockets, handle connections, rooms/channels, message broadcasting, user presence, typing indicators. Store messages in database, implement message history, authentication for sockets, handle reconnections, rate limiting.

### 79. How would you design a file upload service with progress tracking?

**Answer:** Use streaming uploads, chunked uploads, track progress with events, store metadata in database, implement resumable uploads, validate file types/sizes, use cloud storage (S3), provide download endpoints, implement cleanup for failed uploads.

### 80. How would you implement a notification system?

**Answer:** Create notifications table, endpoints to create/read/update notifications, real-time delivery via WebSockets, background jobs for scheduled notifications, different notification types, user preferences, mark as read/unread, batch notifications.

### 81. How would you build a search API that can handle millions of records?

**Answer:** Use search engines (Elasticsearch, Algolia), implement indexing, full-text search, faceted search, pagination, caching, debouncing for search queries, ranking algorithms, handle typos (fuzzy search), optimize queries.

### 82. How would you implement a payment processing system?

**Answer:** Integrate payment gateways (Stripe, PayPal), handle webhooks, secure payment data (PCI compliance), idempotency keys, transaction logging, refund handling, payment status tracking, error handling, test with sandbox environments.

### 83. How would you design a multi-tenant SaaS application backend?

**Answer:** Tenant isolation (separate databases or shared with tenant_id), middleware to identify tenant, row-level security, tenant-specific configurations, data isolation, billing per tenant, tenant management API, migration strategies.

### 84. How would you implement a recommendation engine API?

**Answer:** Collect user behavior data, implement algorithms (collaborative filtering, content-based), calculate similarities, generate recommendations, cache results, A/B testing, personalization based on user history, real-time vs batch processing.

### 85. How would you build a scalable image processing service?

**Answer:** Accept image uploads, queue processing jobs, use image processing libraries (Sharp, ImageMagick), generate thumbnails/variants, store in CDN, implement resizing/optimization, background workers, progress tracking, error handling, support multiple formats.

---

## Coding Challenges - Brief Approaches

### Challenge 1: Create a RESTful API

**Approach:** Set up Express app, create routes for posts/comments/users, implement CRUD operations, add authentication middleware, input validation, error handling, use proper HTTP methods and status codes, organize with Router.

### Challenge 2: Implement Authentication

**Approach:** User model with hashed passwords (bcrypt), registration endpoint, login endpoint generating JWT, authentication middleware verifying tokens, protected routes, password reset flow, token refresh mechanism.

### Challenge 3: Build a File Management API

**Approach:** Use multer for uploads, create endpoints for upload/download/list/delete, validate file types, store metadata in database, implement file serving, handle large files with streaming, security checks.

### Challenge 4: Create a Search API

**Approach:** Accept search query, implement filtering across fields, sorting, pagination, use database queries or array filtering, support fuzzy search, return formatted results with metadata.

### Challenge 5: Implement Rate Limiting

**Approach:** Use express-rate-limit or custom implementation, configure limits per route, implement sliding window algorithm, use Redis for distributed limiting, handle IP-based and user-based limiting, return appropriate headers.

---

## Debugging Scenarios - Solutions

### Scenario 1: Memory Leak

**Solution:** Use Node.js inspector (`--inspect`), take heap snapshots, identify growing objects, check for: unclosed connections, event listeners not removed, closures keeping references, global variable accumulation. Fix by removing listeners, closing connections, avoiding memory retention.

### Scenario 2: Slow API Response

**Solution:** Profile code, check database queries (add indexes, optimize), check for N+1 queries, implement caching, check middleware order, add logging to identify bottlenecks, use APM tools, optimize algorithms, check network latency, consider connection pooling.

### Scenario 3: Database Connection Issues

**Solution:** Check connection string, verify database is running, check connection pool settings, implement connection retry logic, check for connection leaks (not closing connections), monitor connection count, implement health checks, check firewall/network.

### Scenario 4: Authentication Not Working

**Solution:** Verify token generation, check token validation logic, verify middleware order, check token in headers (Authorization: Bearer token), verify secret key, check token expiration, verify user exists, check password hashing, test with logging.

### Scenario 5: CORS Errors

**Solution:** Verify CORS middleware is configured, check allowed origins, verify preflight requests (OPTIONS), check headers (Access-Control-Allow-Origin), ensure CORS middleware is before routes, test with different origins, check browser console for specific errors.

---

## Tips for Interview Success

1. **Explain concepts clearly** - Use simple language, avoid jargon
2. **Provide examples** - Show code examples when possible
3. **Think aloud** - Show your thought process
4. **Ask clarifying questions** - Understand requirements before solving
5. **Consider edge cases** - Think about error scenarios
6. **Discuss trade-offs** - Show you understand pros/cons
7. **Be honest** - Admit when you don't know something

---

**Good luck with your interviews!** Remember, understanding concepts deeply is more important than memorizing answers. Practice explaining these concepts in your own words.
