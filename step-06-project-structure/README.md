# Step 6: Project Structure

Now that you understand Express basics, let's organize your code into a proper project structure. Good organization makes your code maintainable and scalable!

## Learning Objectives

By the end of this step, you will:

- Understand how to structure a Node.js/Express project
- Organize routes into separate files
- Create reusable controllers
- Set up proper project folders
- Understand separation of concerns
- Prepare for building the ecommerce backend

## What is Project Structure?

Project structure is how you organize your files and folders. A good structure makes it easy to:

- Find code quickly
- Maintain and update code
- Add new features
- Collaborate with others
- Scale your application

## Recommended Project Structure

For our ecommerce backend, we'll use this structure:

```
ecommerce-backend/
├── src/
│   ├── routes/
│   │   ├── products.js
│   │   ├── users.js
│   │   └── orders.js
│   ├── controllers/
│   │   ├── productsController.js
│   │   ├── usersController.js
│   │   └── ordersController.js
│   ├── data/
│   │   ├── products.js
│   │   ├── users.js
│   │   └── orders.js
│   └── app.js
├── package.json
└── README.md
```

## Exercises

### Exercise 1: Create Project Structure

**Task:** Set up the folder structure for your ecommerce backend.

**Instructions:**

1. Create a new folder `ecommerce-backend` (or use your project root)
2. Create these folders:
   - `src/` - Source code folder
   - `src/routes/` - Route definitions
   - `src/controllers/` - Business logic
   - `src/data/` - Data storage (in-memory for now)
3. Create an `app.js` file in the `src/` folder
4. Move your existing Express code to this new structure

**What to learn:**

- How folders organize code
- Why separation of concerns matters

### Exercise 2: Organize Routes

**Task:** Separate routes into different files.

**Instructions:**

1. In `src/routes/`, create:
   - `products.js` - All product-related routes
   - `users.js` - All user-related routes
   - `orders.js` - All order-related routes
2. Use `express.Router()` in each file
3. Define routes in each file
4. Export the routers
5. Import and use them in `app.js`

**Benefits:**

- Each file has a single responsibility
- Easy to find specific routes
- Easier to maintain

### Exercise 3: Create Controllers

**Task:** Move business logic to controller files.

**Instructions:**

1. In `src/controllers/`, create:
   - `productsController.js` - Product business logic
   - `usersController.js` - User business logic
   - `ordersController.js` - Order business logic
2. Move your route handler logic to controllers
3. Export controller functions
4. Import and use them in route files

**Structure:**

- Routes handle HTTP requests/responses
- Controllers contain business logic
- Routes call controller functions

### Exercise 4: Organize Data

**Task:** Separate data storage into data files.

**Instructions:**

1. In `src/data/`, create:
   - `products.js` - Product data and storage operations
   - `users.js` - User data and storage operations
   - `orders.js` - Order data and storage operations
2. Create functions for data operations:
   - `getAll()`, `getById()`, `create()`, `update()`, `delete()`
3. Export these functions
4. Use them in controllers

**What to learn:**

- Data layer separation
- Reusable data operations
- Easier to switch to database later

### Exercise 5: Set Up Main App File

**Task:** Create a clean main application file.

**Instructions:**

1. In `src/app.js`, set up:
   - Express app initialization
   - Middleware (JSON parsing, etc.)
   - Route imports and mounting
   - Error handling middleware
   - Server startup
2. Keep it clean and organized
3. Add comments explaining each section

**Goal:**

- `app.js` should be the entry point
- Easy to see overall app structure
- All middleware and routes in one place

### Exercise 6: Add Environment Configuration

**Task:** Set up environment variables.

**Instructions:**

1. Create a `.env` file (you'll need `dotenv` package: `npm install dotenv`)
2. Move port number to environment variable
3. Add other configuration (e.g., API keys, database URLs)
4. Use `process.env` to access variables
5. Load `.env` file using `dotenv` at the start of `app.js`

**Benefits:**

- Sensitive data not in code
- Easy to change configuration
- Different configs for dev/prod

## Hints and Tips

### For Exercise 1: Create Project Structure

- Create folders: `mkdir -p src/routes src/controllers src/data` (or create manually)
- Move your existing code to the new structure
- Update require paths accordingly

### For Exercise 2: Organize Routes

- Each route file: `const router = express.Router()`
- Define routes: `router.get('/path', handler)`
- Export: `module.exports = router`
- In app.js: `app.use('/api/products', require('./routes/products'))`

### For Exercise 3: Create Controllers

- Export functions: `exports.getAllProducts = (req, res) => { ... }`
- Or: `module.exports = { getAllProducts, getProductById, ... }`
- In routes: `const controller = require('../controllers/productsController')`
- Use: `router.get('/', controller.getAllProducts)`

### For Exercise 4: Organize Data

- Create data arrays: `let products = []`
- Export functions: `exports.getAll = () => products`
- Export functions: `exports.create = (product) => { ... }`
- In controllers: `const data = require('../data/products')`
- Use: `const products = data.getAll()`

### For Exercise 5: Set Up Main App File

- Structure should be:
  1. Imports
  2. App initialization
  3. Middleware
  4. Routes
  5. Error handling
  6. Server start

### For Exercise 6: Environment Configuration

- Install: `npm install dotenv`
- At top of app.js: `require('dotenv').config()`
- Use: `const PORT = process.env.PORT || 3000`
- Create `.env` file with: `PORT=3000`

## File Structure Example

### `src/app.js`

```
- Require dotenv
- Require express
- Require routes
- Create app
- Add middleware
- Mount routes
- Error handling
- Start server
```

### `src/routes/products.js`

```
- Require express.Router
- Require controller
- Define routes
- Export router
```

### `src/controllers/productsController.js`

```
- Require data module
- Create controller functions
- Export functions
```

### `src/data/products.js`

```
- Data storage (array)
- Data operation functions
- Export functions
```

## Checklist

Before moving to Step 7, make sure you can:

- [ ] Create proper folder structure
- [ ] Separate routes into different files
- [ ] Create and use controllers
- [ ] Organize data operations
- [ ] Set up main app file cleanly
- [ ] Use environment variables
- [ ] Understand separation of concerns

## Key Concepts

### Separation of Concerns

- **Routes** - Handle HTTP requests/responses
- **Controllers** - Business logic
- **Data** - Data storage and operations
- Each layer has a specific responsibility

### Project Organization

- Group related files together
- Use folders to organize
- Keep files focused and small
- Easy to navigate and find code

### Module Exports

- `module.exports` - Export single value
- `exports.functionName` - Export multiple functions
- `require()` - Import modules

### Environment Variables

- Store configuration outside code
- Use `.env` file for local development
- Access with `process.env.VARIABLE_NAME`
- Never commit `.env` to git (add to `.gitignore`)

## Next Steps

Once you've organized your project structure, you're ready for:
**[Step 7: Products API](../step-07-products-api/README.md)**

## Common Issues

**Issue:** Cannot find module

- **Solution:** Check file paths in require statements, use relative paths correctly (`./` or `../`)

**Issue:** Routes not working

- **Solution:** Make sure routes are mounted correctly in app.js with `app.use()`

**Issue:** Controller functions not defined

- **Solution:** Check exports in controller files and imports in route files

**Issue:** Environment variables not loading

- **Solution:** Make sure `dotenv` is required at the very top of app.js

---

