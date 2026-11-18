# C1 Advanced Speaking Scorer

A single-page web app for scoring Cambridge C1 Advanced Speaking. The examiner taps the band descriptor (0 to 5) that best matches the candidate on each of five criteria, and the page totals the score out of 25.

## Criteria

Each criterion is scored 0 to 5 with a weight of 1, for a maximum of 25:

1. Grammatical Resource
2. Lexical Resource
3. Discourse Management
4. Pronunciation
5. Interactive Communication

Bands 1, 3 and 5 have full descriptors. Bands 2 and 4 mean the performance shares features of the bands either side, and 0 is below Band 1.

## Features

- Candidate name, date, examiner and comments
- Live total and percentage in a bar at the bottom of the screen
- **Choose your spreadsheet in the app**: pick one from your Google Drive, paste a link, or create a new one that's set up for you. The choice is remembered in your browser, and **Change** switches it later
- **Save to Google Sheet**: appends one row per candidate to the spreadsheet's `Results` tab
- **Copy results**: copies a plain-text summary to the clipboard
- Keeps an unsaved draft in the browser, so a reload doesn't lose the scores
- Light and dark mode, phone-width layout

## Running it

The page is plain HTML, CSS and JavaScript with no build step. Open `index.html` in a browser to score candidates and copy results.

Saving uses the Claude artifact runtime (`window.claude.use("mcp")`), so it works only when the page is published as a Claude artifact on claude.ai with the `mcp` capability for these connector tools:

- Google Sheets: `get_values`, `append_values`, `get_spreadsheet`, `update_spreadsheet`
- Google Drive: `search_files`, `create_file` (to list your spreadsheets and create a new one; pasting a link works without Drive)

Opened anywhere else, the page still scores and copies results, and says that saving needs claude.ai.

## Choosing your spreadsheet

The first time you open the page it asks where to save results:

- **Use an existing spreadsheet**: pick it from the list (search by name) or paste its link. If it has no `Results` tab, the app offers to add one; your other tabs aren't touched.
- **Create a new one**: makes a Google Sheet in your Drive with a `Results` tab already set up.

The choice is stored in your browser, so it's remembered on your next visit. Tap **Change** at the top of the page to switch. No spreadsheet ID is kept in this repository.

A `Results` tab created by the app has these columns:

| A | B | C | D | E | F | G | H | I | J | K | L |
|---|---|---|---|---|---|---|---|---|---|---|---|
| Saved at | Date | Candidate | Examiner | Grammatical Resource | Lexical Resource | Discourse Management | Pronunciation | Interactive Communication | Comments | Total | Percentage |

Total (out of 25) and Percentage are formulas that fill in for each new row. If you set up a `Results` tab by hand, the app writes columns A to J, and the "Saved in your sheet" list shows column L, or K if L is empty.

## Privacy

Candidate names and scores are stored only in your own Google Sheet and, as an unsaved draft, in your browser. Nothing about candidates is kept in this repository.
