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
- **Save to Google Sheet**: appends one row per candidate to a `Results` tab
- **Copy results**: copies a plain-text summary to the clipboard
- Keeps an unsaved draft in the browser, so a reload doesn't lose the scores
- Light and dark mode, phone-width layout

## Running it

The page is plain HTML, CSS and JavaScript with no build step. Open `index.html` in a browser to score candidates and copy results.

Saving to Google Sheets uses the Claude artifact runtime (`window.claude.use("mcp")`) with the Google Sheets connector, so it works only when the page is published as a Claude artifact on claude.ai with the `mcp` capability for the Google Sheets `append_values` and `get_values` tools. Opened anywhere else, the page still scores and copies results, and says that saving needs claude.ai.

## Setting up your sheet

1. Create a Google Sheet with a tab named `Results`.
2. Put headers in row 1. The app writes columns A to J:

   | A | B | C | D | E | F | G | H | I | J |
   |---|---|---|---|---|---|---|---|---|---|
   | Saved at | Date | Candidate | Examiner | GR | LR | DM | PR | IC | Comments |

   Optionally add a total in column K (for example `=SUM(E2:I2)`) and a percentage in column L (`=K2/25`). The "Saved in your sheet" list shows column L, or K if L is empty.
3. Copy the sheet's ID from its URL (the long string between `/d/` and `/edit`) and paste it into `SHEET_ID` near the top of the script in `index.html`, replacing `YOUR_SHEET_ID_HERE`.

## Privacy

Candidate names and scores are stored only in your own Google Sheet and, as an unsaved draft, in your browser. Nothing about candidates is kept in this repository.
