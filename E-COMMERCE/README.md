# Orbit Market: Modern E-commerce Storefront

A clean, minimal storefront built as a **single self-contained HTML file** (no build step, no dependencies). It pulls its catalogue from [FakeStoreAPI](https://fakestoreapi.com/products) and includes a persistent cart, wishlist, full-screen product pages and a simulated checkout.

## Quick start

1. Download `storefront.html`.
2. Open it in any modern browser (double-click, or serve it from any static host such as GitHub Pages or Vercel).

That's it. When opened as a local file or from your own site, the page loads live data and real product photos from FakeStoreAPI.

## Features

**Shopping**
- Live product catalogue from `https://fakestoreapi.com/products`
- Product cards with star ratings, review counts, prices and badges (*Top rated*, *Best seller*, *Great value*)
- Category filters: All, Electronics, Jewelry, Clothing, Saved
- Live search and sorting (Featured, Top rated, price low to high, price high to low)
- Full-screen product page with the complete description, rating, SKU, availability, delivery info, quantity picker and related products
- Wishlist (heart on any product), saved across visits

**Cart and checkout**
- Slide-out cart drawer with a badge counter in the navbar
- `addToCart()`, `removeFromCart()`, `updateQuantity()` and `calculateTotal()`
- Quantity increment and decrement (going to 0 removes the item)
- Subtotal, tax, shipping and total, with a free-shipping progress bar
- Promo codes: `SAVE10` (10% off) and `WELCOME` (15% off)
- Cart persists across refreshes
- Simulated checkout modal with form validation and an order confirmation (no payment is taken)

**Design and motion**
- Neutral, professional palette with automatic light/dark mode and a manual toggle
- Hero banner that rotates through top-rated products from the catalogue
- Trending row, category tiles, scrolling offers ticker, benefits strip and footer
- Scroll-reveal sections, staggered card entrance, hover effects, count-up stats, scroll progress bar
- Fly-to-cart animation and cart badge bump
- Hand-drawn SVG product illustrations used as a fallback whenever an image can't load
- Fully responsive; animations are disabled for users who prefer reduced motion

## Configuration

Edit the constants near the top of the `<script>` block:

| Constant | Default | Purpose |
|---|---|---|
| `TAX_RATE` | `0.08` | Tax applied after discounts |
| `FREE_SHIP` | `100` | Subtotal at which shipping becomes free |
| `SHIP_FEE` | `7.99` | Flat shipping fee below the threshold |
| `CODES` | `SAVE10`, `WELCOME` | Promo codes and their discount rates |
| `API` | FakeStoreAPI URL | Product data source |

## How it works

- **Data:** the page fetches the API on load. If the request fails, it falls back to a built-in copy of the 20 catalogue products (with full descriptions), so the store always renders.
- **Categories:** the API's `men's clothing` and `women's clothing` are grouped under **Clothing**, and `jewelery` is displayed as **Jewelry**.
- **Storage:** the cart and wishlist are kept in `localStorage` (keys `orbit-cart` and `orbit-wish`). All storage access is wrapped in `try/catch`, so the store still works if storage is unavailable.
- **Deep links:** each product page has its own address, for example `storefront.html#p5` opens product 5.
- **Keyboard:** `Esc` closes the product page, cart and dialogs.

## Project structure

```
storefront.html   # markup, styles and script, all in one file
README.md
```

Inside `storefront.html`: CSS (theme tokens, layout, animations) → HTML shell → JavaScript (data, cart logic, rendering, product page, hero/trending, event handling, boot).

## Notes and limitations

- **Images on sandboxed hosts:** some hosting environments (for example claude.ai's hosted artifacts) block images and API calls to other sites. There, the store uses the built-in product data and the SVG illustrations instead of photos. Open the file locally or host it yourself to see the real photos.
- **Checkout is a demo:** orders are not sent anywhere and no payment is processed.
- **Reviews, stock and delivery times** on the product page are display content, not data from the API.
- Requires a modern browser (Chrome, Edge, Firefox, Safari from the last few years).

## Customising

- **Branding:** change the "Orbit Market" text in the `.logo` element and the colour tokens in the `:root` block.
- **Catalogue:** point `API` at another endpoint that returns the same fields (`id`, `title`, `price`, `description`, `category`, `image`, `rating.rate`, `rating.count`), or edit the built-in fallback data.
- **Illustrations:** add or edit shapes in the `SHAPES` object and map product IDs to them in `KIND`.

## Credits

Product data and images from [FakeStoreAPI](https://fakestoreapi.com/).
