# Step 7: Products API

Now let's build the Products API for our ecommerce backend! This will be a complete CRUD API for managing products.

## Learning Objectives

By the end of this step, you will:

- Build a complete Products API
- Implement all CRUD operations for products
- Add proper validation
- Handle errors appropriately
- Return proper HTTP status codes
- Create a well-structured API

## What You'll Build

You'll create a Products API with these endpoints:

- `GET /api/products` - Get all products
- `GET /api/products/:id` - Get product by ID
- `POST /api/products` - Create new product
- `PUT /api/products/:id` - Update product
- `DELETE /api/products/:id` - Delete product

## Exercises

### Exercise 1: Product Data Model

**Task:** Define the product data structure.

**Instructions:**

1. In `src/data/products.js`, create an array to store products
2. Each product should have:
   - `id` (number) - Unique identifier
   - `name` (string) - Product name
   - `description` (string) - Product description
   - `price` (number) - Product price
   - `category` (string) - Product category
   - `stock` (number) - Available quantity
   - `image` (string) - Image URL (optional)
   - `createdAt` (date) - Creation timestamp
   - `updatedAt` (date) - Last update timestamp
3. Initialize with 3-5 sample products

**What to learn:**

- How to structure product data
- What fields are important for ecommerce
- How to initialize sample data

### Exercise 2: Get All Products (GET)

**Task:** Create endpoint to get all products.

**Instructions:**

1. In `src/controllers/productsController.js`, create `getAllProducts` function
2. In `src/routes/products.js`, create GET route `/`
3. Return all products with status 200
4. Add optional query parameters:
   - `category` - Filter by category
   - `minPrice` - Filter by minimum price
   - `maxPrice` - Filter by maximum price
   - `search` - Search by name/description

**Think about:**

- How to filter products based on query parameters
- How to return empty array if no products match
- Performance considerations (though small dataset for now)

### Exercise 3: Get Product by ID (GET)

**Task:** Create endpoint to get a single product.

**Instructions:**

1. Create `getProductById` controller function
2. Create GET route `/api/products/:id`
3. Find product by ID
4. Return product if found (200)
5. Return 404 if not found
6. Validate that ID is a valid number

**What to learn:**

- How to handle route parameters
- How to handle not found cases
- Proper error responses

### Exercise 4: Create Product (POST)

**Task:** Create endpoint to add new products.

**Instructions:**

1. Create `createProduct` controller function
2. Create POST route `/api/products`
3. Validate required fields: `name`, `price`, `category`, `stock`
4. Validate data types and values:
   - `name` must be non-empty string
   - `price` must be positive number
   - `category` must be non-empty string
   - `stock` must be non-negative number
5. Generate unique ID
6. Add `createdAt` and `updatedAt` timestamps
7. Add product to array
8. Return created product with status 201

**Important:**

- Validate all input data
- Return clear error messages
- Set appropriate timestamps

### Exercise 5: Update Product (PUT)

**Task:** Create endpoint to update existing products.

**Instructions:**

