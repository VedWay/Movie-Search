# Movie Search (React + Vite)

Search and discover movies using the TMDB API with a fast, responsive React UI. The app tracks popular search terms in an Appwrite database to display a simple “Trending Movies” section based on what users search most.

## Features

- **Movie search** using TMDB (debounced for better UX)
- **Trending list** powered by Appwrite (counts searches and orders by popularity)
- **Responsive UI** styled with Tailwind CSS
- **Fast dev/build** via Vite

## Tech Stack

- **React 19**, **Vite 6**
- **Tailwind CSS 4**
- **Appwrite JS SDK** for analytics storage
- **react-use** for utilities (debounce)

## Prerequisites

- Node.js 18+ and npm
- TMDB account with a v4 API Read Access Token
- Appwrite project (Cloud or self‑hosted) with a database and collection

## Environment Variables

Create a `.env` file in the project root with the following variables:

```bash
VITE_TMDB_API_KEY=<TMDB_V4_READ_ACCESS_TOKEN>
VITE_APPWRITE_PROJECT_ID=<YOUR_APPWRITE_PROJECT_ID>
VITE_APPWRITE_DATABASE_ID=<YOUR_APPWRITE_DATABASE_ID>
VITE_APPWRITE_COLLECTION_ID=<YOUR_APPWRITE_COLLECTION_ID>
```

Notes:

- The TMDB API in this project uses the v4 Bearer token in the `Authorization` header.
- The Appwrite endpoint is set to `https://nyc.cloud.appwrite.io/v1` in `src/appwrite.js`. If your project uses a different region or self‑hosted URL, update it there.

## Getting Started

Install dependencies:

```bash
npm install
```

Start the dev server:

```bash
npm run dev
```

Build for production:

```bash
npm run build
```

Preview the production build locally:

```bash
npm run preview
```

## Appwrite Setup (Trending Searches)

Create a collection to store search analytics. Suggested attributes:

- `searchTerm` (string)
- `count` (integer)
- `movie_ID` (string or integer)
- `poster_URL` (string)

The app:

- Increments `count` for an existing `searchTerm`, or creates a new document on first search.
- Reads top items using `orderDesc("count")` and `limit(5)` for the Trending section.

Ensure your API keys/permissions allow the client to create, read, and update documents in this collection as appropriate for your use case.

## Project Structure

```
Movie-Search/
├─ public/
├─ src/
│  ├─ components/
│  │  ├─ movieCard.jsx
│  │  └─ search.jsx
│  ├─ appwrite.js         # Appwrite client + trending helpers
│  ├─ App.jsx             # Main app (search, trending, list)
│  ├─ main.jsx
│  ├─ index.css
│  └─ App.css
├─ index.html
├─ package.json
├─ vite.config.js
└─ README.md
```

## Configuration Highlights

- TMDB base URL: `https://api.themoviedb.org/3`
- Bearer Authorization header is set from `VITE_TMDB_API_KEY`
- Debounce: 500ms via `react-use` in `App.jsx`

## Troubleshooting

- If you see “Failed to fetch movies”, verify your TMDB token and that it’s a v4 Read Access Token.
- If Trending is empty, confirm Appwrite IDs and collection attributes and check the region endpoint in `src/appwrite.js`.

## License

This project is provided as-is under your preferred license. If none is specified, consider adding one (e.g., MIT) to clarify usage.
