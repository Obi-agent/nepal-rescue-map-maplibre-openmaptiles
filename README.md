# Nepal Rescue Map – MapLibre Edition

This project provides an interactive trekking and rescue‑point map for Nepal using **MapLibre GL JS**.  It replaces the original Leaflet/Mapbox implementation with an entirely open‑source stack based on [MapLibre](https://maplibre.org/) and [OpenMapTiles](https://openmaptiles.org/).

## Features

* **Vector basemap** provided by the MapLibre demo style (`demotiles.maplibre.org`), showing topography and roads without requiring API keys.
* **Nine major trekking routes** drawn as polylines, with colours and metadata taken from open trekking data.
* **35 rescue points** plotted as circular markers.  Each point shows its name, altitude, approximate coordinate flag, associated routes and operational notes when clicked.
* **Route selection** via buttons: click a route name to isolate its path and relevant rescue points; click *Show All Routes* to return to the global view.
* **Summary cards** reporting the total number of routes, points, altitude range, high‑altitude points, approximate coordinates and export formats.
* **Search** to filter rescue points by name, route or note.  The list updates live and the map hides non‑matching markers.
* **Reset view** button to return to the default map centre and zoom.

## Running locally

To run the map locally you only need a web browser.  Clone this repository and open `index.html` in your browser.  All dependencies are loaded from CDNs (MapLibre GL JS and its stylesheet), and the data is packaged as static JSON in `assets/data.js`.  No build step or API keys are required.

```
git clone https://github.com/Obi-agent/nepal-rescue-map-maplibre-openmaptiles.git
cd nepal-rescue-map-maplibre-openmaptiles
open index.html
```

Because MapLibre loads its basemap style from an external domain (`demotiles.maplibre.org`), you will need an internet connection to display the tiles.

## Editing the map style

The vector basemap is defined by a Mapbox Style JSON file.  You can modify colours, labels or layers using the excellent [Maputnik](https://maputnik.github.io/) visual style editor:

1. Open [Maputnik](https://maputnik.github.io/) in your browser.
2. Choose **Open** → **Open URL** and paste `https://demotiles.maplibre.org/style.json`.
3. Edit the style as desired – change colours, hide layers, adjust fonts, etc.
4. Save the modified style JSON to your computer.
5. In `assets/app.js`, change the `styleUrl` variable to the path of your customised style (for example, host the JSON yourself or embed it as a data URI).

See `docs/MAPUTNIK_EDITING_GUIDE.md` for step‑by‑step guidance.

## Data sources

The trekking routes and rescue points were derived from public KML and CSV files and converted into JSON for the map.  They are stored in `assets/data.js` so the map loads instantly without extra requests.

* `ROUTES` – array of route objects with id, name, colour, textual description and waypoints.
* `RESCUE_POINTS` – array of rescue points with id, name, latitude/longitude, altitude, approximate flag, associated route names, route colours and operational notes.

Feel free to modify these arrays in `assets/data.js` to add or correct points or update route metadata.

## Folder structure

```
maplibre_repo/
├── index.html         – HTML entry point
├── assets/
│   ├── styles.css     – CSS for layout and components
│   ├── data.js        – Static data for routes and rescue points
│   └── app.js         – JavaScript to build the map and UI
├── data/
│   ├── routes.json    – Original JSON source for routes
│   ├── rescue_points.json – Original JSON source for rescue points
│   └── nepal_routes_and_rescue_points.kml – Original KML data
├── docs/
│   └── MAPUTNIK_EDITING_GUIDE.md – guide to editing the basemap style
└── GITHUB_UPLOAD_GUIDE.md – explanation for uploading this project to GitHub
```

## License

This project is released under the MIT License.  See `LICENSE` for details.
