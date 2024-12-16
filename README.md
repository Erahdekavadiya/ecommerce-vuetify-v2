# Vue.js E-Commerce Product Filter with Vuetify

## Overview

This repository contains a simple yet powerful **E-commerce Product Filter** built using **Vue.js** and **Vuetify**. It allows users to filter products dynamically based on categories (and additional attributes in future). The project demonstrates how to create a filter component in Vue.js with Vuetify's Material Design components, and how to handle dynamic filtering by category.

## Features

- **Dynamic Product Filter:** Users can filter products by category.
- **Vuetify Integration:** Leveraging Vuetify components to build a responsive, Material Design-based UI.
- **Vue.js:** Utilizing Vue.js reactivity system to efficiently update product listings when filters are applied.
- **API Integration:** Fetches product data from an API and applies selected filters.
- **Cart Integration:** Allows adding products to a cart and viewing the cart in a side drawer.

## Installation

### Prerequisites

To run this project, you'll need:

- **Node.js** (preferably the latest LTS version)
- **Vue CLI** (for easier Vue project setup)
- **Vuetify** installed in your project

### Setup

1. **Clone the repository:**

   ```bash
   git clone https://github.com/yourusername/vue-vuetify-ecommerce-filter.git
   cd vue-vuetify-ecommerce-filter
   ```

2. **Install dependencies:**

   Use npm or yarn to install the project dependencies:

   ```bash
   npm install
   # or
   yarn install
   ```

3. **Run the application:**

   Start the Vue development server:

   ```bash
   npm run serve
   # or
   yarn serve
   ```

   The app will be available at `http://localhost:8080`.

## Project Structure

- `src/`
  - `components/`
    - `ProductFilter.vue`: The component that handles the product filter UI.
    - `ProductList.vue`: Displays the filtered product list.
    - `CartDrawer.vue`: Side drawer for the shopping cart.
  - `App.vue`: Main component that ties everything together.
  - `assets/`: Contains static assets like images and icons.
  - `router/`: Contains Vue Router setup for navigation.
  - `store/`: Vuex store to manage global state (cart and products).
  
## Usage

1. **Filter by Category:**
   The product filter is implemented using Vuetify's `v-select` component. You can filter products by selecting a category from the dropdown. The filtered products will be displayed dynamically without the need to reload the page.

2. **Add to Cart:**
   The app includes a shopping cart feature. When a user adds a product to the cart, it is saved in the `cartItems` array and displayed in a side drawer.

3. **Cart Drawer:**
   The cart drawer displays all the items added to the cart, and users can remove items directly from the cart.

## API Integration

This app is set up to fetch products from a mock API. Replace the API endpoint in the `fetchProducts()` method inside `App.vue` to use your own API for fetching product data.

```javascript
async fetchProducts() {
  const response = await axios.get('https://api.example.com/products');
  this.products = response.data;
}
```

### Example API Response

```json
[
  {
    "id": 1,
    "name": "Product 1",
    "category": "Electronics",
    "price": 100,
    "image": "https://example.com/product1.jpg"
  },
  {
    "id": 2,
    "name": "Product 2",
    "category": "Apparel",
    "price": 50,
    "image": "https://example.com/product2.jpg"
  }
]
```

## Contributing

1. Fork the repository.
2. Create a new branch for your feature or fix.
3. Make your changes.
4. Commit your changes and push to your fork.
5. Create a pull request.

## License

This project is open-source and available under the [MIT License](LICENSE).

## Acknowledgements

- **Vue.js** - A progressive JavaScript framework for building user interfaces.
- **Vuetify** - A Material Design framework for Vue.js.

---