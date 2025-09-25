# NuxtCommerce AI Agent Instructions

## Architecture Overview
This is a Nuxt 4 headless storefront for WooCommerce using WordPress + WPGraphQL + WooGraphQL as the backend. The app follows a client-server pattern where:
- **Client-side** (`app/`): Vue components, composables for state management, GraphQL queries
- **Server-side** (`server/`): Nitro API routes that proxy GraphQL requests with caching and WooCommerce session handling
- **Data flow**: Client → Nitro API (`/api/*`) → WPGraphQL → WooCommerce

## Key Patterns & Conventions

### State Management
Use composables in `app/composables/` for reactive state:
- `useCart()`: Manages cart items in localStorage, handles add/update/remove
- `useWishlist()`: Favorites stored in localStorage
- `useCheckout()`: Handles billing/payment submission
- Pattern: Return reactive refs + methods, use `notivue` for user feedback

### GraphQL Integration
- Queries/mutations in `app/gql/` using `gql` template literals
- Server routes in `server/api/` use `cachedEventHandler` for GET requests with SWR caching
- Mutations use `requestMutation()` for WooCommerce session cookie handling
- Example: `server/api/products.get.ts` proxies `app/gql/queries/getProducts.ts`

### API Routes Structure
- GET endpoints: `cachedEventHandler` with `{ swr: true, maxAge: 60 }`
- POST endpoints: Handle WooCommerce sessions via `requestMutation()`
- Route rules in `nuxt.config.ts`: SWR caching for `/categories`, `/favorites`

### Styling & UI
- Tailwind CSS + `@nuxt/ui` components
- Icons via Iconify (`@iconify-json/*`)
- Dark mode support, micro-interactions, skeletons
- Notivue for toast notifications

### Internationalization
- `@nuxtjs/i18n` with locales in `i18n/locales/`
- Supported: en-GB, nb-NO, nl-NL, de-DE
- Use `useLocalePath()` for localized routes

## Development Workflow
- **Package manager**: pnpm (scripts in `package.json`)
- **Environment**: Set `GQL_HOST=https://your-wp-site.com/graphql` in `.env`
- **Dev server**: `pnpm run dev` (HTTP) or `dev:ssl` (HTTPS)
- **Build**: `pnpm run build` → `preview` for static generation
- **Deploy**: `nuxthub deploy` (optional Cloudflare Workers + KV cache)

## Common Tasks
- **Add product feature**: Create component in `app/components/`, add to page, create GraphQL query if needed
- **Modify cart logic**: Update `useCart.ts` composable and related server routes
- **Add API endpoint**: Create file in `server/api/` following existing patterns
- **Style changes**: Use Tailwind classes, reference `@nuxt/ui` components

## File Structure Reference
- `app/pages/`: Nuxt pages (index.vue, categories.vue, product/[id].vue)
- `app/components/`: Reusable UI components (ProductCard.vue, Cart.vue)
- `server/api/`: API routes with caching (products.get.ts, cart/add.post.ts)
- `shared/types/`: TypeScript interfaces (CartItem, ProductNode)</content>
<parameter name="filePath">c:\Users\kamil\Documents\nuxtcommerce\.github\copilot-instructions.md

## Best Practices
Analyze the provided codebase for redundancies, simplifications, and enhancements. Ensure that your analysis aligns with best practices, specifically the SOLID, KISS, and YAGNI principles. 

For your analysis, focus on: 
- Identifying redundant code segments and recommending removals or consolidations. 
- Suggesting ways to simplify complex structures and improve readability. 
- Highlighting areas where enhancements can improve performance or maintainability.
- Ensuring compliance with SOLID principles (Single Responsibility, Open/Closed, Liskov Substitution, Interface Segregation, and Dependency Inversion).
- Applying KISS (Keep It Simple, Stupid) by advising against unnecessary complexities.
- Following YAGNI (You Aren't Gonna Need It) to avoid implementing features that are not currently required.

Be specific in your recommendations, providing examples or code snippets where applicable. 

### Output Format
Deliver the output as a structured report with sections for each principle (SOLID, KISS, YAGNI), summarizing your findings and recommendations. Include any relevant code snippets or explanations to support your analysis.

### Examples
- **Redundant Code**: Identify function duplicates and suggest a consolidated approach. 
- **Simplification**: Recommend using helper functions for repetitive code patterns.
- **Enhancements**: Suggest more efficient algorithms or patterns to improve performance.