# Dialed

A simple, minimal coffee log for dialing in espresso and pour over. Save your beans once, log each shot in a few taps, see charts, and get a suggestion for what to change on the next shot.

It is a single static page with no build step and no dependencies, so it runs anywhere you can host a file, including GitHub Pages. Your data stays in your browser, and you can optionally sync it to a private GitHub repo.

**[How-to guide (PDF)](Dialed-how-to-guide.pdf)**

## Features

**Beans**
- Bean profiles with name, roast, purchase date, roast date and flavour tags
- Bag weight and price, with remaining weight, low-bag warnings and cost per shot
- Finish a bag to stop its age counting and lock it from new shots
- Filter by new or finished beans, newest first

**Espresso log**
- Dose, yield, time and grinder clicks, with + / - steppers (hold to repeat) and quick picks
- Ratio shortcuts that fill in the yield for your dose
- Black or White, taste (Sour, Balanced, Bitter, Diluted), 1 to 5 rating and notes
- Live ratio, flow rate, days since roast and cost while you type
- Edit or delete any shot, with the time it was logged saved automatically

**Dial in faster**
- Next-shot suggestion based on taste, time and ratio, with a one-tap Use these settings
- Best shot per bean, and an average of your good shots, scoped to that bean only
- Latest shot gauges against the 25 to 30 second and 1:1.8 to 1:2.5 targets, plus a comparison with the previous shot

**Overview**
- Last 7 days summary
- Charts for time, ratio, yield and clicks, plus a clicks-versus-time sweet spot chart
- Filters by bean, taste and rating, and a paged shot list

**Pour over**
- Recipe cards for Tetsu Kasuya 4:6, James Hoffmann V60 and a Scott Rao-style V60, each with specs, a step table and technique notes

**App feel**
- Phone-first layout with a fixed bottom tab bar, no zoom and no sideways scrolling
- Dark (default) and light themes
- First-visit walkthrough, with a link to the how-to guide

## Quick start

1. Create a new **public** repository, for example `dialed`.
2. Upload these files to the root of it:
   - `index.html`
   - `Dialed-how-to-guide.pdf`
   - `README.md`
3. Go to **Settings, Pages**. Under Branch choose `main` and `/ (root)`, then save.
4. After a minute or two, open `https://YOUR-USERNAME.github.io/dialed/`.

Keep the PDF's file name exactly as it is. The app links to it by that name.

## Sync across devices (optional)

Without sync, each device keeps its own log in that browser. To share one log between your phone and laptop, sync to a private repo.

1. Create a second repository, for example `dialed-data`, set to **Private**, with a README so it is not empty. Do not use the public site repo, because anything in it is readable by anyone.
2. Create a token: GitHub, Settings, Developer settings, Fine-grained tokens, Generate new token.
   - Repository access: **Only select repositories**, then choose `dialed-data`
   - Repository permissions: **Contents**, set to **Read and write**
   - Pick an expiry date and note it
3. In the app, tap the gear icon. Under **Sync with GitHub** enter `YOUR-USERNAME/dialed-data` as the repo, leave the file path blank, paste the token, and tap **Save and sync**.
4. The footer should say **Synced to GitHub**, and `espresso-log.json` appears in the data repo.
5. Repeat step 3 on each device with the same repo and token.

How sync behaves:
- Changes are pushed about a second after you make them, and pulled when you open the page or return to the tab.
- Two devices are merged, so shots are not lost, and deletes carry across.
- It works offline and catches up when you are next online.
- The data repo's commit history keeps older versions of your log.

## Your data

- Stored in your browser's local storage on each device. Clearing site data on a device deletes its local copy.
- With sync on, the GitHub copy is the safety net. Without it, use **Export JSON** on the gear page now and then.
- The gear page also has **Export CSV** for spreadsheets and **Import JSON** to restore or merge a backup.
- The GitHub token is stored in that browser only and is never written into the data file or the site repo.
- Preferences (theme, currency, grinder direction) are saved per device and are not synced.

## Using it

See the [how-to guide](Dialed-how-to-guide.pdf) for a full walkthrough. In short:

1. **Beans** tab: add a bean.
2. **Log** tab: pick the bean, enter dose, yield, time, clicks and taste, then tap **Log shot**.
3. **Overview** tab: read the gauges and the next-shot suggestion, then tap **Use these settings** and pull the next shot.

Set **More clicks = coarser** or **finer** on the gear page so click suggestions move the right way for your grinder.

## Files

| File | Purpose |
| --- | --- |
| `index.html` | The whole app: markup, styles and script |
| `Dialed-how-to-guide.pdf` | The how-to guide, linked from the first-visit walkthrough and the settings page |
| `README.md` | This file |

## Technical notes

- Plain HTML, CSS and JavaScript in one file. No framework, bundler or package install.
- Local data key: `espresso-log-v2` in local storage. Older `espresso-log-v1` data is converted automatically.
- The sync file is JSON with `beans`, `shots` and `deleted` lists. It is written to the GitHub Contents API with a fine-grained token.
- Target ranges (25 to 30 seconds, 1:1.8 to 1:2.5) are constants in the script. Search `band` and `rOk` in `index.html` to change them.
- Link previews use the page title and description only. To add a preview image, add an `og:image` meta tag with the full URL of an image in your repo.

## Troubleshooting

| Problem | Fix |
| --- | --- |
| Footer says GitHub rejected the token | The token expired or lacks Contents read and write on the data repo. Create a new one and paste it in |
| Footer says repo not found | Check the `owner/name` spelling and that the token was given access to that repo |
| Nothing syncs after the first save | Open the gear page and tap Save and sync again, then check the footer |
| The PDF link shows a 404 | Make sure `Dialed-how-to-guide.pdf` is in the same folder as `index.html` |
| Changes to the page do not appear | Hard refresh, or close and reopen the tab. GitHub Pages can take a minute or two to update |
| Lost data after clearing the browser | Enter your repo and token again to pull it back, or import a JSON backup |

## Credits

Pour over recipes are summaries of the methods popularised by Tetsu Kasuya, James Hoffmann and Scott Rao. Check their original sources for the full detail.
