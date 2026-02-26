# Create Product - JSON Examples

Complete JSON examples for creating products via POST `/api/products`

## Required Fields
- `name` (string) - Product name
- `price` (number) - Product price (must be >= 0)

## Optional Fields
- `description` (string) - Product description
- `category` (string) - Product category
- `inStock` (boolean) - Stock availability (default: `true`)
- `stockQuantity` (number) - Quantity in stock (default: `0`)

---

## Example 1: Basic Product (Minimum Required)

```json
{
  "name": "Smartphone",
  "price": 699.99
}
```

**cURL:**
```bash
curl -X POST http://localhost:3000/api/products \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Smartphone",
    "price": 699.99
  }'
```

---

## Example 2: Full Product Details

```json
{
  "name": "Gaming Laptop",
  "description": "High-end gaming laptop with RTX 4080, 32GB RAM, 1TB SSD",
  "price": 2499.99,
  "category": "Electronics",
  "inStock": true,
  "stockQuantity": 10
}
```

**cURL:**
```bash
curl -X POST http://localhost:3000/api/products \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Gaming Laptop",
    "description": "High-end gaming laptop with RTX 4080, 32GB RAM, 1TB SSD",
    "price": 2499.99,
    "category": "Electronics",
    "inStock": true,
    "stockQuantity": 10
  }'
```

---

## Example 3: Electronics Product

```json
{
  "name": "Wireless Headphones",
  "description": "Premium noise-cancelling wireless headphones with 30-hour battery",
  "price": 199.99,
  "category": "Electronics",
  "inStock": true,
  "stockQuantity": 50
}
```

---

## Example 4: Out of Stock Product

```json
{
  "name": "Limited Edition Watch",
  "description": "Premium limited edition smartwatch",
  "price": 599.99,
  "category": "Accessories",
  "inStock": false,
  "stockQuantity": 0
}
```

---

## Example 5: Product with Default Values

```json
{
  "name": "USB-C Cable",
  "description": "Fast charging USB-C cable, 2 meters length",
  "price": 19.99,
  "category": "Accessories"
}
```

*Note: `inStock` will default to `true` and `stockQuantity` will default to `0`*

---

## Example 6: Multiple Products (for testing)

### Product A
```json
{
  "name": "Laptop",
  "description": "High-performance laptop with 16GB RAM and 512GB SSD",
  "price": 999.99,
  "category": "Electronics",
  "inStock": true,
  "stockQuantity": 25
}
```

### Product B
```json
{
  "name": "Mechanical Keyboard",
  "description": "RGB mechanical keyboard with Cherry MX switches",
  "price": 149.99,
  "category": "Accessories",
  "inStock": true,
  "stockQuantity": 75
}
```

### Product C
```json
{
  "name": "4K Monitor",
  "description": "27-inch 4K UHD monitor with HDR support",
  "price": 399.99,
  "category": "Electronics",
  "inStock": true,
  "stockQuantity": 15
}
```

---

## JavaScript/Fetch Example

```javascript
// Create Product Function
async function createProduct(productData) {
  try {
    const response = await fetch('http://localhost:3000/api/products', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify(productData),
    });
    
    const result = await response.json();
    
    if (result.success) {
      console.log('Product created:', result.data);
      return result.data;
    } else {
      console.error('Error:', result.message);
      return null;
    }
  } catch (error) {
    console.error('Network error:', error);
    return null;
  }
}

// Usage
const newProduct = {
  name: "Laptop",
  description: "High-performance laptop",
  price: 999.99,
  category: "Electronics",
  inStock: true,
  stockQuantity: 25
};

createProduct(newProduct);
```

---

## Axios Example

```javascript
import axios from 'axios';

const createProduct = async (productData) => {
  try {
    const response = await axios.post(
      'http://localhost:3000/api/products',
      productData
    );
    return response.data;
  } catch (error) {
    console.error('Error creating product:', error.response?.data || error.message);
    throw error;
  }
};

// Usage
const product = {
  name: "Laptop",
  price: 999.99,
  description: "High-performance laptop",
  category: "Electronics"
};

createProduct(product);
```

---

## React Example

```javascript
import { useState } from 'react';

function CreateProductForm() {
  const [formData, setFormData] = useState({
    name: '',
    description: '',
    price: '',
    category: '',
    inStock: true,
    stockQuantity: 0
  });

  const handleSubmit = async (e) => {
    e.preventDefault();
    
    try {
      const response = await fetch('http://localhost:3000/api/products', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify({
          name: formData.name,
          description: formData.description,
          price: parseFloat(formData.price),
          category: formData.category,
          inStock: formData.inStock,
          stockQuantity: parseInt(formData.stockQuantity)
        }),
      });

      const result = await response.json();
      
      if (result.success) {
        alert('Product created successfully!');
        console.log('Created product:', result.data);
        // Reset form or redirect
      } else {
        alert('Error: ' + result.message);
      }
    } catch (error) {
      console.error('Error:', error);
      alert('Failed to create product');
    }
  };

  return (
    <form onSubmit={handleSubmit}>
      <input
        type="text"
        placeholder="Product Name *"
        value={formData.name}
        onChange={(e) => setFormData({...formData, name: e.target.value})}
        required
      />
      <input
        type="number"
        placeholder="Price *"
        value={formData.price}
        onChange={(e) => setFormData({...formData, price: e.target.value})}
        required
        min="0"
        step="0.01"
      />
      <textarea
        placeholder="Description"
        value={formData.description}
        onChange={(e) => setFormData({...formData, description: e.target.value})}
      />
      <input
        type="text"
        placeholder="Category"
        value={formData.category}
        onChange={(e) => setFormData({...formData, category: e.target.value})}
      />
      <button type="submit">Create Product</button>
    </form>
  );
}
```

---

## Expected Response

### Success Response (201 Created)
```json
{
  "success": true,
  "message": "Product created successfully",
  "data": {
    "_id": "64a1b2c3d4e5f6g7h8i9j0k1",
    "name": "Laptop",
    "description": "High-performance laptop with 16GB RAM and 512GB SSD",
    "price": 999.99,
    "category": "Electronics",
    "inStock": true,
    "stockQuantity": 25,
    "createdAt": "2024-01-15T10:30:00.000Z",
    "updatedAt": "2024-01-15T10:30:00.000Z"
  }
}
```

### Error Response (400 Bad Request)
```json
{
  "success": false,
  "message": "Name and price are required fields"
}
```

---

## Quick Copy-Paste JSON

Copy any of these for quick testing:

**Minimal:**
```json
{"name": "Test Product", "price": 99.99}
```

**Complete:**
```json
{"name": "Laptop", "description": "High-performance laptop", "price": 999.99, "category": "Electronics", "inStock": true, "stockQuantity": 25}
```
