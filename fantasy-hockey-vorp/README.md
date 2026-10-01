# Fantasy Hockey VORP Draft Board

A lightweight, browser-based fantasy hockey draft tool. Upload one or two sets of skater and goalie projections, enter your league’s scoring and roster rules, and generate a sortable Value Over Replacement Player (VORP) board for a points league.

Everything runs locally in your browser — there is no account, server, or upload of your projection data.

## Features

- Import up to two CSV projection files for skaters and up to two for goalies; the second projection is optional
- Configure custom league scoring for any stat column in your files
- Calculate projected fantasy points and VORP by forward, defense, and goalie replacement level
- Account for teams, starter slots, utility slots, and position-specific bench allocation
- Include power-play and short-handed scoring
- Add a defenseman-only bonus for every point scored
- Compare each player's VORP across two projection sets and see their average VORP
- Review games played (GP) and scored projection stats beside the calculated results
- Filter the board to F, D, or G and sort any result/stat column
- Check off drafted players, optionally hide them, and keep those marks after refreshing
- Save and switch between multiple named league/scoring presets
- Export the current rankings as a CSV

## Getting started

1. Download or clone this repository.
2. Open `fantasy-hockey-vorp/index.html` in a modern web browser.
3. Upload at least one File 1 projections CSV. Add a File 1 skater file, a goalie file, or both.
4. Optionally upload File 2 projections to compare a second set. Each file has its own player-name and, for skaters, position-column mapping.
5. Enter your league setup and scoring values.
6. Select **Calculate VORP rankings**.

No installation or web server is required.

## Projection CSV format

The tool is flexible about CSV headers. You choose the player-name and position fields after upload, then enter the relevant CSV header beside each scoring rule.

Each uploaded projection file should have a header row. Skater files should include:

| Required data | Example headers |
| --- | --- |
| Player name | `Player`, `Name` |
| Position | `Pos`, `Position` |
| Scoring stats | `G`, `A`, `SOG`, `PPG`, `PPA`, `HIT`, `BLK` |
| Games played (optional) | `GP` |

Goalie files need a player-name column plus whichever goalie stats your scoring uses, such as `W`, `SV`, `GA`, `SO`, or `SA`. An optional `GP` column is also supported. Goalies are automatically assigned to the G group.

File 1 and File 2 players are matched by player name and roster group. If you upload only one File 2 file type, the corresponding File 1 file supplies the other type when calculating File 2 replacement levels. If a player appears in only one projection, their Average VORP uses the available projection value.

Example skater CSV:

```csv
Player,Pos,G,A,SOG,PPG,PPA,HIT,BLK
Example Center,C,34,58,244,11,20,61,36
Example Defender,D,15,49,178,7,23,92,143
```

Example goalie CSV:

```csv
Player,W,SV,SO
Example Goalie,33,1480,5
```

## Scoring settings

For each scoring rule, provide:

1. A display label
2. The matching CSV column header
3. Fantasy points per unit

For example, with a `G` column and 3 points per goal, use:

| Stat label | CSV column | Points per unit |
| --- | --- | ---: |
| Goals | `G` | 3 |

Leave a rule at zero or remove it if your league does not score that stat. Negative values are supported.

### Defenseman point bonus

Use the `D_PTS` scoring row to award extra fantasy points for defenseman scoring. It calculates goals plus assists only for players classified as D, using the CSV columns configured on the **Goals** and **Assists** rows.

For example, giving `D_PTS` a value of `0.5` adds 0.5 fantasy points for each goal or assist by a defenseman.

## How replacement level works

The app calculates a replacement baseline independently for F, D, and G:

```text
VORP = projected fantasy points − replacement-level fantasy points
```

Replacement rank is based on the roster demand you enter:

```text
position replacement rank = teams × (starters + assigned utility + assigned bench)
```

For example, a 10-team league with 9 F, 5 D, 2 G, and one forward-filled utility slot has default baselines of:

- F100
- D50
- G20

If your league uses benches, assign each bench spot to F, D, or G. For example, three bench slots per team allocated F2 / D0 / G1 changes the pool by 20 additional forwards and 10 additional goalies in a 10-team league.

## Live draft mode

After calculating rankings, the board shows File 1 projected points and VORP, and—when File 2 is uploaded—File 2 projected points and VORP plus Average VORP. GP is shown alongside each projection's scored stat columns. Raw stat columns are limited to stats named in the scoring settings. Numeric projection and stat values are displayed to one decimal place; rank stays an integer.

After calculating rankings:

- Use the F, D, and G checkboxes to narrow the board.
- Check the box beside a player when they are drafted.
- Turn on **Hide drafted** to remove checked players from view.
- Use **Clear drafted marks** to reset the board.

Draft marks are stored locally in the browser, keyed by player name and position.

## Saved league presets

The **Saved league settings** section stores named presets containing:

- Team and roster configuration
- Utility and bench allocation
- All scoring rows and values

Projection files and drafted-player marks are not included in a preset. Presets are stored in browser local storage, so they are available only in the same browser profile on the same device. Clearing browser site data may remove them.

## Privacy and data

The tool is a single HTML file. It does not send projections or saved settings to a server. Your imported CSV data remains in the browser session; named presets and draft marks use local browser storage.

## License

Add a license appropriate to your intended use before publishing or sharing the project.
