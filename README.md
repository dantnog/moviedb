# MovieDB

An application made with [`SvelteKit`](https://kit.svelte.dev/)

## Starting with

Clone the repo and install the dependences

```bash
git clone https://github.com/dantnog/moviedb.git
cd moviedb
npm install
npm run dev
```

Set your api key on `src/lib/api.js` or in a `.env` file at the root directory

```bash
#example
KEY = "?api_key=<MOVIE-DB-KEY-HERE>"
API = "https://api.themoviedb.org/3"
```

Your can get a free api key on [`TMDB`](https://www.themoviedb.org/faq/account)