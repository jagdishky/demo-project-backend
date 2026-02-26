# Products API Documentation

Complete API documentation for frontend integration.

## Base URL

```
Local: http://localhost:3000
Production: https://your-api-domain.com
```

## Endpoints

### 1. Create Product

**POST** `/api/products`

Create a new product in the database.

**Request Body:**
```json
{
  "name": "Laptop",                    // Required
  "description": "High-performance laptop",
  "price": 999.99,                     // Required
  "category": "Electronics",
  "inStock": true,
  "stockQuantity": 25
}
```

**Response (201 Created):**
```json
{
  "success": true,
  "message": "Product created successfully",
  "data": {
    "_id": "64a1b2c3d4e5f6g7h8i9j0k1",
    "name": "Laptop",
    "description": "High-performance laptop",
    "price": 999.99,
    "category": "Electronics",
    "inStock": true,
    "stockQuantity": 25,
    "createdAt": "2024-01-15T10:30:00.000Z",
    "updatedAt": "2024-01-15T10:30:00.000Z"
  }
}
```

**Error Response (400 Bad Request):**
```json
{
  "success": false,
  "message": "Name and price are required fields"
}
```

---

### 2. Get All Products

**GET** `/api/products`

Retrieve all products from the database.

**Response (200 OK):**
```json
{
  "success": true,
  "count": 5,
  "data": [
    {
      "_id": "64a1b2c3d4e5f6g7h8i9j0k1",
      "name": "Laptop",
      "description": "High-performance laptop",
      "price": 999.99,
      "category": "Electronics",
      "inStock": true,
      "stockQuantity": 25,
      "createdAt": "2024-01-15T10:30:00.000Z",
      "updatedAt": "2024-01-15T10:30:00.000Z"
    }
  ]
}
```

---

### 3. Get Product by ID

**GET** `/api/products/:id`

Get a single product by its ID.

**URL Parameters:**
- `id` - Product ID (MongoDB ObjectId)

**Response (200 OK):**
```json
{
  "success": true,
  "data": {
    "_id": "64a1b2c3d4e5f6g7h8i9j0k1",
    "name": "Laptop",
    "description": "High-performance laptop",
    "price": 999.99,
    "category": "Electronics",
    "inStock": true,
    "stockQuantity": 25,
    "createdAt": "2024-01-15T10:30:00.000Z",
    "updatedAt": "2024-01-15T10:30:00.000Z"
  }
}
```

**Error Response (404 Not Found):**
```json
{
  "success": false,
  "message": "Product not found"
}
```

---

### 4. Update Product

**PUT** `/api/products/:id`

Update an existing product. You can update any field(s).

**URL Parameters:**
- `id` - Product ID (MongoDB ObjectId)

**Request Body:**
```json
{
  "name": "Updated Laptop",
  "price": 1099.99,
  "stockQuantity": 30
}
```

**Response (200 OK):**
```json
{
  "success": true,
  "message": "Product updated successfully",
  "data": {
    "_id": "64a1b2c3d4e5f6g7h8i9j0k1",
    "name": "Updated Laptop",
    "description": "High-performance laptop",
    "price": 1099.99,
    "category": "Electronics",
    "inStock": true,
    "stockQuantity": 30,
    "createdAt": "2024-01-15T10:30:00.000Z",
    "updatedAt": "2024-01-15T10:35:00.000Z"
  }
}
```

**Error Response (404 Not Found):**
```json
{
  "success": false,
  "message": "Product not found"
}
```

---

### 5. Delete Product

**DELETE** `/api/products/:id`

Delete a product by its ID.

**URL Parameters:**
- `id` - Product ID (MongoDB ObjectId)

**Response (200 OK):**
```json
{
  "success": true,
  "message": "Product deleted successfully"
}
```

**Error Response (404 Not Found):**
```json
{
  "success": false,
  "message": "Product not found"
}
```

---

## Frontend Integration Examples

### JavaScript (Fetch API)

```javascript
const API_URL = 'http://localhost:3000/api/products';

// Create Product
async function createProduct(productData) {
  const response = await fetch(API_URL, {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
    },
    body: JSON.stringify(productData),
  });
  return await response.json();
}

// Get All Products
async function getAllProducts() {
  const response = await fetch(API_URL);
  return await response.json();
}

// Get Product by ID
async function getProductById(id) {
  const response = await fetch(`${API_URL}/${id}`);
  return await response.json();
}

// Update Product
async function updateProduct(id, updateData) {
  const response = await fetch(`${API_URL}/${id}`, {
    method: 'PUT',
    headers: {
      'Content-Type': 'application/json',
    },
    body: JSON.stringify(updateData),
  });
  return await response.json();
}

// Delete Product
async function deleteProduct(id) {
  const response = await fetch(`${API_URL}/${id}`, {
    method: 'DELETE',
  });
  return await response.json();
}
```

### Axios

```javascript
import axios from 'axios';

const API_URL = 'http://localhost:3000/api/products';

const api = axios.create({
  baseURL: API_URL,
  headers: {
    'Content-Type': 'application/json',
  },
});

// Create Product
export const createProduct = (productData) => api.post('/', productData);

// Get All Products
export const getAllProducts = () => api.get('/');

// Get Product by ID
export const getProductById = (id) => api.get(`/${id}`);

// Update Product
export const updateProduct = (id, updateData) => api.put(`/${id}`, updateData);

// Delete Product
export const deleteProduct = (id) => api.delete(`/${id}`);
```

### React Example

```javascript
import { useState, useEffect } from 'react';

function ProductsList() {
  const [products, setProducts] = useState([]);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    fetchProducts();
  }, []);

  const fetchProducts = async () => {
    try {
      const response = await fetch('http://localhost:3000/api/products');
      const data = await response.json();
      if (data.success) {
        setProducts(data.data);
      }
    } catch (error) {
      console.error('Error fetching products:', error);
    } finally {
      setLoading(false);
    }
  };

  const handleCreateProduct = async (productData) => {
    try {
      const response = await fetch('http://localhost:3000/api/products', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(productData),
      });
      const data = await response.json();
      if (data.success) {
        fetchProducts(); // Refresh list
      }
    } catch (error) {
      console.error('Error creating product:', error);
    }
  };

  if (loading) return <div>Loading...</div>;

  return (
    <div>
      {products.map((product) => (
        <div key={product._id}>
          <h3>{product.name}</h3>
          <p>${product.price}</p>
        </div>
      ))}
    </div>
  );
}
```

## Error Handling

All endpoints return errors in the following format:

```json
{
  "success": false,
  "message": "Error message here",
  "error": "Detailed error information (in development)"
}
```

**HTTP Status Codes:**
- `200` - Success
- `201` - Created
- `400` - Bad Request (validation errors)
- `404` - Not Found
- `500` - Internal Server Error

## CORS

CORS is enabled for all origins. You can make requests from any frontend application.

## Product Schema

```typescript
interface Product {
  _id: string;              // MongoDB ObjectId
  name: string;             // Required
  description?: string;
  price: number;           // Required, min: 0
  category?: string;
  inStock: boolean;        // Default: true
  stockQuantity: number;   // Default: 0, min: 0
  createdAt: Date;         // Auto-generated
  updatedAt: Date;         // Auto-generated
}
```
