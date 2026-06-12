# PROJECT_MAP.md: Shopify Theme Analysis

## 1. Theme Name
* **Theme Name**: Dawn
* **Theme Schema Version**: 15.4.1 (Shopify Online Store 2.0 architecture)
* **Permanent Store Domain**: `19usmg-pb.myshopify.com` (`dinyx.in`)

---

## 2. Theme Structure
This theme follows the standard Shopify Online Store 2.0 structure:
* `assets/`: Contains styling stylesheets (CSS), behaviors scripts (JS), and images/icons (SVG).
* `config/`: Configuration files for theme settings (`settings_data.json` and `settings_schema.json`).
* `layout/`: Main structural wrapper layout templates (e.g. `theme.liquid`).
* `locales/`: Localization language JSON files (e.g., `en.default.json`).
* `sections/`: Reusable dynamic layout sections (e.g., `main-product.liquid`, `header.liquid`, `footer.liquid`).
* `snippets/`: Smaller reusable Liquid snippets called by sections (e.g., `buy-buttons.liquid`, `product-variant-picker.liquid`, `product-variant-options.liquid`, `swatch.liquid`).
* `templates/`: Page definitions mapped to layout JSON schemes (e.g. `templates/product.json`, `templates/index.json`).

---

## 3. Product Page Files
The main product page features are rendered and controlled by:
* **Section Layout**: [sections/main-product.liquid](file:///c:/Users/midhl/Downloads/Dinyx/sections/main-product.liquid) (defines blocks like title, price, quantity selector, variant picker, and buy buttons).
* **Styles**: [assets/section-main-product.css](file:///c:/Users/midhl/Downloads/Dinyx/assets/section-main-product.css) and [assets/base.css](file:///c:/Users/midhl/Downloads/Dinyx/assets/base.css).
* **Variant Picker Snippet**: [snippets/product-variant-picker.liquid](file:///c:/Users/midhl/Downloads/Dinyx/snippets/product-variant-picker.liquid) (coordinates whether dropdowns or radio pills are rendered).
* **Variant Option Values**: [snippets/product-variant-options.liquid](file:///c:/Users/midhl/Downloads/Dinyx/snippets/product-variant-options.liquid) (loops through each individual option and prints the markup).
* **Swatches**: [snippets/swatch.liquid](file:///c:/Users/midhl/Downloads/Dinyx/snippets/swatch.liquid) and [snippets/swatch-input.liquid](file:///c:/Users/midhl/Downloads/Dinyx/snippets/swatch-input.liquid) (handles native swatch values).
* **Buy Buttons**: [snippets/buy-buttons.liquid](file:///c:/Users/midhl/Downloads/Dinyx/snippets/buy-buttons.liquid) (renders the form and "Add to Cart" or "Buy It Now" buttons).
* **Product Media Gallery**: [snippets/product-media-gallery.liquid](file:///c:/Users/midhl/Downloads/Dinyx/snippets/product-media-gallery.liquid) (manages images, videos, and zoom on hover).
* **JavaScript Behaviors**: [assets/product-info.js](file:///c:/Users/midhl/Downloads/Dinyx/assets/product-info.js) (manages state updates when options change) and [assets/product-form.js](file:///c:/Users/midhl/Downloads/Dinyx/assets/product-form.js) (submits additions to cart via AJAX).

---

## 4. Variant System Implementation
Variant change events in this version of Dawn work as follows:
* Option selections are wrapped in a `<variant-selects>` custom element defined in [assets/global.js](file:///c:/Users/midhl/Downloads/Dinyx/assets/global.js) (line 1063).
* When a change occurs, the custom element publishes a `PUB_SUB_EVENTS.optionValueSelectionChange` event.
* The `<product-info>` element defined in [assets/product-info.js](file:///c:/Users/midhl/Downloads/Dinyx/assets/product-info.js) listens to this event.
* It fetches the updated section markup asynchronously using standard Shopify Section Rendering APIs (e.g. `?variant=xxxx&section_id=xxxx`).
* It swaps the price, inventory status, product SKU, and product gallery images dynamically via Javascript (`HTMLUpdateUtility.viewTransition` or `this.updateMedia`).

---

## 5. CSS Files
* **Global Core Stylesheet**: [assets/base.css](file:///c:/Users/midhl/Downloads/Dinyx/assets/base.css)
* **Product Page Stylesheet**: [assets/section-main-product.css](file:///c:/Users/midhl/Downloads/Dinyx/assets/section-main-product.css)
* **Cart Drawer Stylesheet**: [assets/component-cart-drawer.css](file:///c:/Users/midhl/Downloads/Dinyx/assets/component-cart-drawer.css)
* **Card Stylesheet**: [assets/component-card.css](file:///c:/Users/midhl/Downloads/Dinyx/assets/component-card.css)
* **Swatch Input Stylesheet**: [assets/component-swatch-input.css](file:///c:/Users/midhl/Downloads/Dinyx/assets/component-swatch-input.css)
* **Swatch Stylesheet**: [assets/component-swatch.css](file:///c:/Users/midhl/Downloads/Dinyx/assets/component-swatch.css)

---

## 6. JavaScript Files
* **Core Global JS**: [assets/global.js](file:///c:/Users/midhl/Downloads/Dinyx/assets/global.js) (contains custom element components, drawer logic, menu handling).
* **Product Updates Handler**: [assets/product-info.js](file:///c:/Users/midhl/Downloads/Dinyx/assets/product-info.js) (updates product states on variant changes).
* **Cart Interactions**: [assets/cart-drawer.js](file:///c:/Users/midhl/Downloads/Dinyx/assets/cart-drawer.js) and [assets/cart.js](file:///c:/Users/midhl/Downloads/Dinyx/assets/cart.js).

---

## 7. Mobile Navigation Files
* **Section**: [sections/header.liquid](file:///c:/Users/midhl/Downloads/Dinyx/sections/header.liquid) (contains header-drawer block settings).
* **Snippet**: [snippets/header-drawer.liquid](file:///c:/Users/midhl/Downloads/Dinyx/snippets/header-drawer.liquid) (markup for mobile hamburger menu navigation).
* **CSS**: [assets/component-menu-drawer.css](file:///c:/Users/midhl/Downloads/Dinyx/assets/component-menu-drawer.css) and [assets/component-list-menu.css](file:///c:/Users/midhl/Downloads/Dinyx/assets/component-list-menu.css).
* **JS**: [assets/global.js](file:///c:/Users/midhl/Downloads/Dinyx/assets/global.js) (`MenuDrawer` and `HeaderDrawer` classes).

---

## 8. Best Files to Modify for Features

### A. Color Redesign (Store colors to #111111 Primary, #FFFFFF Secondary, #FF5A5F Accent)
* **Best Files**:
  * [config/settings_data.json](file:///c:/Users/midhl/Downloads/Dinyx/config/settings_data.json) (update standard Shopify color schemes like scheme-1, scheme-2, etc., directly to map to the new colors).
  * [assets/base.css](file:///c:/Users/midhl/Downloads/Dinyx/assets/base.css) (add custom CSS variables override or styling for headers, buttons, Badges, and mobile menu color matching).

### B. Color Swatches (Modern swatches fallback for options named "Color" or "Colour")
* **Best Files**:
  * [snippets/product-variant-picker.liquid](file:///c:/Users/midhl/Downloads/Dinyx/snippets/product-variant-picker.liquid) (force option type to `swatch` if option name is "Color" or "Colour" even if native swatches are not filled).
  * [snippets/swatch.liquid](file:///c:/Users/midhl/Downloads/Dinyx/snippets/swatch.liquid) (add color fallback logic that outputs hex color values or custom CSS color variables matching option text, e.g. `var(--color-swatch-midnight-blue, midnightblue)`).
  * [assets/base.css](file:///c:/Users/midhl/Downloads/Dinyx/assets/base.css) (declare CSS variables for non-standard color values, e.g., `--color-swatch-midnight-blue: #191970`).

### C. Delivery Estimation (Estimated delivery: Current + 5 to 7 days, below price)
* **Best Files**:
  * [sections/main-product.liquid](file:///c:/Users/midhl/Downloads/Dinyx/sections/main-product.liquid) (render delivery estimator directly under the price block).
  * [assets/section-main-product.css](file:///c:/Users/midhl/Downloads/Dinyx/assets/section-main-product.css) (add custom styles matching premium look).

### D. WhatsApp Order Form (Selected products replace ATC with form to order on WhatsApp)
* **Best Files**:
  * [snippets/buy-buttons.liquid](file:///c:/Users/midhl/Downloads/Dinyx/snippets/buy-buttons.liquid) (conditional check: if product is tagged for WhatsApp order, render fields [Name, Phone, Address, Size] and "Book on WhatsApp" button, hiding the standard Cart buttons).
  * [sections/main-product.liquid](file:///c:/Users/midhl/Downloads/Dinyx/sections/main-product.liquid) (add configurations for WhatsApp phone number).
  * [assets/base.css](file:///c:/Users/midhl/Downloads/Dinyx/assets/base.css) (style the form and fields, touch targets, and sticky bottom navigation for mobile).
