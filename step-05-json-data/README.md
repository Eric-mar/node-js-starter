# Step 5: JSON and Data Handling

In this step, you'll learn how to work with JSON data, handle request bodies, and manage data in your Express application. This is crucial for building APIs!

## Learning Objectives

By the end of this step, you will:

- Work with JSON data effectively
- Handle different types of request bodies
- Validate and sanitize input data
- Create data storage (in-memory for now)
- Implement CRUD operations with JSON
- Handle errors in data operations

## What You'll Build

You'll create a simple data management system that can:

- Store data in memory (as JavaScript objects/arrays)
- Create, Read, Update, Delete (CRUD) operations
- Handle JSON requests and responses
- Validate input data
- Return appropriate error messages

## Exercises

### Exercise 1: In-Memory Data Storage

**Task:** Create a simple in-memory data store for products.

**Instructions:**

1. Create an array to store products in memory
2. Each product should have: `id`, `name`, `price`, `description`
3. Initialize with a few sample products
4. Create a GET route `/api/products` that returns all products as JSON

**What to learn:**

- How to store data in memory (variables)
- Why this is temporary (data lost on restart)
- How to structure data objects

### Exercise 2: Creating Data (POST)

**Task:** Create an endpoint to add new products.

**Instructions:**

1. Create a POST route `/api/products`
2. Accept JSON data in the request body
3. Validate that required fields are present (`name`, `price`)
4. Generate a unique ID for the new product
5. Add the product to your array
6. Return the newly created product

**Think about:**

- How to generate unique IDs
- What validation is needed
- What status code to return (201 for created)

### Exercise 3: Reading Specific Data (GET by ID)

**Task:** Create an endpoint to get a single product by ID.

**Instructions:**

1. Create a GET route `/api/products/:id`
2. Find the product with the matching ID
3. Return the product if found
4. Return 404 error if not found
5. Handle the case where ID is not a valid number

**What to explore:**

- How to find items in arrays
- How to handle not found cases
- How to convert string IDs to numbers

### Exercise 4: Updating Data (PUT)

**Task:** Create an endpoint to update existing products.

**Instructions:**

1. Create a PUT route `/api/products/:id`
2. Find the product by ID
3. Update the product with data from request body
4. Return the updated product
5. Handle cases where product doesn't exist
6. Only update fields that are provided

**Important:**

- Don't overwrite the ID
- Validate the data before updating
- Return appropriate error messages

### Exercise 5: Deleting Data (DELETE)

**Task:** Create an endpoint to delete products.

**Instructions:**

1. Create a DELETE route `/api/products/:id`
2. Find the product by ID
3. Remove it from the array
4. Return a success message
5. Handle cases where product doesn't exist

**What to learn:**

- How to remove items from arrays
- Array methods like `findIndex()` and `splice()`

### Exercise 6: Data Validation Middleware

**Task:** Create reusable validation middleware.

**Instructions:**

1. Create a validation middleware function
2. Check for required fields
3. Validate data types (name is string, price is number)
4. Validate price is positive
5. Return clear error messages
6. Use this middleware in your POST and PUT routes

**Benefits:**

- Reusable validation logic
- Cleaner route handlers
- Consistent error messages

### Exercise 7: Search and Filter

**Task:** Add search and filter capabilities.

**Instructions:**

1. Modify GET `/api/products` to accept query parameters
2. Support filtering by:
   - Minimum price (`?minPrice=100`)
   - Maximum price (`?maxPrice=500`)
   - Name search (`?search=laptop`)
3. Return filtered results
4. If no filters, return all products

**Explore:**

- How to use `req.query` for query parameters
- Array methods like `filter()` and `includes()`

## Hints and Tips

### For Exercise 1: In-Memory Data Storage

- Create an array: `let products = []`
- Initialize with sample data
- Use `res.json()` to return the array
- Remember: this data is lost when server restarts

### For Exercise 2: Creating Data (POST)

- Access request body: `req.body`
- Generate ID: use array length or Date.now() or a counter
- Validate required fields exist
- Use `products.push()` to add to array
- Return status 201 (Created) with the new product

### For Exercise 3: Reading Specific Data

- Use `products.find(p => p.id === id)` to find product
- Convert ID from string to number: `parseInt(req.params.id)`
- Check if product exists before returning
- Return 404 if not found

### For Exercise 4: Updating Data

- Find product index: `findIndex()`
- Use spread operator to update: `{ ...product, ...req.body }`
- Don't allow ID to be updated
- Validate updated data
- Return 404 if product doesn't exist

### For Exercise 5: Deleting Data

- Find index: `products.findIndex(p => p.id === id)`
- Remove: `products.splice(index, 1)`
- Return success message
- Handle not found case

### For Exercise 6: Data Validation

- Check `req.body` for required fields
- Use `typeof` to check data types
- Validate price is number and positive
- Return error with `res.status(400).json({ error: 'message' })`
- Call `next()` only if validation passes

### For Exercise 7: Search and Filter

- Access query params: `req.query.minPrice`, `req.query.search`
- Use `products.filter()` to filter array
- Check if price is within range
- Use `.toLowerCase()` and `.includes()` for name search
- Return filtered array

## Testing Your API

1. **Test GET all products:**

   ```bash
   curl http://localhost:3000/api/products
   ```

2. **Test POST (create product):**

   ```bash
   curl -X POST http://localhost:3000/api/products \
     -H "Content-Type: application/json" \
     -d '{"name":"Laptop","price":999,"description":"Gaming laptop"}'
   ```

3. **Test GET by ID:**

   ```bash
   curl http://localhost:3000/api/products/1
   ```

4. **Test PUT (update):**

   ```bash
   curl -X PUT http://localhost:3000/api/products/1 \
     -H "Content-Type: application/json" \
     -d '{"price":1099}'
   ```

5. **Test DELETE:**

   ```bash
   curl -X DELETE http://localhost:3000/api/products/1
   ```

6. **Test filtering:**
   ```bash
   curl http://localhost:3000/api/products?minPrice=100&maxPrice=500
   ```

## Checklist

Before moving to Step 6, make sure you can:

- [ ] Store data in memory (arrays/objects)
- [ ] Create data with POST requests
- [ ] Read all data with GET requests
- [ ] Read specific data by ID
- [ ] Update data with PUT requests
- [ ] Delete data with DELETE requests
- [ ] Validate input data
- [ ] Handle errors appropriately
- [ ] Filter and search data

## Key Concepts

### CRUD Operations

- **Create** - POST request, add new item
- **Read** - GET request, retrieve data
- **Update** - PUT request, modify existing item
- **Delete** - DELETE request, remove item

### Data Storage (In-Memory)

- Arrays for collections
- Objects for individual items
- Lost when server restarts
- Good for learning, not for production

### Array Methods

- `find()` - Find item matching condition
- `findIndex()` - Find index of item
- `filter()` - Filter array by condition
- `push()` - Add item to array
- `splice()` - Remove item from array
- `map()` - Transform array items

### Validation

- Check required fields exist
- Validate data types
- Validate value ranges
- Return clear error messages

## Next Steps

Once you've completed all exercises and understand data handling, you're ready for:
**[Step 6: Project Structure](../step-06-project-structure/README.md)**

## Common Issues

**Issue:** `req.body` is undefined

- **Solution:** Make sure `express.json()` middleware is added

**Issue:** Data not persisting

- **Solution:** This is expected - in-memory data is temporary. We'll use databases later.

**Issue:** ID not found

- **Solution:** Check if ID is being converted to number correctly, and if product exists

**Issue:** Validation not working

- **Solution:** Make sure validation middleware runs before route handler

---
