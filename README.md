# Fitlex

[Fitlex](https://fitlex.cakrasera.com) is a modern e-commerce platform for fitness equipment, designed to provide a seamless shopping experience for users looking to enhance their home workouts.

Table of Contents:

- [Fitlex](#fitlex)
  - [Links](#links)
  - [Architecture](#architecture)
    - [Presentation Layer (UI)](#presentation-layer-ui)
    - [Application Layer (Business Logic)](#application-layer-business-logic)
    - [Data Access Layer (Database)](#data-access-layer-database)
  - [Flowchart](#flowchart)
  - [Features](#features)
  - [UI Designs](#ui-designs)
    - [Home Page](#home-page)
  - [Entity Relationship Diagram (ERD)](#entity-relationship-diagram-erd)
  - [REST API Endpoints](#rest-api-endpoints)
    - [Product](#product)
    - [Add New Product](#add-new-product)

## Links

- Website/Frontend: <https://fitlex.cakrasera.com>
  - Backend: <https://fitlex-api.cakrasera.dev>
- Repositories:
  - General: <https://github.com/cakrasera/fitlex>
  - Backend: <https://github.com/cakrasera/fitlex-api>
  - Frontend: <https://github.com/cakrasera/fitlex-web>

Inspirations:

- <https://www.pvolve.com>
- <https://www.trxtraining.com/>
- <https://www.speediance.com>

## Architecture

### Presentation Layer (UI)

- HTML
- CSS
  - Tailwind CSS
  - Shadcn/ui
- Javascript
- Typescript
- React
- React Router
- Docker

### Application Layer (Business Logic)

- Javascript
- Typescript
- Hono
- OpenAPI
- Zod
- Docker

### Data Access Layer (Database)

- Prisma
- PostgreSQL
- Docker

## Flowchart

```mermaid
graph TD
    A[Visit Website/App] --> B{**Home Page**};

    B -- Click Banner / Promo Bundle --> C[**Bundle Detail Page**];
    B -- Click Catalog Menu --> D[**Product Catalog Page**];

    D -- Select Product / Bundle --> C;

    C -- "Package includes: [Tool A] + [Tool B] & Program X" --> F[**Add to Cart**];

    F --> G{**Shopping Cart Page**};
    G -- "Continue Shopping" --> D;
    G -- "Proceed to Checkout" --> H[**Checkout Page**];

    H --> I[Payment Processing];

    I --> J{**Order Confirmation Page**};
    J -- "Order Received (Order ID #123)" --> K[User Receives Email/Notification];
```

## Features

- **Home page**
  - A hero section with a large banner highlighting the main promotional bundle (e.g., "30% Off the Desk Warrior Bundle").
  - The primary call-to-action (CTA) is "View Bundle" or "Shop Now," leading directly to that bundle's detail page.
  - A section showcasing a few other featured bundles.
  - Access to the full product catalog with filtering (by tool, price, workout goal) and sorting (best-sellers, latest) options. ([see example](https://www.pvolve.com/collections/equipment))
- **Product page**
  - Product image gallery, including **short videos of the product being used in a limited space** (e.g., a small apartment room).
  - SKU (stock keeping unit)
  - Name
  - Price (in Indonesian Rupiah)
  - Detailed description
    - Technical specifications.
    - Key benefits.
    - A **"Related In-App Workout Programs"** section that shows how this product can be used.
  - Add to cart form: quantity input & add to cart button
- **Shopping cart page**
  - Product items to buy
    - Image, name, price, quantity, total (price x quantity)
    - Remove item from cart
  - Navigation links: continue shopping, go to products catalogue
  - Proceed to checkout
- **Checkout page**
  - Order summary
    - List of products to purchase
    - Grand total of all items
  - Payment method selection (e.g., bank transfer, e-wallet)
- **Order processing**
  - Confirmation page with order details (Order Number, summary, status).
  - An engagement CTA: "**While waiting for your order, download our app and set up your account!**".
  - Order status updates sent via email or app notifications (Order Processed, Shipped, Tracking Number).

## UI Designs

- Figma: <https://www.figma.com/design/YuakY42L50ZxmpKhSU0Dzu/fitlex?t=Wpj3PZr2GdZa7WLb-1>

### Home Page

<img alt="Home Page" src="./designs/home.jpg" width="400" />

## Entity Relationship Diagram (ERD)

Detailed design: [https://dbdiagram.io/d/fitlex-688948d2cca18e685c55af5c](https://dbdiagram.io/d/fitlex-688948d2cca18e685c55af5c)

![ERD](./diagrams/erd.svg)

## REST API Endpoints

- Production: `https://fitlex-backend.cakrasera.dev`
- Local: `http://localhost:3000`

| Endpoint             | HTTP  | Description             |
| -------------------- | ----- | ----------------------- |
| `/products`          | `GET` | Get all products        |
| `/products/:slug`    | `GET` | Get product by slug     |
| `/products/featured` | `GET` | Get product by featured |

| Endpoint         | HTTP   | Permission    |
| ---------------- | ------ | ------------- |
| `/`              | `GET`  | Public        |
| `/users`         | `GET`  | Public        |
| `/users/{id}`    | `GET`  | Public        |
| `/auth/register` | `POST` | Public        |
| `/auth/login`    | `POST` | Public        |
| `/auth/me`       | `GET`  | Authenticated |
| `/auth/logout`   | `POST` | Authenticated |

### Product

Example response for a single product:

```json
{
  "id": "abc123",
  "name": "Panda Plush",
  "price": 120000
}
```

### Add New Product

Request Body:

```json
{
  "name": "Panda Plush",
  "price": 120000,
  "color": "white"
}
```

Response Body:

```json
{
  "id": "abc123",
  "name": "Panda Plush",
  "price": 120000,
  "colors": ["white"]
}
```
