# Step 9: Orders API

Now let's build the Orders API! Orders connect products and users, making this the core of our ecommerce backend.

## Learning Objectives

By the end of this step, you will:

- Create a complete Orders API
- Understand relationships between data (products, users, orders)
- Implement order creation with product validation
- Calculate order totals
- Handle order status
- Implement order history

## What You'll Build

You'll create an Orders API with:

- Create orders with products
- Get all orders (with filtering)
- Get order by ID
- Get user's orders
- Update order status
- Calculate order totals

## Exercises

### Exercise 1: Order Data Model

**Task:** Define the order data structure.

**Instructions:**

1. In `src/data/orders.js`, create an array to store orders
2. Each order should have:
   - `id` (number) - Unique identifier
   - `userId` (number) - ID of user who placed the order
   - `items` (array) - Array of order items, each with:
     - `productId` (number) - Product ID
     - `quantity` (number) - Quantity ordered
     - `price` (number) - Price at time of order
     - `name` (string) - Product name at time of order
   - `total` (number) - Total order amount
   - `status` (string) - Order status: 'pending', 'processing', 'shipped', 'delivered', 'cancelled'
   - `shippingAddress` (object) - Shipping address:
     - `street`, `city`, `state`, `zipCode`, `country`
   - `createdAt` (date) - Order creation date
   - `updatedAt` (date) - Last update date
3. Initialize with 1-2 sample orders

**What to learn:**

- How to structure nested data
- How to store order items
- Why we store product details (price, name) in order

### Exercise 2: Create Order (POST)

**Task:** Create endpoint to place new orders.

**Instructions:**

1. Create `createOrder` controller function
2. Create POST route `/api/orders` (protected - requires authentication)
3. Validate required fields:
   - `items` - Array of order items
   - `shippingAddress` - Shipping address object
4. For each item in `items`:
   - Validate `productId` and `quantity` exist
   - Find product by ID
   - Verify product exists and has sufficient stock
   - Store product details (name, price) in order item
   - Calculate item total (price × quantity)
5. Calculate order total (sum of all item totals)
6. Create order with status 'pending'
7. Reduce product stock (update products array)
8. Return created order with status 201

**Important:**

- Verify products exist before creating order
- Check stock availability
- Store product snapshot (price/name) in order
- Update product stock
- Get userId from authenticated user (`req.user`)

### Exercise 3: Get All Orders (GET)

**Task:** Create endpoint to get all orders (admin only).

**Instructions:**

1. Create `getAllOrders` controller function
2. Create GET route `/api/orders` (protected, admin only)
3. Support query parameters:
   - `status` - Filter by status
   - `userId` - Filter by user ID
   - `minTotal` - Filter by minimum total
   - `maxTotal` - Filter by maximum total
4. Return all matching orders
5. Include user information if possible

**Think about:**

- How to filter orders
- What information to include
- How to handle admin-only access

### Exercise 4: Get Order by ID (GET)

**Task:** Create endpoint to get a single order.

**Instructions:**

1. Create `getOrderById` controller function
2. Create GET route `/api/orders/:id` (protected)
3. Find order by ID
4. Authorization:
   - Users can only see their own orders
   - Admins can see any order
5. Return order if found and authorized
6. Return 404 if not found
7. Return 403 if user tries to access another user's order

**What to learn:**

- How to check ownership
- How to handle authorization
- What information to return

### Exercise 5: Get User's Orders (GET)

**Task:** Create endpoint to get orders for authenticated user.

**Instructions:**

1. Create `getUserOrders` controller function
2. Create GET route `/api/orders/my-orders` (protected)
3. Get userId from authenticated user (`req.user.id`)
4. Filter orders by userId
5. Support optional query parameters:
   - `status` - Filter by status
6. Return user's orders

**Benefits:**

- Users can see their order history
- Easy to filter by status
- Better UX than getting all orders

### Exercise 6: Update Order Status (PUT)

**Task:** Create endpoint to update order status.

**Instructions:**

1. Create `updateOrderStatus` controller function
2. Create PUT route `/api/orders/:id/status` (protected, admin only)
3. Accept new `status` in request body
4. Validate status is one of: 'pending', 'processing', 'shipped', 'delivered', 'cancelled'
5. Find order by ID
6. Update order status
7. Update `updatedAt` timestamp
8. If status is 'cancelled', restore product stock
9. Return updated order

**Important:**

- Only admins can update order status
- Validate status values
- Handle stock restoration on cancellation
- Update timestamps

### Exercise 7: Order Calculation Helper

**Task:** Create helper functions for order calculations.

**Instructions:**

1. Create helper functions in a separate file or in controller:
   - `calculateItemTotal(item)` - Calculate total for one item
   - `calculateOrderTotal(items)` - Calculate total for all items
   - `validateStock(product, quantity)` - Check if product has enough stock
2. Use these helpers in order creation
3. Make code more maintainable and testable

