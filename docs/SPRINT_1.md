# Sprint 1: Architecture & Scope Definition

## Section 1: Target Audience & Market Focus
* **Primary Persona:** Young tech-savvy retail consumers and early adopters who prefer online shopping for gadgets and accessories.
* **Core Pain Point:** The lack of a centralized, responsive, and seamless platform that offers quick product discovery, real-time cart updates, and secure checkout without overwhelming the user.
* **Domain Scope:** Consumer Electronics and Tech Accessories.

## Section 2: Minimum Viable Product (MVP) Feature Scope
| Category | Feature Name | Description | Priority |
| :--- | :--- | :--- | :--- |
| Authentication | User Registration & Auth | Password hashing and JWT-based authentication mechanism. | High (MVP) |
| Catalog | Product List & Search | Product browsing interface with taxonomy-based filtering. | High (MVP) |
| Cart | Cart Management | State persistent cart management (item addition, modification, and deletion). | High (MVP) |
| Checkout | Order Processing | Mock or Stripe payment gateway integration and order object instantiation. | High (MVP) |
| Admin | Inventory Control | Administrative CRUD operations for product inventory. | Medium |

## Section 3: Tech Stack Selection & Justification
* **Frontend Framework:** React.js
  * **Justification:** React offers a component-based architecture which is highly efficient for building dynamic, state-heavy user interfaces like shopping carts and product catalogs. It ensures rapid rendering and a seamless user experience.
* **Backend Infrastructure:** Node.js with Express.js
  * **Justification:** Node.js provides a non-blocking, event-driven architecture that is perfect for handling concurrent API requests in an e-commerce platform. Express.js allows for rapid routing and middleware integration.
* **Database Management System:** MongoDB Atlas
  * **Justification:** As a NoSQL document database, MongoDB offers high scalability and flexible schema design, which is ideal for managing varied product catalogs. The trade-off is handling relational integrity at the application level, but it greatly accelerates full-stack development speed.

## Section 4: Entity-Relationship Diagram (ERD)

```mermaid
erDiagram
    USERS ||--o{ ORDERS : places
    USERS ||--o| CART : owns
    ORDERS ||--|{ ORDER_ITEMS : contains
    PRODUCTS ||--o{ ORDER_ITEMS : ordered_in
    CATEGORIES ||--o{ PRODUCTS : categorizes
    CART ||--|{ CART_ITEMS : contains
    PRODUCTS ||--o{ CART_ITEMS : added_to

    USERS {
        INTEGER id PK
        VARCHAR email
        VARCHAR password_hash
        TIMESTAMP created_at
    }

    CATEGORIES {
        INTEGER id PK
        VARCHAR name
        VARCHAR description
    }

    PRODUCTS {
        INTEGER id PK
        INTEGER category_id FK
        VARCHAR name
        DECIMAL price
        INTEGER stock_quantity
    }

    ORDERS {
        INTEGER id PK
        INTEGER user_id FK
        DECIMAL total_amount
        VARCHAR status
        TIMESTAMP created_at
    }

    ORDER_ITEMS {
        INTEGER id PK
        INTEGER order_id FK
        INTEGER product_id FK
        INTEGER quantity
        DECIMAL unit_price
    }

    CART {
        INTEGER id PK
        INTEGER user_id FK
        TIMESTAMP updated_at
    }

    CART_ITEMS {
        INTEGER id PK
        INTEGER cart_id FK
        INTEGER product_id FK
        INTEGER quantity
    }
