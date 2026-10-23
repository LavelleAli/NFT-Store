# Ultraverse NFT Marketplace

A responsive NFT marketplace front end built with React. Visitors can browse trending collections, newly listed items and top sellers, explore and sort the full catalog, and open author profiles and item detail pages. All of the content comes from a live REST API.

I built this during a virtual front-end internship. The internship provided a static starter template ([hannamitri/nft-marketplace-starter](https://github.com/hannamitri/nft-marketplace-starter)) with hard-coded placeholder content. My job was to turn it into a dynamic, data-driven app: connect every section to the API, add routing between pages, build loading states and interactive features, and polish the UI with responsive carousels and scroll animations.

**Live demo:** https://nft-store-sepia.vercel.app/

---

## Tech stack

- **React 17** (Create React App)
- **React Router v6** with `HashRouter` so it works on GitHub Pages
- **Axios** for API requests
- **React Slick** for the responsive carousels
- **AOS** (Animate On Scroll) for scroll animations
- **Bootstrap 5** grid and template CSS
- **Vercel** for hosting (GitHub Pages is also supported through `gh-pages`)

## Features

- **Home page**: Hot Collections and New Items carousels, a Top Sellers list, and a Browse by Category section
- **Explore page**: the full NFT catalog with live countdown timers, a "Load more" button, and sorting by price or likes
- **Author pages**: dynamic profiles with the author's details, follower count, a Follow/Unfollow button, and a grid of their NFTs
- **Item detail pages**: dynamic pages showing an NFT's image, price, views, likes, owner and creator
- **Skeleton loading states** on every data-driven section while API requests are in flight
- **Responsive layout** across desktop, tablet and mobile breakpoints

---

## My contributions

Everything below was built on top of the static starter code, one feature branch per section (`lavelle-hotcollections`, `lavelle-newitems`, `lavelle-topsellers`, `lavelle-explore`, `lavelle-author`, `lavelle-itemdetails`), and then merged into `main`.

### Hot Collections (home page)
- Replaced the hard-coded cards with data fetched from the `hotCollections` API endpoint
- Built a responsive React Slick carousel with custom navigation arrows centered on the slider edges, with breakpoints for desktop, tablet and mobile
- Added a skeleton loading carousel that shows while data loads
- Linked each collection to its item detail page and its author profile

### New Items (home page)
- Fetched newly listed NFTs from the `newItems` endpoint and rendered them in a responsive carousel
- Added a live countdown timer for items with an expiry date
- Built skeleton loading cards that match the layout of the real cards

### Top Sellers (home page)
- Fetched and rendered the top sellers list from the `topSellers` endpoint
- Built a skeleton loading state that renders on mount while the API data is fetched
- Linked each seller to their author profile

### Explore page
- Fetched the full catalog from the `explore` endpoint and rendered it into the item grid
- Built live countdown timers for each listing that update every second and stop at zero
- Made the "Load more" button work: it reveals 4 more NFTs per click until every item is shown
- Connected the sort dropdown to the API's filter options (price low to high, price high to low, most liked)
- Linked every card to its author profile and item detail page

### Author page
- Built dynamic routing (`/author/:id`) so each author's profile is fetched from the `authors` endpoint by ID
- Rendered the author's banner, avatar, username, wallet address and NFT collection
- Made the Follow/Unfollow button work, updating the follower count in real time
- Built skeleton loading states for the profile header and the NFT grid

### Item Details page
- Built dynamic routing (`/item-details/:id`) and fetched each NFT from the `itemDetails` endpoint
- Rendered the item's image, title, description, views, likes, price, owner and creator, with links to both authors' profiles
- Built a skeleton loading layout that mirrors the final page
- Split the rendering logic into helper functions to keep the component readable

### Animations and polish
- Installed and configured AOS, and added fade animations to the landing hero, the category tiles and the Explore page
- Wrote per-component CSS files for the new layouts, skeleton styles and responsive tweaks

### Deployment
- Set up `gh-pages` deployment scripts
- Switched from `BrowserRouter` to `HashRouter` so client-side routes work on static hosts
- Deployed to Vercel, and fixed a blank-page bug: the `homepage` field pointed at the GitHub Pages subfolder (`/Lavelle-Internship`), so on Vercel the browser requested the JS and CSS from a path that didn't exist. Setting `homepage` to `"."` makes the build use relative asset paths, which work on Vercel and on GitHub Pages

---

## Getting started

### Prerequisites
- Node.js (v17 or later; the start script uses `--openssl-legacy-provider`)
- npm

### Install and run

```bash
git clone https://github.com/LavelleAli/NFT-Store.git
cd NFT-Store
npm install
npm start
```

The app runs at **http://127.0.0.1:3000**.

### Available scripts

| Command | Description |
| --- | --- |
| `npm start` | Runs the development server with hot reloading |
| `npm run build` | Creates an optimized production build in `build/` |
| `npm run deploy` | Builds the app and publishes it to GitHub Pages (optional) |
| `npm test` | Runs the test runner in watch mode |

## Deployment (Vercel)

The live site is hosted on Vercel and redeploys automatically on every push to `main`. Vercel's default Create React App settings work as-is:

| Setting | Value |
| --- | --- |
| Framework preset | Create React App |
| Build command | `npm run build` |
| Output directory | `build` |

Because the app uses `HashRouter` and `"homepage": "."`, you don't need any rewrite rules, and refreshing any page or opening a deep link (for example `/#/author/123`) works.

## Project structure

```
src/
├── App.jsx                  # Routes and AOS setup
├── pages/                   # Home, Explore, Author, ItemDetails
├── components/
│   ├── home/                # Landing, HotCollections, NewItems, TopSellers, BrowseByCategory
│   ├── explore/             # ExploreItems (grid, sorting, load more)
│   ├── author/              # AuthorItems (an author's NFT grid)
│   ├── timer/               # Countdown timer component (work in progress)
│   └── UI/                  # Shared UI pieces (skeletons)
├── css/                     # Template styles, color schemes and icon fonts
└── images/
```

## Credits

- Starter template by [Hanna Mitri](https://github.com/hannamitri/nft-marketplace-starter)
- API data provided by the internship's NFT cloud functions
- Image credits are listed in [image-credits.txt](image-credits.txt)
