# Next.js Movies Exploration

This document will track changes made to this fork of the [TasteJS/Movies](https://tastejs.com/movies/) application built in Next.js. My intent is primarily to learn and share my insights in three usage contexts:

 1. Hosting - using Azure (SWA + App Insights)
 2. Testing - using Playwright + Lighthouse
 3. Experience - using GitHub Actions + Codespaces + Copilot

 In the process I hope to also fulfill a fourth objective - learning better Next.js development practices by `deconstructing` the project, one step at a time - then `extending` it with some new feature.

---

## Views

The Movies App has the following Views - the first 6 are general to all versions, the last 4 use specific Next.js features.

 * Popular Movies - with pagination or infinite scroll
 * Individual Movies - with recommendations, cast, and more.
 * Cast member/Actor with history
 * Categories - popular, TV/Movies and more.
 * Search - find, filter, sort movies. Paginated.
 * Authentication with TMDB - login, logout (Next.js)
 * Lists - create new lists (Next.js)
 * Lists - view all your saved lists (Next.js)
 * Lists - add/remove/edit lists (Next.js)

---

## Components

> 🚧 TODO 

I'll update this section with the list of React Components that exist in the codebase.

---

## API

The Movies App uses the [The Movie Database (TMDB)](https://www.themoviedb.org/) API. Relevant resources:
 - [API Documentation](https://developers.themoviedb.org/3/getting-started/introduction)
 - [Open API Specification (OAS)](https://api.stoplight.io/v1/versions/9WaNJfGpnnQ76opqe/export/oas.json)
 - [API Wrappers & Libraries](https://www.themoviedb.org/documentation/api) for various languages.
 - [API on Postman](https://www.postman.com/devrel/workspace/ac6d53a3-844d-4092-8cd3-59d1a11d243d/overview)
 - [API Docs on Postman](https://www.postman.com/devrel/workspace/tmdb-api/documentation/13191452-e12a1487-f709-47b4-9f55-c11c8e0daea2)

 ---

## Routes

The [Next.js Movies Demo](https://next-movies-zeta.vercel.app/?category=Popular&page=1) is hosted on Vercel and currently has the following routes accessible as _guest_ user.

| Route | Parameters | Description |
|:---| :---|:---|
| / |  ?category=Popular&page=1| Home |
| /movie | ?id=436270&page=1 | Movie Details |
| /person | ?id=18918&page=1 | Cast Member Details |
| /genre | ?id=12&name=Adventure&page=1 | Category |
| /search | ?searchTerm=test&page=1 | Search Results (for query from navbar) |
| | | |

> TODO: List auth-driven routes

The Demo also has a set of authenticated routes, which require user to login before they can be accessed:

| Route | Parameters | Description |
|:---| :---|:---|
| | | |
| | | |
| | | |
| | | |

For any route that is invalid or inaccessible (i.e., route exists but not accessible as guest), there is a default `404` page shown.



---