1. Create `updateProduct` controller function
2. Create PUT route `/api/products/:id`
3. Find product by ID
4. Validate that product exists (return 404 if not)
5. Validate updated data (same rules as create)
6. Update only provided fields (don't overwrite with undefined)
7. Update `updatedAt` timestamp
8. Don't allow ID to be changed
9. Return updated product with status 200

**Think about:**

- How to do partial updates (only update provided fields)
- How to preserve existing data
- How to validate partial updates

### Exercise 6: Delete Product (DELETE)

**Task:** Create endpoint to delete products.

**Instructions:**

1. Create `deleteProduct` controller function
2. Create DELETE route `/api/products/:id`
3. Find product by ID
4. Return 404 if product doesn't exist
5. Remove product from array
6. Return success message with status 200
7. Optionally return deleted product data

**What to learn:**

- How to safely delete data
- How to confirm deletion
- What to return after deletion

### Exercise 7: Validation Middleware

**Task:** Create reusable validation middleware for products.

**Instructions:**

1. Create validation middleware function
2. Check required fields for POST requests
3. Validate data types and constraints
4. Return detailed error messages
5. Use middleware in POST and PUT routes
6. Make middleware flexible for partial updates (PUT)

**Benefits:**

- Reusable validation logic
- Consistent error messages
- Cleaner controller code

### Exercise 8: Error Handling

**Task:** Improve error handling for products API.

**Instructions:**

1. Create consistent error response format:
   ```json
   {
     "error": "Error message",
     "details": "Additional details"
   }
   ```
2. Handle different error types:
   - Validation errors (400)
   - Not found (404)
   - Server errors (500)
3. Add try-catch blocks in controllers
4. Return appropriate status codes

## Hints and Tips

### For Exercise 1: Product Data Model

- Use descriptive field names
- Include timestamps for tracking
- Consider what fields are essential for ecommerce
- Sample products help with testing

### For Exercise 2: Get All Products

- Use `req.query` to access query parameters
- Use array `filter()` method for filtering
- Return empty array if no matches
- Consider case-insensitive search

### For Exercise 3: Get Product by ID

- Convert `req.params.id` to number: `parseInt()` or `Number()`
- Use `find()` to locate product
- Return 404 with error message if not found
- Validate ID is valid number before searching

### For Exercise 4: Create Product

- Validate all required fields exist
- Check data types: `typeof name === 'string'`
- Validate constraints: `price > 0`, `stock >= 0`
- Generate ID: could use array length, Date.now(), or counter
- Use `new Date()` for timestamps

### For Exercise 5: Update Product

- Use spread operator: `{ ...existingProduct, ...updates }`
- Don't allow ID to be updated
- Only update fields that are provided
- Validate updated data follows same rules
- Update `updatedAt` timestamp

### For Exercise 6: Delete Product

- Find product first to confirm it exists
- Use `findIndex()` and `splice()` to remove
- Return 404 if product doesn't exist
- Return success message or deleted product

### For Exercise 7: Validation Middleware

- Create function that takes validation rules
- Check required fields exist
- Validate each field according to rules
- Return error response if validation fails
- Call `next()` if validation passes
- For PUT, make some fields optional

### For Exercise 8: Error Handling

- Use consistent error format
- Include helpful error messages
- Set appropriate status codes
- Log errors for debugging
- Don't expose internal errors to users

## Testing Your Products API

Test all endpoints:

1. **GET all products:**

   ```bash
   curl http://localhost:3000/api/products
   ```

2. **GET with filters:**

   ```bash
   curl http://localhost:3000/api/products?category=electronics&minPrice=100
   ```

3. **GET by ID:**

   ```bash
   curl http://localhost:3000/api/products/1
   ```

4. **POST (create):**

   ```bash
   curl -X POST http://localhost:3000/api/products \
     -H "Content-Type: application/json" \
     -d '{"name":"iPhone","price":999,"category":"electronics","stock":50,"description":"Latest iPhone"}'
   ```

5. **PUT (update):**

   ```bash
   curl -X PUT http://localhost:3000/api/products/1 \
     -H "Content-Type: application/json" \
     -d '{"price":1099,"stock":45}'
   ```

6. **DELETE:**
   ```bash
   curl -X DELETE http://localhost:3000/api/products/1
   ```

## Checklist

Before moving to Step 8, make sure you can:

- [ ] Define product data model
- [ ] Get all products with filtering
- [ ] Get product by ID
- [ ] Create new products with validation
- [ ] Update existing products
- [ ] Delete products
- [ ] Validate input data
- [ ] Handle errors properly
- [ ] Return appropriate status codes

## Key Concepts

### RESTful API Design

- GET - Retrieve data
- POST - Create new resource
- PUT - Update existing resource
- DELETE - Remove resource
- Use proper HTTP methods and status codes

### Data Validation

- Validate required fields
- Check data types
- Validate constraints (positive numbers, etc.)
- Return clear error messages

### Error Handling

- Consistent error format
- Appropriate status codes
- Helpful error messages
- Don't expose internal details

### Query Parameters

- Use for filtering and searching
- Optional parameters
- Multiple parameters can be combined
- Access via `req.query`

## Next Steps

Once you've completed the Products API, you're ready for:
**[Step 8: Users and Authentication](../step-08-users-auth/README.md)**

## Common Issues

**Issue:** Validation not catching errors

- **Solution:** Check validation logic and ensure middleware runs before route handler

**Issue:** ID not found

- **Solution:** Verify ID is converted to number and product exists in array

**Issue:** Update overwrites all fields

- **Solution:** Use spread operator to merge existing and new data, only include provided fields

---

