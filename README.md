# Lambertville XR

Website for the Lambertville XR walking tour.

## Hosting

Production is served from the custom domain [https://flowingtogether.lambertvillenj.org](https://flowingtogether.lambertvillenj.org).

The static build is deployed to GitHub Pages, and GitHub Pages maps that content to the custom domain. Because production is served from the domain root, the deployment workflow intentionally uses `NUXT_APP_BASE_URL=/`.

If you need to preview a fork or a repo-scoped GitHub Pages deployment, use a repo subpath base URL for that build only. Do not change the production workflow away from `/` unless the production hosting model changes.

## Developing

### Prerequisites

- Make sure you have Node.js 20 installed.
- Clone this repository
- Run

  ```bash
  npm i
  ```

### Hosting a local server

Run

```bash
npm run dev
```

### Hosting a local server live

If you need to test the website from different devices, it's best to host the server live through a proxy. This repo has scripts to host from ngrok.

#### Using ngrok

Make sure you have [ngrok](https://ngrok.com/product) installed and have registered an ngrok account and setup your ngrok token.

Run

```bash
npm run dev
```

In a separate terminal, run

```bash
npm run ngrok
```

> **NOTE:**
>
> We have a separate command for ngrok because it doesn't display any output when its
> used with the "concurrently" npm command.

### Building the website

Run

```bash
npm run build
```

The static website should be built inside of the `.output/public` folder.

#### Settings

The settings for building the website can be configured by environment variables.

- `HIDE_DEMOS`
  - If set to `true`, then the demos will not be built. This should be enabled for production builds.
- `META_URL`
  - If set, then all social media previews will link to this URL. This should be set for production builds.
- `STORYMAP_URL`
  - If set, then the story map url on the site will link to this URL. This should be set for production builds.
- `NUXT_APP_BASE_URL`
  - Production should remain `/` because the live site is served from the custom domain root.
  - For fork previews or repo-scoped GitHub Pages builds, this can be set to `/<repo-name>/`.

#### Site URLs

Navigating to a site with `?ar=true` after its url will automatically enter AR mode when loaded. When making actual site QR codes, you should include this query text to the end of the site urls to ensure users are sent to AR mode immediately after they open the site from the QR code.

```
Ex.

https://flowingtogether.lambertvillenj.org/sites/site-1/?ar=true
https://flowingtogether.lambertvillenj.org/sites/site-2/?ar=true
https://flowingtogether.lambertvillenj.org/sites/site-3/?ar=true
...
```

### Credits

- "Low Poly Bicycle" (https://skfb.ly/6VSyo) by tolotedesign is licensed under Creative Commons Attribution (https://creativecommons.org/licenses/by/4.0/).
- "Chevrolet Camaro SS Coupe" (https://free3d.com/3d-model/chevrolet-camaro-ss-coupe-373476.html) by thmacr
- "Debris Concrete Junk" (https://sketchfab.com/3d-models/debris-concrete-junk-3f161258ebde4bd8afc98e57c9e06890) by matousekfoto
- "Stop Sign Free" (https://skfb.ly/6prBt) by MathewMantas is licensed under Creative Commons Attribution (https://creativecommons.org/licenses/by/4.0/).
- "Low poly tree" (https://skfb.ly/6sSUr) by Anthony Van Dosselaer is licensed under Creative Commons Attribution-NonCommercial (https://creativecommons.org/licenses/by-nc/4.0/).
- "Lowpoly Tree" (https://skfb.ly/KLAv) by dionne is licensed under Creative Commons Attribution (https://creativecommons.org/licenses/by/4.0/).
- "Low poly tree" (https://skfb.ly/6YTBS) by Chenuka Wijesundara is licensed under Creative Commons Attribution (https://creativecommons.org/licenses/by/4.0/).
- "Game ready bush" (https://skfb.ly/oE99R) by H U N T E R 7 is licensed under Creative Commons Attribution (https://creativecommons.org/licenses/by/4.0/).
