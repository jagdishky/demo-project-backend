# ✅ CORRECT JSON Format for Creating Products

## ❌ WRONG - What you're sending:
```json
{
  "createProduct": {
    "name": "Smartphone",
    "request": {
      "body": {
        "name": "Laptop",
        "price": 999.99
      }
    }
  }
}
```

## ✅ CORRECT - What you should send:

### Option 1: Minimal (Required Fields Only)
```json
{
  "name": "Smartphone",
  "price": 699.99
}
```

### Option 2: With Description
```json
{
  "name": "Smartphone",
  "price": 699.99,
  "description": "Latest smartphone with 128GB storage"
}
```

### Option 3: Complete Product
```json
{
  "name": "Smartphone",
  "price": 699.99,
  "description": "Latest smartphone with 128GB storage and triple camera",
  "category": "Electronics",
  "inStock": true,
  "stockQuantity": 50
}
```

---

## How to Use in Postman:

1. **Method:** POST
2. **URL:** `http://localhost:3000/api/products`
3. **Headers:** 
   - Key: `Content-Type`
   - Value: `application/json`
4. **Body:** Select "raw" and "JSON", then paste ONLY the product object:

```json
{
  "name": "Smartphone",
  "price": 699.99,
  "description": "Latest smartphone",
  "category": "Electronics"
}
```

---

## How to Use in JavaScript/Fetch:

```javascript
// ✅ CORRECT
const productData = {
  name: "Smartphone",
  price: 699.99,
  description: "Latest smartphone",
  category: "Electronics"
};

fetch('http://localhost:3000/api/products', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify(productData)  // Send productData directly
});
```

---

## Common Errors:

### Error 1: Nested Structure
❌ **Wrong:**
```json
{
  "createProduct": {
    "body": {
      "name": "Product",
      "price": 100
    }
  }
}
```

✅ **Correct:**
```json
{
  "name": "Product",
  "price": 100
}
```

### Error 2: Missing Required Fields
❌ **Wrong:**
```json
{
  "description": "Product description"
}
```

✅ **Correct:**
```json
{
  "name": "Product",
  "price": 100
}
```

### Error 3: Price as String
❌ **Wrong:**
```json
{
  "name": "Product",
  "price": "2000"  // String instead of number
}
```

✅ **Correct:**
```json
{
  "name": "Product",
  "price": 2000  // Number
}
```

---

## Quick Test Examples:

### Example 1: Basic Product
```json
{
  "name": "Laptop",
  "price": 999.99
}
```

### Example 2: Full Details
```json
{
  "name": "Gaming Laptop",
  "description": "High-end gaming laptop with RTX 4080",
  "price": 2499.99,
  "category": "Electronics",
  "inStock": true,
  "stockQuantity": 10
}
```

### Example 3: Accessories
```json
{
  "name": "USB-C Cable",
  "description": "Fast charging cable",
  "price": 19.99,
  "category": "Accessories"
}
```

---

## Expected Response:

### Success (201 Created):
```json
{
  "success": true,
  "message": "Product created successfully",
  "data": {
    "_id": "64a1b2c3d4e5f6g7h8i9j0k1",
    "name": "Smartphone",
    "price": 699.99,
    "description": "Latest smartphone",
    "category": "Electronics",
    "inStock": true,
    "stockQuantity": 0,
    "createdAt": "2024-01-15T10:30:00.000Z",
    "updatedAt": "2024-01-15T10:30:00.000Z"
  }
}
```

### Error (400 Bad Request):
```json
{
  "success": false,
  "message": "Name and price are required fields"
}
```
