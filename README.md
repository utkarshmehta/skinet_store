# SkiNet E-Commerce Platform

A modern, full-stack e-commerce platform designed specifically for ski and winter sports equipment. SkiNet provides a seamless shopping experience with advanced product filtering, secure payment processing, and comprehensive order management.

## Table of Contents

- [Project Overview](#project-overview)
- [Architecture](#architecture)
- [Tech Stack](#tech-stack)
- [Setup Instructions](#setup-instructions)
- [Project Structure](#project-structure)
- [Development Guidelines](#development-guidelines)
- [API Documentation](#api-documentation)
- [Database Schema](#database-schema)
- [Contributing Guidelines](#contributing-guidelines)

## Project Overview

### Purpose

SkiNet is a cutting-edge e-commerce application built to revolutionize the online shopping experience for ski and winter sports enthusiasts. The platform offers:

- **Product Catalog**: Browse a comprehensive collection of ski equipment, snowboards, apparel, and accessories
- **Advanced Search & Filtering**: Find products by brand, price range, size, skill level, and season
- **Secure Payment Processing**: Integrated payment gateway for safe and reliable transactions
- **Order Management**: Track orders, manage returns, and access order history
- **User Accounts**: Personalized shopping experience with saved preferences and addresses
- **Admin Dashboard**: Comprehensive tools for managing products, orders, and users
- **Shopping Cart**: Persistent cart with real-time updates and inventory management

### Key Features

- ✅ Responsive design for mobile and desktop
- ✅ Real-time inventory tracking
- ✅ Secure JWT-based authentication
- ✅ Role-based access control (User, Admin)
- ✅ Product reviews and ratings
- ✅ Wishlist functionality
- ✅ Order tracking and notifications
- ✅ Advanced search with filters
- ✅ Payment integration with Stripe/PayPal
- ✅ API-first architecture

## Architecture

### High-Level Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                     Client Layer                             │
│              (Angular/React SPA Frontend)                    │
└──────────────────────────────┬──────────────────────────────┘
                               │ HTTP/REST API
┌──────────────────────────────▼──────────────────────────────┐
│                    API Gateway Layer                         │
│                  (Express.js Server)                         │
├─────────────────────────────────────────────────────────────┤
│  Authentication │ Validation │ Logging │ Error Handling     │
└──────────────────────────────┬──────────────────────────────┘
                               │
┌──────────────────────────────▼──────────────────────────────┐
│                   Business Logic Layer                       │
│         (Controllers, Services, Business Logic)             │
├─────────────────────────────────────────────────────────────┤
│  Product Service │ Order Service │ User Service │ etc.      │
└──────────────────────────────┬──────────────────────────────┘
                               │
┌──────────────────────────────▼──────────────────────────────┐
│                   Data Access Layer                          │
│              (Repository Pattern)                            │
├─────────────────────────────────────────────────────────────┤
│           Product Repo │ Order Repo │ User Repo             │
└──────────────────────────────┬──────────────────────────────┘
                               │
┌──────────────────────────────▼──────────────────────────────┐
│                   Database Layer                             │
│               (SQL Database with ORM)                        │
├─────────────────────────────────────────────────────────────┤
│    Products │ Users │ Orders │ Reviews │ Inventory          │
└─────────────────────────────────────────────────────────────┘
```

### Design Patterns

- **Repository Pattern**: Abstraction of data access logic
- **Service Layer Pattern**: Business logic separation
- **Middleware Pattern**: Cross-cutting concerns (auth, logging, validation)
- **DTO Pattern**: Data Transfer Objects for API responses
- **Factory Pattern**: Object creation for complex entities

## Tech Stack

### Frontend
- **Framework**: Angular 16+ / React 18+
- **State Management**: NgRx / Redux
- **Styling**: Bootstrap 5 / Tailwind CSS
- **HTTP Client**: Angular HttpClient / Axios
- **Build Tool**: Angular CLI / Webpack

### Backend
- **Runtime**: Node.js (v16 or higher)
- **Framework**: Express.js 4.x
- **Language**: TypeScript 5.x
- **Authentication**: JWT (JSON Web Tokens)
- **Validation**: Joi / class-validator

### Database
- **Primary DB**: SQL Server / PostgreSQL
- **ORM**: Entity Framework Core / TypeORM / Sequelize
- **Migrations**: Flyway / TypeORM migrations

### External Services
- **Payment Processing**: Stripe API / PayPal API
- **Email Service**: SendGrid / Nodemailer
- **Cloud Storage**: AWS S3 / Azure Blob Storage
- **CDN**: CloudFront / Azure CDN

### Development Tools
- **Version Control**: Git
- **Package Manager**: npm / yarn
- **Testing**: Jest / Mocha + Chai
- **Linting**: ESLint
- **Code Formatter**: Prettier
- **Documentation**: Swagger/OpenAPI
- **Container**: Docker & Docker Compose

## Setup Instructions

### Prerequisites

Before you begin, ensure you have the following installed:

- Node.js v16+ (download from [nodejs.org](https://nodejs.org))
- npm v7+ or yarn v1.22+
- Git
- Docker & Docker Compose (optional, for containerized setup)
- SQL Server or PostgreSQL

### Backend Setup

1. **Clone the Repository**
   ```bash
   git clone https://github.com/utkarshmehta/skinet_store.git
   cd skinet_store
   ```

2. **Checkout Develop Branch**
   ```bash
   git checkout develop
   ```

3. **Install Dependencies**
   ```bash
   cd API
   npm install
   ```

4. **Environment Configuration**
   Create a `.env` file in the `API` directory:
   ```env
   # Database Configuration
   DB_HOST=localhost
   DB_PORT=5432
   DB_NAME=skinet_db
   DB_USER=postgres
   DB_PASSWORD=your_password

   # JWT Configuration
   JWT_SECRET=your_jwt_secret_key
   JWT_EXPIRY=7d

   # Payment Gateway
   STRIPE_SECRET_KEY=your_stripe_secret
   STRIPE_PUBLIC_KEY=your_stripe_public

   # Email Service
   SENDGRID_API_KEY=your_sendgrid_key
   EMAIL_FROM=noreply@skinet.com

   # AWS Configuration
   AWS_ACCESS_KEY_ID=your_aws_access_key
   AWS_SECRET_ACCESS_KEY=your_aws_secret
   AWS_S3_BUCKET=skinet-products

   # Application
   NODE_ENV=development
   PORT=3000
   CLIENT_URL=http://localhost:4200
   ```

5. **Database Setup**
   ```bash
   # Create database
   npm run db:create

   # Run migrations
   npm run db:migrate

   # Seed sample data (optional)
   npm run db:seed
   ```

6. **Start Backend Server**
   ```bash
   npm run dev
   ```
   Server runs on `http://localhost:3000`

### Frontend Setup

1. **Navigate to Client Directory**
   ```bash
   cd ../client
   ```

2. **Install Dependencies**
   ```bash
   npm install
   ```

3. **Environment Configuration**
   Create an `environment.ts` file in `src/environments/`:
   ```typescript
   export const environment = {
     production: false,
     apiUrl: 'http://localhost:3000/api',
     stripePublicKey: 'your_stripe_public_key'
   };
   ```

4. **Start Development Server**
   ```bash
   ng serve
   # or
   npm start
   ```
   Application runs on `http://localhost:4200`

### Docker Setup (Optional)

1. **Build and Run with Docker Compose**
   ```bash
   docker-compose up -d
   ```

2. **View Logs**
   ```bash
   docker-compose logs -f
   ```

3. **Stop Services**
   ```bash
   docker-compose down
   ```

## Project Structure

```
skinet_store/
├── API/                          # Backend application
│   ├── src/
│   │   ├── controllers/          # Route controllers
│   │   │   ├── AuthController.ts
│   │   │   ├── ProductController.ts
│   │   │   ├── OrderController.ts
│   │   │   ├── UserController.ts
│   │   │   └── AdminController.ts
│   │   ├── services/             # Business logic
│   │   │   ├── AuthService.ts
│   │   │   ├── ProductService.ts
│   │   │   ├── OrderService.ts
│   │   │   ├── UserService.ts
│   │   │   └── PaymentService.ts
│   │   ├── repositories/         # Data access
│   │   │   ├── ProductRepository.ts
│   │   │   ├── OrderRepository.ts
│   │   │   ├── UserRepository.ts
│   │   │   └── ReviewRepository.ts
│   │   ├── models/               # Database models
│   │   │   ├── User.ts
│   │   │   ├── Product.ts
│   │   │   ├── Order.ts
│   │   │   ├── OrderItem.ts
│   │   │   └── Review.ts
│   │   ├── middleware/           # Express middleware
│   │   │   ├── authMiddleware.ts
│   │   │   ├── errorHandler.ts
│   │   │   ├── logger.ts
│   │   │   └── validation.ts
│   │   ├── routes/               # API routes
│   │   │   ├── auth.routes.ts
│   │   │   ├── products.routes.ts
│   │   │   ├── orders.routes.ts
│   │   │   ├── users.routes.ts
│   │   │   └── admin.routes.ts
│   │   ├── dtos/                 # Data Transfer Objects
│   │   │   ├── CreateProductDTO.ts
│   │   │   ├── CreateOrderDTO.ts
│   │   │   └── UserDTO.ts
│   │   ├── utils/                # Utility functions
│   │   │   ├── tokenUtils.ts
│   │   │   ├── encryption.ts
│   │   │   └── validators.ts
│   │   ├── config/               # Configuration
│   │   │   ├── database.ts
│   │   │   ├── payment.ts
│   │   │   └── email.ts
│   │   ├── migrations/           # Database migrations
│   │   ├── seeds/                # Database seeds
│   │   ├── tests/                # Unit tests
│   │   └── app.ts               # Express app setup
│   ├── .env                      # Environment variables
│   ├── .env.example             # Example environment file
│   ├── tsconfig.json            # TypeScript configuration
│   ├── package.json
│   └── README.md
│
├── client/                       # Frontend application
│   ├── src/
│   │   ├── app/
│   │   │   ├── components/      # Reusable components
│   │   │   │   ├── header/
│   │   │   │   ├── footer/
│   │   │   │   ├── navbar/
│   │   │   │   ├── product-card/
│   │   │   │   └── shopping-cart/
│   │   │   ├── pages/           # Page components
│   │   │   │   ├── home/
│   │   │   │   ├── products/
│   │   │   │   ├── product-detail/
│   │   │   │   ├── checkout/
│   │   │   │   ├── order-confirmation/
│   │   │   │   └── admin/
│   │   │   ├── services/        # API services
│   │   │   │   ├── product.service.ts
│   │   │   │   ├── order.service.ts
│   │   │   │   ├── auth.service.ts
│   │   │   │   └── user.service.ts
│   │   │   ├── store/           # NgRx/Redux store
│   │   │   │   ├── actions/
│   │   │   │   ├── reducers/
│   │   │   │   ├── effects/
│   │   │   │   └── selectors/
│   │   │   ├── models/          # TypeScript interfaces
│   │   │   ├── guards/          # Route guards
│   │   │   ├── interceptors/    # HTTP interceptors
│   │   │   ├── pipes/           # Custom pipes
│   │   │   └── app-routing.module.ts
│   │   ├── assets/              # Static assets
│   │   ├── environments/        # Environment configs
│   │   ├── styles/              # Global styles
│   │   ├── main.ts
│   │   └── index.html
│   ├── angular.json
│   ├── package.json
│   └── README.md
│
├── docker-compose.yml           # Docker compose configuration
├── .gitignore
├── README.md                    # This file
└── CONTRIBUTING.md
```

## Development Guidelines

### Code Style & Conventions

#### TypeScript Naming Conventions
```typescript
// Classes - PascalCase
class UserRepository { }

// Functions - camelCase
function getUserById(id: string) { }

// Constants - UPPER_SNAKE_CASE
const API_BASE_URL = 'http://localhost:3000/api';

// Interfaces - PascalCase, optionally prefixed with 'I'
interface IUser { }

// Private properties - underscore prefix
private _userId: string;
```

#### File Organization
- One class/interface per file
- Group related functions in modules
- Use barrel exports (index.ts) for cleaner imports

### Code Quality

#### Linting & Formatting
```bash
# Check linting errors
npm run lint

# Fix linting errors
npm run lint:fix

# Format code with Prettier
npm run format

# Check code formatting
npm run format:check
```

#### Testing Guidelines
```bash
# Run all tests
npm test

# Run tests with coverage
npm run test:coverage

# Run tests in watch mode
npm run test:watch

# Run specific test file
npm test -- UserService.test.ts
```

### Commit Conventions

Follow [Conventional Commits](https://www.conventionalcommits.org/):

```bash
# Format: <type>(<scope>): <subject>

# Examples:
git commit -m "feat(products): add product filtering by price range"
git commit -m "fix(auth): resolve JWT token expiration issue"
git commit -m "docs(readme): update setup instructions"
git commit -m "refactor(orders): optimize order status update logic"
git commit -m "test(products): add unit tests for product service"
git commit -m "chore(deps): update express to version 4.18.2"

# Types: feat, fix, docs, style, refactor, test, chore, perf, ci
```

### Git Workflow

1. **Create Feature Branch**
   ```bash
   git checkout develop
   git pull origin develop
   git checkout -b feature/feature-name
   ```

2. **Make Changes & Commit**
   ```bash
   git add .
   git commit -m "feat(feature-name): description"
   ```

3. **Push to Remote**
   ```bash
   git push origin feature/feature-name
   ```

4. **Create Pull Request**
   - Use the PR template
   - Link related issues
   - Add meaningful description

5. **Code Review & Merge**
   - Address review comments
   - Squash commits if needed
   - Merge to develop

### Error Handling

#### Backend
```typescript
// Use consistent error responses
throw new ApiError(
  'Product not found',
  404,
  'PRODUCT_NOT_FOUND'
);

// Middleware handles and formats error
{
  success: false,
  message: 'Product not found',
  code: 'PRODUCT_NOT_FOUND',
  statusCode: 404
}
```

#### Frontend
```typescript
// Handle errors in services
catchError(error => {
  this.handleError(error);
  return throwError(() => error);
})
```

## API Documentation

### Base URL
```
Development: http://localhost:3000/api
Production: https://api.skinet.com/api
```

### Authentication

All protected endpoints require a Bearer token in the Authorization header:
```
Authorization: Bearer <jwt_token>
```

### Core Endpoints

#### Authentication
```
POST   /auth/register         - User registration
POST   /auth/login            - User login
POST   /auth/refresh-token    - Refresh JWT token
POST   /auth/logout           - User logout
POST   /auth/forgot-password  - Request password reset
POST   /auth/reset-password   - Reset password
```

#### Products
```
GET    /products              - List all products (with filters)
GET    /products/:id          - Get product details
POST   /products              - Create product (Admin only)
PUT    /products/:id          - Update product (Admin only)
DELETE /products/:id          - Delete product (Admin only)
GET    /products/:id/reviews  - Get product reviews
POST   /products/:id/reviews  - Add product review
```

#### Orders
```
GET    /orders                - Get user's orders
GET    /orders/:id            - Get order details
POST   /orders                - Create new order
PUT    /orders/:id            - Update order
DELETE /orders/:id            - Cancel order
GET    /orders/:id/invoice    - Download invoice
POST   /orders/:id/payment    - Process payment
```

#### Users
```
GET    /users/profile         - Get user profile
PUT    /users/profile         - Update user profile
GET    /users/addresses       - Get user addresses
POST   /users/addresses       - Add new address
PUT    /users/addresses/:id   - Update address
DELETE /users/addresses/:id   - Delete address
PUT    /users/password        - Change password
GET    /users/wishlist        - Get wishlist
POST   /users/wishlist        - Add to wishlist
DELETE /users/wishlist/:id    - Remove from wishlist
```

#### Admin
```
GET    /admin/dashboard       - Dashboard statistics
GET    /admin/users           - List all users
GET    /admin/orders          - List all orders
GET    /admin/analytics       - Sales analytics
POST   /admin/products        - Bulk upload products
GET    /admin/reports         - Generate reports
```

### Response Format

#### Success Response
```json
{
  "success": true,
  "data": {
    "id": "123",
    "name": "Product Name",
    "price": 299.99
  },
  "message": "Request successful"
}
```

#### Error Response
```json
{
  "success": false,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Invalid input data",
    "details": [
      {
        "field": "email",
        "message": "Invalid email format"
      }
    ]
  }
}
```

### Pagination
```
GET /products?page=1&limit=20&sort=name&order=asc
```

Response includes:
```json
{
  "success": true,
  "data": [...],
  "pagination": {
    "page": 1,
    "limit": 20,
    "total": 150,
    "pages": 8
  }
}
```

### Filtering & Search
```
GET /products?search=ski&category=equipment&minPrice=100&maxPrice=500&brand=Rossignol
```

## Database Schema

### Users Table
```sql
CREATE TABLE users (
  id UUID PRIMARY KEY,
  email VARCHAR(255) UNIQUE NOT NULL,
  password_hash VARCHAR(255) NOT NULL,
  first_name VARCHAR(100),
  last_name VARCHAR(100),
  phone VARCHAR(20),
  role ENUM('user', 'admin') DEFAULT 'user',
  is_active BOOLEAN DEFAULT TRUE,
  email_verified BOOLEAN DEFAULT FALSE,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### Products Table
```sql
CREATE TABLE products (
  id UUID PRIMARY KEY,
  name VARCHAR(255) NOT NULL,
  slug VARCHAR(255) UNIQUE,
  description TEXT,
  category VARCHAR(100),
  brand VARCHAR(100),
  price DECIMAL(10, 2) NOT NULL,
  compare_price DECIMAL(10, 2),
  sku VARCHAR(100) UNIQUE,
  quantity INT DEFAULT 0,
  rating DECIMAL(3, 2) DEFAULT 0,
  review_count INT DEFAULT 0,
  is_active BOOLEAN DEFAULT TRUE,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### Orders Table
```sql
CREATE TABLE orders (
  id UUID PRIMARY KEY,
  order_number VARCHAR(50) UNIQUE,
  user_id UUID NOT NULL,
  status ENUM('pending', 'confirmed', 'shipped', 'delivered', 'cancelled') DEFAULT 'pending',
  total_amount DECIMAL(10, 2) NOT NULL,
  tax_amount DECIMAL(10, 2) DEFAULT 0,
  shipping_amount DECIMAL(10, 2) DEFAULT 0,
  payment_method VARCHAR(50),
  payment_status ENUM('pending', 'completed', 'failed', 'refunded') DEFAULT 'pending',
  shipping_address TEXT,
  billing_address TEXT,
  notes TEXT,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (user_id) REFERENCES users(id)
);
```

### Order Items Table
```sql
CREATE TABLE order_items (
  id UUID PRIMARY KEY,
  order_id UUID NOT NULL,
  product_id UUID NOT NULL,
  quantity INT NOT NULL,
  price DECIMAL(10, 2) NOT NULL,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (order_id) REFERENCES orders(id),
  FOREIGN KEY (product_id) REFERENCES products(id)
);
```

### Reviews Table
```sql
CREATE TABLE reviews (
  id UUID PRIMARY KEY,
  product_id UUID NOT NULL,
  user_id UUID NOT NULL,
  rating INT CHECK (rating >= 1 AND rating <= 5),
  title VARCHAR(255),
  comment TEXT,
  is_verified_purchase BOOLEAN DEFAULT FALSE,
  helpful_count INT DEFAULT 0,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (product_id) REFERENCES products(id),
  FOREIGN KEY (user_id) REFERENCES users(id)
);
```

### Addresses Table
```sql
CREATE TABLE addresses (
  id UUID PRIMARY KEY,
  user_id UUID NOT NULL,
  type ENUM('billing', 'shipping', 'both') DEFAULT 'both',
  street_address VARCHAR(255),
  city VARCHAR(100),
  state_province VARCHAR(100),
  postal_code VARCHAR(20),
  country VARCHAR(100),
  phone VARCHAR(20),
  is_default BOOLEAN DEFAULT FALSE,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (user_id) REFERENCES users(id)
);
```

### Wishlist Table
```sql
CREATE TABLE wishlist (
  id UUID PRIMARY KEY,
  user_id UUID NOT NULL,
  product_id UUID NOT NULL,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  UNIQUE(user_id, product_id),
  FOREIGN KEY (user_id) REFERENCES users(id),
  FOREIGN KEY (product_id) REFERENCES products(id)
);
```

## Contributing Guidelines

### Code of Conduct

We are committed to providing a welcoming and inspiring community. Please read and adhere to our [Code of Conduct](CODE_OF_CONDUCT.md).

### Getting Started with Contributing

1. **Fork the Repository**
   - Click the "Fork" button on GitHub

2. **Clone Your Fork**
   ```bash
   git clone https://github.com/YOUR_USERNAME/skinet_store.git
   cd skinet_store
   ```

3. **Add Upstream Remote**
   ```bash
   git remote add upstream https://github.com/utkarshmehta/skinet_store.git
   ```

### Making Changes

1. **Create a Feature Branch**
   ```bash
   git checkout -b feature/your-feature-name
   ```

2. **Make Your Changes**
   - Write clean, well-documented code
   - Follow the code style guidelines
   - Add tests for new functionality

3. **Test Your Changes**
   ```bash
   npm test
   npm run lint
   ```

4. **Commit Your Changes**
   ```bash
   git commit -m "feat(scope): description of changes"
   ```

5. **Push to Your Fork**
   ```bash
   git push origin feature/your-feature-name
   ```

6. **Create a Pull Request**
   - Provide a clear title and description
   - Link related issues
   - Reference any relevant documentation

### Pull Request Process

1. **PR Description Should Include**
   - What problem does this PR solve?
   - How does it solve the problem?
   - What are the changes made?
   - Any breaking changes?
   - Screenshots (if UI changes)

2. **Code Review Checklist**
   - [ ] Code follows project style guidelines
   - [ ] Tests are included and passing
   - [ ] Documentation is updated
   - [ ] No console errors or warnings
   - [ ] No merge conflicts

3. **Before Merging**
   - Get approval from at least 2 maintainers
   - All CI checks pass
   - Branch is up to date with develop

### Types of Contributions

#### Bug Reports
- Use the bug report template
- Provide clear steps to reproduce
- Include expected and actual behavior
- Add screenshots/videos if applicable

#### Feature Requests
- Use the feature request template
- Explain the use case
- Provide examples or mockups
- Consider backward compatibility

#### Documentation
- Improve README or code comments
- Add API documentation
- Create tutorials or guides
- Fix typos and clarify content

#### Testing
- Add unit tests
- Add integration tests
- Report test failures
- Improve test coverage

### Development Best Practices

1. **Keep PRs Focused**
   - One feature per PR
   - Smaller PRs are reviewed faster
   - Easier to revert if needed

2. **Write Meaningful Commit Messages**
   - Use conventional commit format
   - Reference issues when applicable
   - Explain the "why", not just the "what"

3. **Update Documentation**
   - Update README if needed
   - Add API docs for new endpoints
   - Include JSDoc comments

4. **Performance Considerations**
   - Profile code changes
   - Avoid unnecessary re-renders (frontend)
   - Optimize database queries (backend)
   - Monitor bundle size

5. **Security Practices**
   - Never commit secrets or API keys
   - Validate all user inputs
   - Use parameterized queries
   - Keep dependencies updated

### Reporting Issues

#### Security Issues
- Do NOT open public issues for security vulnerabilities
- Email security concerns to: security@skinet.com

#### Regular Issues
- Use the issue tracker
- Provide clear, reproducible examples
- Include environment details
- Attach error messages/logs

### Getting Help

- **Questions?** Open a discussion on GitHub
- **Stuck?** Ask in the community chat
- **Need guidance?** Reach out to maintainers
- **Documentation?** Check the wiki or docs folder

### Recognition

Contributors will be recognized in:
- README contributors section
- Release notes
- Contributors page
- Community newsletter

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Support

For support, email support@skinet.com or open an issue on GitHub.

## Contact

- **Project Owner**: [Utkarsh Mehta](https://github.com/utkarshmehta)
- **Email**: contact@skinet.com
- **Website**: https://skinet.com

---

**Last Updated**: December 17, 2025

Made with ❤️ by the SkiNet Team