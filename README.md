# E-Commerce Microservices Application

A full-stack MERN e-commerce application built with microservices architecture, featuring 4 separate Node.js backend services and a React frontend.

## 🏗️ Architecture Overview

This application demonstrates modern microservices architecture with the following components:

```
Frontend (React) → API Gateway → Microservices
                                    ├── User Service (3001)
                                    ├── Product Service (3002)
                                    ├── Cart Service (3003)
                                    └── Order Service (3004)
```

## 🔧 Technology Stack

### Backend
- **Runtime**: Node.js with Express.js
- **Database**: MongoDB with Mongoose ODM
- **Authentication**: JWT tokens
- **Architecture**: RESTful APIs with microservices

### Frontend
- **Framework**: React 18
- **Routing**: React Router
- **State Management**: React Query + Context API
- **HTTP Client**: Axios
- **Styling**: CSS3 with responsive design

## 📦 Microservices

### 1. User Service (Port 3001)
- User registration and authentication
- Profile management
- JWT token generation and validation
- User data persistence

**Endpoints:**
- `POST /api/auth/register` - User registration
- `POST /api/auth/login` - User authentication
- `GET /api/auth/me` - Get current user
- `GET /api/users/profile` - Get user profile
- `PUT /api/users/profile` - Update user profile

### 2. Product Service (Port 3002)
- Product catalog management
- Category management
- Product search and filtering
- Inventory tracking

**Endpoints:**
- `GET /api/products` - Get products with filtering/pagination
- `GET /api/products/:id` - Get single product
- `POST /api/products` - Create product (admin)
- `PUT /api/products/:id` - Update product (admin)
- `DELETE /api/products/:id` - Soft delete product (admin)
- `GET /api/categories` - Get all categories
- `POST /api/categories` - Create category (admin)

### 3. Cart Service (Port 3003)
- Shopping cart management
- Add/remove/update cart items
- Cart validation
- Integration with Product Service

**Endpoints:**
- `GET /api/cart/:userId` - Get user's cart
- `POST /api/cart/:userId/items` - Add item to cart
- `PUT /api/cart/:userId/items/:productId` - Update cart item
- `DELETE /api/cart/:userId/items/:productId` - Remove cart item
- `DELETE /api/cart/:userId` - Clear entire cart
- `POST /api/cart/:userId/validate` - Validate cart items

### 4. Order Service (Port 3004)
- Order creation and management
- Payment processing simulation
- Order status tracking
- Integration with Cart and Product Services

**Endpoints:**
- `GET /api/orders/user/:userId` - Get user's orders
- `GET /api/orders/:id` - Get single order
- `POST /api/orders` - Create new order
- `PUT /api/orders/:id/status` - Update order status
- `DELETE /api/orders/:id` - Cancel order
- `POST /api/payments/process` - Process payment
- `POST /api/payments/refund` - Process refund

## 🚀 Getting Started

### Prerequisites
- Node.js 16+ and npm
- MongoDB (local or cloud instance)

  
### Dockerized deployment
   Create and Configure docker images and push to Hub

```docker-compose up -d --build```
<img width="1556" height="231" alt="Screenshot 2025-07-24 174723" src="https://github.com/user-attachments/assets/bf179659-2c19-494b-826b-8bc5c2c38d51" />

----------------------------------------------------------------------------------------------------------------------------------------------------------------
Application Worked as expected in Docker

<img width="1772" height="831" alt="Screenshot 2025-07-24 174752" src="https://github.com/user-attachments/assets/99339afa-63c1-420f-9746-7928b9e13abf" />

<img width="1734" height="904" alt="Screenshot 2025-07-24 174813" src="https://github.com/user-attachments/assets/92190f18-d13c-4dae-b694-e3e79a48b22d" />

<img width="1720" height="947" alt="Screenshot 2025-07-24 174839" src="https://github.com/user-attachments/assets/6b12120f-1f86-4172-8f3c-78fc582bbe43" />

# MongoDB Records

<img width="1897" height="642" alt="Screenshot 2025-07-24 174918" src="https://github.com/user-attachments/assets/4dd3bd56-2acd-4539-98fc-048bc4c72ac9" />

### Kubernetes Setup

Create and Configure K8s Cluster in AWS

``` eksctl create cluster --name mlal-ecommerce-cluster  --region us-west-2 --nodegroup-name standard-workers --node-type t3.medium  --nodes 2 ```
<img width="1920" height="1727" alt="Firefox_Screenshot_2025-07-24T12-42-47 410Z" src="https://github.com/user-attachments/assets/62a61f82-e5ca-4681-9aa1-4cb00d2f3bc9" />


### Create Jenkins pipeline and deploy the application

