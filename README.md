# E-Commerce API Documentation

## Overview
This is a Flask-based API for an e-commerce platform. It provides functionalities such as product listing, search, cart management, recommendations, and more.

## Installation
### Prerequisites
- Python 3.7+
- pip
- Flask and required dependencies

### Setup
```sh
pip install -r requirements.txt
python app.py
```

## API Endpoints

### 1. Get Products
**Endpoint:** `GET /products`

**Query Parameters:**
- `category` (optional) - Filter by category
- `brand` (optional) - Filter by brand
- `sort` (optional) - Sort by `price_asc`, `price_desc`, `rating_desc`

**Example Request:**
```sh
curl "http://localhost:5000/products?category=electronics&sort=price_asc"
```

**Response:**
```json
[
  {
    "id": 1,
    "product": "Smartphone",
    "brand": "BrandX",
    "category": "electronics",
    "sale_price": 199.99,
    "market_price": 249.99,
    "rating": 4.5
  }
]
```

### 2. Search Products
**Endpoint:** `GET /search`

**Query Parameters:**
- `q` (required) - Search query

**Example Request:**
```sh
curl "http://localhost:5000/search?q=laptop"
```

**Response:**
```json
[
  {
    "id": 2,
    "product": "Gaming Laptop",
    "brand": "BrandY",
    "category": "electronics",
    "sale_price": 899.99,
    "market_price": 999.99
  }
]
```

### 3. Get Search Suggestions
**Endpoint:** `GET /search/suggestions`

**Query Parameters:**
- `q` (required) - Query for suggestions

**Example Request:**
```sh
curl "http://localhost:5000/search/suggestions?q=phone"
```

**Response:**
```json
{
  "suggestions": [
    { "type": "product", "text": "Smartphone", "icon": "🏷️" },
    { "type": "brand", "text": "BrandX", "icon": "®️" }
  ],
  "recommended_products": [
    { "id": 1, "product": "Smartphone", "brand": "BrandX", "category": "electronics" }
  ]
}
```

### 4. Get Product Details
**Endpoint:** `GET /product/{product_id}`

**Example Request:**
```sh
curl "http://localhost:5000/product/1"
```

**Response:**
```json
{
  "product": {
    "id": 1,
    "product": "Smartphone",
    "brand": "BrandX",
    "category": "electronics",
    "sale_price": 199.99
  },
  "similar_products": [
    { "id": 3, "product": "Tablet", "brand": "BrandX" }
  ]
}
```

### 5. Cart Operations

#### Get Cart
**Endpoint:** `GET /cart`

**Example Request:**
```sh
curl "http://localhost:5000/cart"
```

**Response:**
```json
{
  "items": [],
  "subtotal": 0
}
```

#### Add to Cart
**Endpoint:** `POST /cart/add`

**Request Body:**
```json
{ "product_id": 1 }
```

**Example Request:**
```sh
curl -X POST "http://localhost:5000/cart/add" -H "Content-Type: application/json" -d '{"product_id": 1}'
```

**Response:**
```json
{
  "items": [
    { "id": 1, "product": "Smartphone", "brand": "BrandX", "price": 199.99, "quantity": 1 }
  ],
  "subtotal": 199.99
}
```

#### Remove from Cart
**Endpoint:** `POST /cart/remove`

**Request Body:**
```json
{ "product_id": 1 }
```

**Example Request:**
```sh
curl -X POST "http://localhost:5000/cart/remove" -H "Content-Type: application/json" -d '{"product_id": 1}'
```

**Response:**
```json
{
  "items": [],
  "subtotal": 0
}
```

#### Update Cart Quantity
**Endpoint:** `POST /cart/update`

**Request Body:**
```json
{ "product_id": 1, "quantity": 3 }
```

**Example Request:**
```sh
curl -X POST "http://localhost:5000/cart/update" -H "Content-Type: application/json" -d '{"product_id": 1, "quantity": 3}'
```

**Response:**
```json
{
  "items": [
    { "id": 1, "product": "Smartphone", "brand": "BrandX", "price": 199.99, "quantity": 3 }
  ],
  "subtotal": 599.97
}
```

### 6. Get Categories
**Endpoint:** `GET /categories`

**Example Request:**
```sh
curl "http://localhost:5000/categories"
```

**Response:**
```json
[
  { "name": "electronics", "subcategories": ["mobiles", "laptops"], "productCount": 120 }
]
```

### 7. Get Featured Products
**Endpoint:** `GET /featured`

**Example Request:**
```sh
curl "http://localhost:5000/featured"
```

**Response:**
```json
{
  "topRated": [{ "product": "Smartphone", "rating": 4.8 }],
  "bestDeals": [{ "product": "Laptop", "discount": 20 }],
  "newArrivals": [{ "product": "Smartwatch" }],
  "trending": [{ "product": "Tablet" }]
}
```

## Running the Application
```sh
python app.py
```

## Conclusion
This API provides an efficient and structured way to handle e-commerce functionalities. You can extend it further based on your requirements.