**Benefits:**

- Reusable calculation logic
- Easier to test
- Cleaner controller code

### Exercise 8: Order Validation

**Task:** Create comprehensive validation for orders.

**Instructions:**

1. Create validation middleware or function for orders
2. Validate:
   - `items` array is not empty
   - Each item has `productId` and `quantity`
   - `quantity` is positive number
   - `shippingAddress` has all required fields
   - All products in items exist
   - All products have sufficient stock
3. Return detailed error messages
4. Use in order creation endpoint

## Hints and Tips

### For Exercise 1: Order Data Model

- Store product details in order (price, name) because products can change
- This preserves order history accurately
- Use nested objects for complex data
- Include all necessary shipping information

### For Exercise 2: Create Order

- Get userId from `req.user.id` (from authentication middleware)
- Loop through items array
- For each item:
  - Find product: `products.find(p => p.id === productId)`
  - Check stock: `product.stock >= quantity`
  - Store product snapshot in order item
- Calculate totals
- Update product stock: `product.stock -= quantity`

### For Exercise 3: Get All Orders

- Filter orders array based on query parameters
- Use `filter()` method
- Check multiple conditions
- Return empty array if no matches

### For Exercise 4: Get Order by ID

- Find order: `orders.find(o => o.id === orderId)`
- Check ownership: `order.userId === req.user.id`
- Check admin: `req.user.role === 'admin'`
- Return 403 if unauthorized, 404 if not found

### For Exercise 5: Get User's Orders

- Filter: `orders.filter(o => o.userId === req.user.id)`
- Apply additional filters if provided
- Return array of orders

### For Exercise 6: Update Order Status

- Valid statuses: create array of valid values
- Check: `validStatuses.includes(newStatus)`
- Find order and update status
- If cancelled, loop through items and restore stock:
  - Find product and increase stock: `product.stock += item.quantity`

### For Exercise 7: Order Calculation Helper

- `calculateItemTotal`: `item.price * item.quantity`
- `calculateOrderTotal`: sum all item totals
- Use `reduce()` for summing: `items.reduce((sum, item) => sum + calculateItemTotal(item), 0)`

### For Exercise 8: Order Validation

- Validate items array: `Array.isArray(items) && items.length > 0`
- Validate each item structure
- Check products exist: `products.find(p => p.id === productId)`
- Check stock availability
- Validate address object structure

## Testing Your Orders API

1. **Create order (with auth token):**

   ```bash
   curl -X POST http://localhost:3000/api/orders \
     -H "Content-Type: application/json" \
     -H "Authorization: Bearer YOUR_TOKEN" \
     -d '{
       "items": [
         {"productId": 1, "quantity": 2},
         {"productId": 2, "quantity": 1}
       ],
       "shippingAddress": {
         "street": "123 Main St",
         "city": "New York",
         "state": "NY",
         "zipCode": "10001",
         "country": "USA"
       }
     }'
   ```

2. **Get user's orders:**

   ```bash
   curl http://localhost:3000/api/orders/my-orders \
     -H "Authorization: Bearer YOUR_TOKEN"
   ```

3. **Get order by ID:**

   ```bash
   curl http://localhost:3000/api/orders/1 \
     -H "Authorization: Bearer YOUR_TOKEN"
   ```

4. **Update order status (admin):**
   ```bash
   curl -X PUT http://localhost:3000/api/orders/1/status \
     -H "Content-Type: application/json" \
     -H "Authorization: Bearer ADMIN_TOKEN" \
     -d '{"status": "shipped"}'
   ```

## Checklist

Before moving to Step 10, make sure you can:

- [ ] Define order data model with items
- [ ] Create orders with product validation
- [ ] Calculate order totals
- [ ] Update product stock when order is created
- [ ] Get all orders with filtering (admin)
- [ ] Get order by ID with authorization
- [ ] Get user's orders
- [ ] Update order status (admin)
- [ ] Restore stock on cancellation
- [ ] Validate order data

## Key Concepts

### Data Relationships

- Orders belong to users (userId)
- Orders contain products (items array)
- Store product snapshot in order (historical data)

### Order Lifecycle

- pending → processing → shipped → delivered
- Can be cancelled at any time
- Status changes should be tracked

### Stock Management

- Reduce stock when order is created
- Restore stock when order is cancelled
- Always check stock before creating order

### Authorization

- Users can see their own orders
- Admins can see all orders and update status
- Check ownership before returning data

## Next Steps

Once you've completed the Orders API, you're ready for:
**[Step 10: Complete Integration](../step-10-complete-backend/README.md)**

## Common Issues

**Issue:** Stock not updating

- **Solution:** Make sure you're updating the product in the products array, not just the order

**Issue:** Order total incorrect

- **Solution:** Double-check calculation logic, verify prices are numbers

**Issue:** Can't access other user's orders

- **Solution:** This is correct behavior - users should only see their own orders (unless admin)

---
