# Touchline — Lineup Studio

A self-contained browser-based soccer lineup planner. The interface, styles, and application logic are all in `index.html`; it has no build step or package dependencies.

## Run it

Open `index.html` in a modern browser. The page saves its data in that browser's local storage, so use the same browser and origin to keep working with the same squad.

## Features

- Choose a 4-4-2, 4-3-3, or 4-2-3-1 formation.
- Add players to a squad, then drag them onto the pitch or select an open position and choose a player.
- Move players between the starting lineup and substitutes bench.
- Save, load, and delete named squad lists. A saved squad stores its roster; loading it does not restore a particular lineup arrangement.
- Clear the pitch and substitutes bench together.
- Use the responsive layout on desktop and mobile screens.

## Data and privacy

The current formation, roster, pitch assignments, substitutes, and saved squads are stored locally in the browser under the `touchline-v1` local-storage key. The page does not include a server-side component. It imports DM Sans and DM Mono from Google Fonts when a network connection is available.
