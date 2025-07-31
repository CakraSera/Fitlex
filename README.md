# Fitlex

[Fitlex](https://fitlex.cakrasera.com) is a modern e-commerce platform for fitness equipment, designed to provide a seamless shopping experience for users looking to enhance their home workouts.

Table of Contents:

- [Fitlex](#fitlex)
  - [Links](#links)
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

## Flowchart

```mermaid
graph TD
    A[Masuk ke Website/Aplikasi] --> B{**Home Page**};

    B -- Klik Banner / Kuis Cerdas --> C[Halaman Rekomendasi Paket Solusi];
    B -- Klik Menu Katalog --> D[**Halaman Katalog Produk**];
    B -- Klik Produk Unggulan --> E[**Halaman Detail Produk**];

    D -- Gunakan Filter & Sorting --> D;
    D -- Pilih Produk --> E;

    C -- 'Paket berisi: [Alat A] + [Alat B]' --> F[**Menambahkan ke Keranjang**];
    E -- Mengisi Kuantitas & Klik 'Tambah ke Keranjang' --> F;

    F --> G{**Halaman Keranjang Belanja**};
    G -- "Lanjutkan Belanja" --> D;
    G -- "Lanjut ke Pembayaran" --> H[**Halaman Checkout**];
    G -- Hapus Item --> G;

    H -- Mengisi Alamat & Pilih Pengiriman --> H;
    H -- Pilih Metode Pembayaran --> I[Proses Pembayaran];

    I --> J{**Halaman Konfirmasi Pesanan**};
    J -- "Pesanan Diterima (Order ID #123)" --> K[Pengguna Menerima Email/Notifikasi];
    K -- "Status Pesanan: Diproses" --> K;
```

## Features

- **Home page**
  - Hero section with a promotional banner and a primary call-to-action (CTA) that leads to the **Smart Quiz** (e.g., "Confused? Find Your Program in 2 Minutes")..
  - Featured products section, emphasizing solution-based **Bundled Packages** (e.g., "Morning Energy Pack," "Desk Warrior Pack").
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

Detailed design: [https://dbdiagram.io/d/688948d2cca18e685c55af5c](https://dbdiagram.io/d/688948d2cca18e685c55af5c)

![ERD](./diagrams/erd.svg)

## REST API Endpoints

- Production: `https://fitlex-backend.cakrasera.dev`
- Local: `http://localhost:3000`

| Endpoint         | HTTP     | Description               |
| ---------------- | -------- | ------------------------- |
| `/products`      | `GET`    | Get all products          |
| `/products/:id`  | `GET`    | Get product by id         |
| `/products/seed` | `POST`   | Seed all initial products |
| `/products`      | `POST`   | Add new product           |
| `/products`      | `DELETE` | Delete all products       |
| `/products/:id`  | `DELETE` | Delete product by id      |
| `/products/:id`  | `PUT`    | Update product by id      |

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
