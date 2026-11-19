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
- **Choose where results go, in the app**: a Google Sheet in your own Drive (pick one or create one) or an Excel `.xlsx` file. The choice is remembered in your browser, and **Change** switches it later
- **Save result**: adds one row per candidate to the `Results` tab
- **Copy results**: copies a plain-text summary to the clipboard
- Keeps an unsaved draft in the browser, so a reload doesn't lose the scores
- Light and dark mode, phone-width layout

## Running it

The page is plain HTML, CSS and JavaScript with no build step. It can run in three ways:

| Where it runs | Google Sheets | Excel `.xlsx` |
|---|---|---|
| A public website (for example GitHub Pages) with the `GOOGLE` settings filled in | Each person signs in with their own Google account | Yes |
| A public website without the `GOOGLE` settings, or `index.html` opened from disk | No | Yes |
| A Claude artifact on claude.ai | Through the owner's Claude connectors | Yes, kept in the browser with a Download button |

### Excel files

- **Chrome and Edge on a computer**: open or create an `.xlsx` file and the page saves each result straight into it. The browser asks once for permission to edit the file. Use a workbook just for these results: the page rewrites the file when it saves, which can drop charts, pictures or pivot tables.
- **Other browsers, phones and tablets, and the Claude artifact**: the workbook is kept in the browser. Tap **Download** to get the updated file. Clearing the browser's site data removes this copy, so download it regularly.

Excel support uses [ExcelJS](https://github.com/exceljs/exceljs), loaded from jsDelivr when needed.

### Google sign-in setup (website)

The website asks for Google's `drive.file` permission only: the page can open just the spreadsheets each person picks in Google's file picker, or creates from the page. It never sees the rest of their Drive. This permission doesn't need Google's app review.

1. Go to [console.cloud.google.com](https://console.cloud.google.com), and create a project (for example "C1 Speaking Scorer").
2. In **APIs & Services → Library**, enable **Google Sheets API**, **Google Drive API** and **Google Picker API**.
3. In **Google Auth Platform** (the OAuth consent screen), fill in the app name and your email, choose **External** as the audience, and add the `.../auth/drive.file` scope under **Data access**. Then, under **Audience**, tap **Publish app** so anyone can sign in, not only test users.
4. In **Clients**, create an **OAuth client ID** of type **Web application**. Under **Authorized JavaScript origins**, add your site's address, for example `https://tsiqueira81.github.io`. Copy the client ID.
5. Copy the **project number** from the project's settings page.
6. Paste the client ID and project number into `GOOGLE` near the top of the script in `index.html`. They're safe to publish: Google only accepts sign-ins from the addresses you listed.
7. In **Google Auth Platform → Branding**, fill in the home page and privacy policy links (`.../privacy.html`) and add your site's domain under authorized domains. Google needs these before you can publish the app.

No API key is needed: Google's file picker works with each person's sign-in alone.

### Publishing on GitHub Pages

In the repository's **Settings → Pages**, set **Source** to **Deploy from a branch**, choose `main` and `/ (root)`, and save. The site appears at `https://<your-user>.github.io/c1-speaking-assessment/` after a minute.

### As a Claude artifact

Published as a Claude artifact, the page saves to Google Sheets through the owner's claude.ai connectors. It needs the `mcp` capability for Google Sheets `get_values`, `append_values`, `get_spreadsheet`, `update_spreadsheet` and Google Drive `search_files`, `create_file`, and the `downloads` capability for Excel downloads. Other people who open a shared artifact can't use the owner's connectors, so for them only Excel works. Use the website to let everyone save to their own Google Drive.

## Choosing where results go

The first time you open the page it asks where to save results:

- **Google Sheet**: pick one (on the website, through Google's file picker; in the artifact, from a list or by pasting a link), or create a new one that's set up for you. If a spreadsheet has no `Results` tab, the page offers to add one; your other tabs aren't touched.
- **Excel file**: open an `.xlsx` file or create a new one. A file without a `Results` tab gets one added, the same way.

The choice is stored in your browser, so it's remembered on your next visit. Tap **Change** at the top of the page to switch. No spreadsheet ID is kept in this repository.

A `Results` tab created by the page has these columns:

| A | B | C | D | E | F | G | H | I | J | K | L |
|---|---|---|---|---|---|---|---|---|---|---|---|
| Saved at | Date | Candidate | Examiner | Grammatical Resource | Lexical Resource | Discourse Management | Pronunciation | Interactive Communication | Comments | Total | Percentage |

Total (out of 25) and Percentage are formulas. If you set up a `Results` tab by hand, the page writes columns A to J, and the "Saved results" list shows column L, or K if L is empty.

## Privacy

Candidate names and scores are stored only in your own Google Sheet or Excel file and, as an unsaved draft (and an Excel copy, where the browser can't save into files), in your browser. Nothing about candidates is kept in this repository.
