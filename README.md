# Кропкі (kropki_web)

Static interactive map of historic buildings in **Mahilioŭ (Магілёў)**, built for GitHub Pages.

- Leaflet + white Carto Positron (OSM) tiles — no Mapbox / no backend
- Data imported from a Notion HTML/CSV export
- Pin icons by building type and preservation status

Live (after Pages is enabled): `https://colorage.github.io/kropki_web/`

## Create the GitHub repo

This project is meant to live at **`colorage/kropki_web`**. If you only have this branch on another repository, publish it with:

```bash
gh repo create colorage/kropki_web --public --source=. --remote=origin --push
# or, from an existing clone of this branch:
git remote add kropki https://github.com/colorage/kropki_web.git
git push -u kropki HEAD:main
```

Then enable **Settings → Pages → Source: GitHub Actions**.

## Develop

```bash
npm install
NOTION_DIR=~/Downloads/notion npm run import   # preferred
# or, if Notion export is missing:
npm run bootstrap
npm run dev
```

## Import from Notion

Export the Notion workspace as HTML (with assets). Point the importer at the folder that contains `Кропкі/` (or the `Кропкі` folder itself):

```bash
NOTION_DIR=~/Downloads/notion npm run import
```

This writes:

- `public/data/buildings.json`
- `public/data/tours.json`
- `public/data/zones.json`
- `public/data/icons.json`
- compressed images under `public/media/`

The cloud build may ship with an OSM bootstrap + a tiny Notion sample so the map is not empty. Re-run the import locally with your full `~/Downloads/notion` export to replace it with all ~180 buildings, photos, and descriptions.

## Deploy

Push to `main`. GitHub Actions builds with Vite `base: '/kropki_web/'` and deploys to GitHub Pages.

## UI improvements vs the old CRA app

1. Correct city center (Mahilioŭ, not Minsk)
2. Pins wired by type + status
3. Search restored
4. Detail panel with Notion descriptions
5. Status / type filters + legend
6. Mobile-friendly header and bottom sheet
7. No Mapbox keys
8. Fully static JSON + media
9. Relative asset paths for project Pages
10. `lang="be"` and proper meta
