# Next.JS Movies Exploration

## Objectives

Explore the repo with three goals in mind:
 - Deploy the app to Azure Static Web Apps
 - Integrate e2e testing with Playwright
 - Deconstruct the app, and reconstruct using TDD

 Note - there are a couple of projects out there that combine Next.js and TMDB
 - [Taste.js Movies](https://tastejs.com/movies/)
 - [Next.js Movies ](https://github.com/transitive-bullshit/next-movie)

---

## Day 01: 

Walking through default README.md instructions to validate existing application on my local dev environment.

### 1.1 Build The App

```bash
$ cd next-movies-explore
$ nvm use 16 
Now using node v16.18.0 (npm v8.19.2)
$ npm install
```

Resulted in errors: 
```
Found: react@17.0.2 
... 
Could not resolve dependency:
peer react@"^16.8.4" from react-select-search@2.2.4
...
npm ERR! Fix the upstream dependency conflict, or retry
npm ERR! this command with --force, or --legacy-peer-deps
npm ERR! to accept an incorrect (and potentially broken) dependency resolution.
```

Opted to use --legacy-peer-deps

```bash
$ npm install --legacy-peer-deps
```
### 1.2 Preview The App

Let's preview existing build:

```bash
$ npm run dev

> movie-app@0.1.0 dev
> next dev -p 8080

ready - started server on 0.0.0.0:8080, url: http://localhost:8080
```

This should give you something like this. The error message is because we have not set up the TMDB API yet - but it validates that build for the Next.js app works.

![Init App Preview](./app-init-preview.png)


### 1.3 Deploy The App to SWA

Before we fix the TMDB API issue, let's first see if we can deploy this app _as is_ to Azure Static Web Apps.

_I'll use the VS Code approach for now, but may later delete resources and use the `swa deploy` option so we can establish a command-line step in `package.json` for future workshops or CI/CD needs_.

This sets up the [.github/workflows](../.github/workflows/azure-static-web-apps-lemon-ground-0d54e8a10.yml) file for automating build/deploy to Azure Static Web Apps. To learn what configuration options were used, see _this_ segment of the workflow.

```yml
# For more information regarding Static Web App workflow configurations, please visit: https://aka.ms/swaworkflowconfig
app_location: "/" # App source code path
api_location: "api" # Api source code path - optional
output_location: "" # Built app content directory - optional
```

The Workflow is set up to run on every commit (push) or PR (pull) request to the repo. 
> The actions status can be found [here](https://github.com/30DaysOf/next-movies-explore/actions/workflows/azure-static-web-apps-lemon-ground-0d54e8a10.yml)

Check VS Code Azure Extensions sidebar, or visit your [Azure Portal](https://portal.azure.com) page to determine the hosted URL for your web app.

> This app is hosted at [this URL](https://lemon-ground-0d54e8a10.2.azurestaticapps.net/)

In the initial run, you will see that the actions fail (for the same reason as our local build - the dependency resolution problem). How can we configure CI/CD to enforce this?

We'll use a hack [based on this GitHub issue discussion](https://github.com/npm/rfcs/discussions/283?sort=old) for now.  
 - Add an [`.npmrc`](./.npmrc) file to this project with `legacy-peer-deps=true`
 - Now `npm install` will just work without you having to explicitly setup options
 - Commit to GitHub, and this should now get enforced in the CI/CD process as well.

> Note that this solution is **NOT IDEAL**. The **right approach** would be to resolve the dependency conflicts by submitting issues to fix it upstream, or fork/fix-ing them in a local copy. Since this is just a demo project, I won't go that route yet.

