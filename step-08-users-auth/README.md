# Step 8: Users and Authentication

Now let's add user management and authentication to your ecommerce backend. Users are essential for orders and personalization!

## Learning Objectives

By the end of this step, you will:

- Create a Users API with CRUD operations
- Implement basic authentication (simplified)
- Understand authentication concepts
- Create user registration and login
- Protect routes with authentication
- Handle user sessions/tokens

## What You'll Build

You'll create:

- Users API for managing user accounts
- User registration endpoint
- User login endpoint
- Authentication middleware
- Protected routes

## Exercises

### Exercise 1: User Data Model

**Task:** Define the user data structure.

**Instructions:**

1. In `src/data/users.js`, create an array to store users
2. Each user should have:
   - `id` (number) - Unique identifier
   - `username` (string) - Unique username
   - `email` (string) - Unique email address
   - `password` (string) - Hashed password (we'll keep it simple for now)
   - `firstName` (string) - User's first name
   - `lastName` (string) - User's last name
   - `role` (string) - User role: 'customer' or 'admin'
   - `createdAt` (date) - Account creation date
   - `updatedAt` (date) - Last update date
3. Initialize with 1-2 sample users

**Important:**

- For now, we'll store passwords in plain text (NOT secure, but for learning)
- In production, always hash passwords!

### Exercise 2: User Registration (POST)

**Task:** Create endpoint for user registration.

**Instructions:**

1. Create `registerUser` controller function
2. Create POST route `/api/users/register`
3. Validate required fields: `username`, `email`, `password`, `firstName`, `lastName`
4. Validate:
   - Username is unique
   - Email is unique and valid format
   - Password is at least 6 characters
   - All required fields are provided
5. Create new user with role 'customer' by default
6. Add timestamps
7. Return user data (without password!) with status 201

**Think about:**

- How to check if username/email already exists
- What information to return (never return password)
- How to validate email format

### Exercise 3: User Login (POST)

**Task:** Create endpoint for user login.

**Instructions:**

1. Create `loginUser` controller function
2. Create POST route `/api/users/login`
3. Accept `username` (or email) and `password`
4. Find user by username or email
5. Verify password matches
6. If valid, return user data (without password) with status 200
7. If invalid, return 401 (Unauthorized) with error message

**What to learn:**

- How to authenticate users
- How to handle failed login attempts
- What to return on successful login

### Exercise 4: Get All Users (GET)

**Task:** Create endpoint to get all users (admin only).

**Instructions:**

1. Create `getAllUsers` controller function
2. Create GET route `/api/users`
3. For now, return all users
4. Remove passwords from response
5. Later, we'll protect this with admin authentication

**Important:**

- Never return passwords in API responses
- Create a helper function to remove sensitive data

### Exercise 5: Get User by ID (GET)

**Task:** Create endpoint to get a single user.

**Instructions:**

1. Create `getUserById` controller function
2. Create GET route `/api/users/:id`
3. Find user by ID
4. Return user data (without password) if found
5. Return 404 if not found
6. Later, we'll add authorization (users can only see their own data)

### Exercise 6: Update User (PUT)

**Task:** Create endpoint to update user information.

**Instructions:**

1. Create `updateUser` controller function
2. Create PUT route `/api/users/:id`
3. Allow updating: `firstName`, `lastName`, `email`
4. Don't allow updating: `id`, `username`, `password` (separate endpoint for password)
5. Validate email format if provided
6. Validate email is unique if changed
7. Update `updatedAt` timestamp
8. Return updated user (without password)

**Think about:**

- Which fields should be updatable
- How to validate email uniqueness when updating
- How to handle partial updates

### Exercise 7: Authentication Middleware

**Task:** Create middleware to protect routes.

**Instructions:**

1. Create `authMiddleware.js` in appropriate folder
2. For now, use a simple token system:
   - On login, generate a simple token (could be user ID or random string)
   - Store tokens in memory (array or object)
   - Check token in middleware
3. Create middleware that:
   - Checks for token in request headers (`Authorization` header)
   - Validates token exists in stored tokens
   - Adds user info to `req.user` if valid
   - Returns 401 if invalid or missing
4. Apply middleware to protected routes

**Note:** This is a simplified authentication. In production, use JWT tokens or sessions.

### Exercise 8: Protect Routes

**Task:** Apply authentication to protected routes.

**Instructions:**

1. Protect these routes with authentication middleware:
   - GET `/api/users` - Get all users (admin only later)
   - GET `/api/users/:id` - Get user by ID
   - PUT `/api/users/:id` - Update user
2. For GET `/api/users/:id` and PUT `/api/users/:id`:
   - Users can only access their own data
   - Admins can access any user data
3. Test protected routes with and without tokens

## Hints and Tips

### For Exercise 1: User Data Model

- Store passwords as strings for now (in production, hash them!)
- Include role field for future authorization
- Use descriptive field names
- Initialize with test users for development

### For Exercise 2: User Registration

- Check uniqueness: `users.find(u => u.username === username)`
- Validate email format: use regex or simple string checks
- Set default role to 'customer'
- Never return password in response
- Generate unique ID

### For Exercise 3: User Login

- Accept username or email (check both)
- Compare passwords (plain text for now)
- Generate token on successful login
- Store token (in memory for now)
- Return token to client
- Return user data without password

### For Exercise 4: Get All Users

- Use `map()` to remove passwords from all users
- Create helper function: `removePassword(user)`
- Return array of users without passwords

### For Exercise 5: Get User by ID

- Find user by ID
- Remove password before returning
- Return 404 if not found
- Validate ID is number

### For Exercise 6: Update User

- Don't allow updating username, password, or ID
- Validate email uniqueness if email is being updated
- Use spread operator for partial updates
- Update `updatedAt` timestamp

### For Exercise 7: Authentication Middleware

- Check header: `req.headers['authorization']` or `req.headers.authorization`
- Token format: `Bearer <token>` or just `<token>`
- Extract token from header
- Check if token exists in stored tokens
- Add user to `req.user`
- Call `next()` if valid, return 401 if invalid

### For Exercise 8: Protect Routes

- Apply middleware: `router.get('/:id', authMiddleware, controller.getUserById)`
- Check `req.user.id === req.params.id` for same user
- Check `req.user.role === 'admin'` for admin access
- Return 403 (Forbidden) if user tries to access another user's data

## Testing Your Users API

1. **Register user:**

   ```bash
   curl -X POST http://localhost:3000/api/users/register \
     -H "Content-Type: application/json" \
     -d '{"username":"john","email":"john@example.com","password":"password123","firstName":"John","lastName":"Doe"}'
   ```

2. **Login:**

   ```bash
   curl -X POST http://localhost:3000/api/users/login \
     -H "Content-Type: application/json" \
     -d '{"username":"john","password":"password123"}'
   ```

3. **Get user (with token):**

   ```bash
   curl http://localhost:3000/api/users/1 \
     -H "Authorization: Bearer YOUR_TOKEN"
   ```

4. **Update user:**
   ```bash
   curl -X PUT http://localhost:3000/api/users/1 \
     -H "Content-Type: application/json" \
     -H "Authorization: Bearer YOUR_TOKEN" \
     -d '{"firstName":"Jane","lastName":"Smith"}'
   ```

## Checklist

Before moving to Step 9, make sure you can:

- [ ] Define user data model
- [ ] Register new users with validation
- [ ] Login users and return tokens
- [ ] Get all users (without passwords)
- [ ] Get user by ID
- [ ] Update user information
- [ ] Create authentication middleware
- [ ] Protect routes with authentication
- [ ] Handle authorization (users see own data)

## Key Concepts

### Authentication

- Verifying who a user is
- Usually done with username/email and password
- Returns a token or session on success

### Authorization

- Determining what a user can do
- Based on user roles and permissions
- Checks if user can access specific resources

### Tokens

- Simple authentication for learning (in-memory)
- In production, use JWT tokens
- Sent in Authorization header
- Validated on each protected request

### Password Security

- **Important:** In production, NEVER store plain text passwords
- Use libraries like `bcrypt` to hash passwords
- For now, we're keeping it simple for learning

## Security Notes

This implementation is simplified for learning:

- Passwords are stored in plain text (NOT secure!)
- Tokens are stored in memory (lost on restart)
- No password hashing (use bcrypt in production)
- No JWT tokens (use proper JWT in production)

For production, you must:

- Hash passwords with bcrypt
- Use JWT tokens or sessions
- Implement proper token storage
- Add rate limiting
- Add CSRF protection

## Next Steps

Once you've completed Users and Authentication, you're ready for:
**[Step 9: Orders API](../step-09-orders-api/README.md)**

## Common Issues

**Issue:** Token not working

- **Solution:** Check token format in header, verify token exists in stored tokens

**Issue:** Can't access protected routes

- **Solution:** Make sure token is sent in Authorization header, check middleware is applied

**Issue:** Password showing in response

- **Solution:** Create helper function to remove password from user objects before returning

---

