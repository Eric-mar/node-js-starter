# Node.js & Express.js Interview Questions - Practice Set

This document contains practice interview questions organized by difficulty level. Use these to test your knowledge and prepare for technical interviews.

---

## Difficulty Levels

- **Beginner**: Fundamental concepts
- **Intermediate**: Practical application
- **Advanced**: Complex scenarios and optimization

---

## Beginner Level Questions

### 1. What is Node.js and what problem does it solve?

### 2. Explain the difference between JavaScript in the browser and Node.js.

### 3. What is npm and what is it used for?

### 4. What is the difference between `var`, `let`, and `const`?

### 5. What is `module.exports` and how do you use it?

### 6. What is the difference between `require()` and `import`?

### 7. What is Express.js and why would you use it instead of plain Node.js?

### 8. What is middleware in Express.js?

### 9. How do you create a route in Express?

### 10. What is the difference between `app.get()` and `app.use()`?

### 11. How do you send JSON responses in Express?

### 12. What is `req.params` used for?

### 13. What is `req.query` used for?

### 14. What is `req.body` and how do you access it?

### 15. What is a callback function?

### 16. What is a Promise?

### 17. What is async/await?

### 18. What are HTTP status codes? Give examples.

### 19. What is REST and what makes an API RESTful?

### 20. What is the difference between GET and POST requests?

---

## Intermediate Level Questions

### 21. Explain the Node.js event loop. How does it work?

### 22. What is the difference between blocking and non-blocking code?

### 23. How do you handle errors in Express applications?

### 24. What is the order of middleware execution in Express?

### 25. How do you structure a Node.js/Express project?

### 26. What are environment variables and why use them?

### 27. How do you implement authentication in an Express app?

### 28. What is JWT and how does it work?

### 29. Why should you never store passwords in plain text?

### 30. What is CORS and how do you handle it in Express?

### 31. What is the difference between authentication and authorization?

### 32. How do you validate input data in Express?

### 33. What is the difference between PUT and PATCH?

### 34. How do you organize routes in Express?

### 35. What is Express Router and when should you use it?

### 36. How do you handle file uploads in Express?

### 37. What is rate limiting and why is it important?

### 38. How do you implement pagination in an API?

### 39. What is the difference between `req.params`, `req.query`, and `req.body`?

### 40. How do you handle async errors in Express?

### 41. What is separation of concerns in backend development?

### 42. How do you implement search functionality in an API?

### 43. What is the purpose of `process.env` in Node.js?

### 44. How do you test Express APIs?

### 45. What is input validation and why is it important?

### 46. How do you implement error handling middleware?

### 47. What is the difference between `throw` and `next(error)`?

### 48. How do you create a CRUD API in Express?

### 49. What is the difference between SQL and NoSQL databases?

### 50. What security best practices should you follow in Express?

---

## Advanced Level Questions

### 51. Explain the Node.js event loop phases in detail.

### 52. How do you implement database transactions in Node.js?

### 53. What is connection pooling and why is it important?

### 54. How do you optimize Node.js application performance?

### 55. What is the difference between `process.nextTick()` and `setImmediate()`?

### 56. How do you handle memory leaks in Node.js applications?

### 57. What is the cluster module in Node.js and when would you use it?

### 58. How do you implement caching in a Node.js application?

### 59. What is the difference between child_process and worker_threads?

### 60. How do you implement real-time features (WebSockets) in Express?

### 61. How do you handle database migrations in Node.js?

### 62. What is the difference between an ORM and ODM?

### 63. How do you implement microservices architecture with Node.js?

### 64. How do you handle distributed transactions?

### 65. What is the purpose of message queues and when would you use them?

### 66. How do you implement API versioning?

### 67. How do you handle large file uploads in Node.js?

### 68. What is the difference between horizontal and vertical scaling?

### 69. How do you implement observability (logging, monitoring, tracing) in Node.js?

### 70. How do you secure an Express API against common vulnerabilities?

### 71. How do you implement GraphQL in Node.js?

### 72. What is the difference between server-side rendering and API-based architecture?

### 73. How do you implement rate limiting with different strategies?

### 74. How do you handle graceful shutdown in Node.js applications?

### 75. What is the difference between event-driven and request-response architectures?

---

## Scenario-Based Questions

### 76. How would you design an ecommerce API with products, users, and orders?

### 77. How would you implement a social media API with posts, comments, and likes?

### 78. How would you build a real-time chat application backend?

### 79. How would you design a file upload service with progress tracking?

### 80. How would you implement a notification system?

### 81. How would you build a search API that can handle millions of records?

### 82. How would you implement a payment processing system?

### 83. How would you design a multi-tenant SaaS application backend?

### 84. How would you implement a recommendation engine API?

### 85. How would you build a scalable image processing service?

---

## Coding Challenges

### Challenge 1: Create a RESTful API

Build a complete RESTful API for a blog with:

- Posts (CRUD operations)
- Comments (CRUD operations)
- Users (registration, login)
- Authentication middleware
- Input validation
- Error handling

### Challenge 2: Implement Authentication

Create a complete authentication system with:

- User registration
- User login
- JWT token generation
- Protected routes
- Password hashing
- Token refresh

### Challenge 3: Build a File Management API

Create an API for file management with:

- File upload
- File download
- File listing
- File deletion
- File metadata
- File type validation

### Challenge 4: Create a Search API

Build a search API that can:

- Search across multiple fields
- Filter results
- Sort results
- Paginate results
- Handle fuzzy search

### Challenge 5: Implement Rate Limiting

Create a rate limiting system with:

- Different limits for different routes
- IP-based limiting
- User-based limiting
- Sliding window algorithm
- Redis-based storage

---

## Debugging Scenarios

### Scenario 1: Memory Leak

Your Node.js application's memory keeps increasing. How do you identify and fix it?

### Scenario 2: Slow API Response

Your API is responding slowly. What steps do you take to diagnose and fix it?

### Scenario 3: Database Connection Issues

Your application is losing database connections. How do you troubleshoot?

### Scenario 4: Authentication Not Working

Users can't log in. What do you check?

### Scenario 5: CORS Errors

Your frontend can't call your API. How do you fix CORS issues?

---

## Practice Tips

1. **Answer Out Loud**: Practice explaining concepts verbally
2. **Write Code**: Don't just explain, show code examples
3. **Think Aloud**: Show your thought process during coding challenges
4. **Ask Questions**: Clarify requirements before solving
5. **Consider Edge Cases**: Think about error scenarios
6. **Optimize**: Consider performance implications
7. **Review**: Review your solutions and improve them

---

## Solutions

For detailed answers to all these questions, see **[INTERVIEW_QUESTIONS_SOLUTIONS.md](./INTERVIEW_QUESTIONS_SOLUTIONS.md)**

This solutions file contains brief, comprehensive answers to all 85 questions plus coding challenges and debugging scenarios.