<img width="1879" height="901" alt="Screenshot 2025-07-24 175146" src="https://github.com/user-attachments/assets/2a55ba68-d1dc-42c9-8bd5-8b310702b310" />
<img width="1858" height="855" alt="Firefox_Screenshot_2025-07-24T12-21-15 493Z" src="https://github.com/user-attachments/assets/31e0a1d8-00f5-417e-a826-1a4ac2d25596" />

# Post Pipeline Success, Validating Services, Pods, Kube Nodes
``` kubects get nodes   ```
<img width="1583" height="150" alt="Screenshot 2025-07-24 180649" src="https://github.com/user-attachments/assets/8c5ef4d6-f2dc-47e9-aeb1-786d730c3431" />

``` kubects get pods ```
<img width="1583" height="150" alt="Screenshot 2025-07-24 180649" src="https://github.com/user-attachments/assets/8c5ef4d6-f2dc-47e9-aeb1-786d730c3431" />

``` kubects get svc ```

<img width="1592" height="185" alt="Screenshot 2025-07-24 180712" src="https://github.com/user-attachments/assets/89deb4ae-94da-4faa-8c35-ff574ede2f03" />


## The application will be available at:
- Frontend: http://localhost:3000
- User Service: http://localhost:3001
- Product Service: http://localhost:3002
- Cart Service: http://localhost:3003
- Order Service: http://localhost:3004

### Now all implementation completed and it's working fine on K8s cluster by frontend load balancer then I will have to shutdown the application. So below is the process which I followed.

## Safely Shutdown Docker

``` docker-compose down ```
<img width="1587" height="222" alt="Screenshot 2025-07-24 181537" src="https://github.com/user-attachments/assets/4239bb6f-ef86-4ac7-a9f8-94c2ac6d8b51" />


## Post Deployment, cleanup activity performed.

``` kubectl delete all --all ```

<img width="1596" height="262" alt="Screenshot 2025-07-24 181947" src="https://github.com/user-attachments/assets/59d660bb-1d1e-4fbd-9cbb-347734861e00" />


# delete EKS cluster 
``` ekctl delete cluster --name munish-ecommerce-cluster-3 --region us-west-2 ```
<img width="1574" height="363" alt="Screenshot 2025-07-24 182549" src="https://github.com/user-attachments/assets/0780169f-1020-451f-9f25-d12ef95ae1e0" />

## 🎯 Features

### User Features
- **Authentication**: Register and login with JWT tokens
- **Product Browsing**: View products with search, filtering, and pagination
- **Shopping Cart**: Add, update, and remove items
- **Checkout Process**: Complete order placement with shipping and payment
- **Order Management**: View order history and track status
- **Profile Management**: Update personal information and addresses

### Admin Features (Future Enhancement)
- Product and category management
- Order status updates
- Inventory management
- User management

### Technical Features
- **Microservices Architecture**: Loosely coupled services
- **RESTful APIs**: Standard HTTP methods and status codes
- **Data Validation**: Input validation and error handling
- **Cross-Service Communication**: HTTP-based service interactions
- **Responsive Design**: Mobile-friendly user interface
- **Error Handling**: Comprehensive error management
- **Loading States**: User-friendly loading indicators

## 📁 Project Structure

```
ecommerce-microservices/
├── backend/
│   ├── user-service/
│   │   ├── models/
│   │   ├── routes/
│   │   ├── middleware/
│   │   ├── server.js
│   │   └── package.json
│   ├── product-service/
│   │   ├── models/
│   │   ├── routes/
│   │   ├── server.js
│   │   └── package.json
│   ├── cart-service/
│   │   ├── models/
│   │   ├── routes/
│   │   ├── server.js
│   │   └── package.json
│   └── order-service/
│       ├── models/
│       ├── routes/
│       ├── server.js
│       └── package.json
├── frontend/
│   ├── public/
│   ├── src/
│   │   ├── components/
│   │   ├── contexts/
│   │   ├── pages/
│   │   ├── services/
│   │   ├── App.js
│   │   └── index.js
│   └── package.json
├── package.json
└── README.md
```

## 🔧 API Testing

You can test the APIs using tools like Postman or curl:

```bash
# Health check for all services
curl http://localhost:3001/health
curl http://localhost:3002/health
curl http://localhost:3003/health
curl http://localhost:3004/health

# Register a new user
curl -X POST http://localhost:3001/api/auth/register \
  -H "Content-Type: application/json" \
  -d '{"firstName":"John","lastName":"Doe","email":"john@example.com","password":"password123"}'

# Get products
curl http://localhost:3002/api/products

# Get categories
curl http://localhost:3002/api/categories
```

## 🚀 Deployment

### Production Considerations

1. **Environment Variables**: Use proper environment variable management
2. **Database**: Use MongoDB Atlas or other managed database services
3. **Process Management**: Use PM2 or similar for process management
4. **Load Balancing**: Implement load balancing for high availability
5. **Monitoring**: Add logging and monitoring solutions
6. **Security**: Implement rate limiting, CORS, and other security measures

