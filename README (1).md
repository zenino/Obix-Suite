# Obix Suite

**You know what to do. So why don't you do it?**

Obix Suite is a set of short, interactive behavioral experiments that show you what's running your autopilot, give you a type you'll want to share, and turn the insight into a personal 4-week development plan.

It's one self-contained HTML file: no installs, no logins, no frameworks.

🔗 **Live app:** `https://YOUR-USERNAME.github.io/obix-suite/` *(replace once GitHub Pages is on)*

---

## What's inside

The suite has two modules.

### Module 1 · Curiosity Lab *(2 min each)*

| Experiment | What you do | What you get |
|---|---|---|
| **Guess vs. Reality** | Rate yourself on focus, calm and root-cause thinking, then face 5 real-life traps | Your type, a self-awareness score and a guess-vs-reality comparison |
| **Root-Cause Detective** | Pick a recurring problem and follow 3 layers of clues: trigger → hidden belief → system flaw | Your type, your root-cause chain and an IF-THEN fix rule |

### Module 2 · Obix Architect *(about 4 min)*

**Part 1 · How You Are:** 10 questions (4 style questions + 6 workplace scenarios) map how you take in information, react, decide and act.

**Part 2 · Your Plan:** choose your 90-day goal, your daily time (10 / 20 / 30+ min) and how you like to learn (on your own, with a coach, with your team).

**Output:** your type, your style at each stage, the stage holding you back, and a 4-week journey:

1. Awareness & Diagnostic Audit
2. Cognitive Reframing
3. The Non-Negotiable IF-THEN Operating Rule
4. Systems Integration & Verification Metric

---

## The framework: 4 stages behind every action

| Stage | What happens | Roots |
|---|---|---|
| 1 · Data Intake | How reality gets in | Five senses (Indriyas), Jungian Sensing vs. Intuition |
| 2 · Reactive Filter | The fast, emotional first response | Manas, Kahneman's System 1 |
| 3 · Discernment | Pausing to check assumptions and consequences | Buddhi, Stoic assent, System 2 |
| 4 · Behavioral Output | What you actually do | DISC style, earned authority |

The experiments show which stage is quietly running the show, and which one you can lean on.

---

## Result types

| Type | Tagline |
|---|---|
| The Night Scroller | Distraction wins the tug-of-war |
| The Hot Take | Fast replies, slow regrets |
| The Quiet Firefighter | Always fixing, never fixed |
| The Tomorrow Starter | Big plans, vanishing evenings |
| The Hero Fixer | Everyone needs you (that's the problem) |
| The Replay Loop | One comment, three hours |
| The Headline Reader | First signal wins |
| The Autopilot Decider | Fast answers, skipped questions |
| The Calm Operator | Rare: your autopilot is on your side |

Every type card includes **Save image** (a 1080×1350 card for stories and posts) and **Share** (the phone's share menu).

---

## Quick start

1. Download `obix-suite.html`.
2. Open it in any modern browser (Chrome, Edge, Safari, Firefox).

That's it. It works offline too; only saving results to Google Sheets needs internet.

---

## Connect Google Sheets (optional)

Results from all three experiences can be saved to one Google Sheet, each in its own tab.

1. Create a Google Sheet, then go to **Extensions → Apps Script**.
2. Replace everything with this code and save:

```javascript
function doPost(e) {
  var d = JSON.parse(e.postData.contents);
  var ss = SpreadsheetApp.getActiveSpreadsheet();
  var app = d.app || "ObixArchitect";
  var sheet = ss.getSheetByName(app) || ss.insertSheet(app);
  var header, row;
  if (app === "ObixGuessVsReality") {
    header = ["Timestamp","Name","Contact","Guess Focus","Guess Calm","Guess Root-Cause","Real Focus","Real Calm","Real Root-Cause"];
    row = [new Date(), d.name, d.contact, d.guesses.gFocus, d.guesses.gCalm, d.guesses.gRoot, d.reality.rFocus, d.reality.rCalm, d.reality.rRoot];
  } else if (app === "ObixRootCauseDetective") {
    header = ["Timestamp","Name","Contact","Case Solved","Clue 1","Clue 2","Clue 3"];
    row = [new Date(), d.name, d.contact, d.caseSolved].concat(d.clues || []);
  } else {
    header = ["Timestamp","Name","Email / WhatsApp","Role","Selected Goal","Bottleneck Stage","Total Score","Journey Assigned","Profile Summary","Plan Preferences"];
    row = [new Date(), d.name, d.email, d.role, d.selectedGoal, d.bottleneckStage, d.totalScore, d.journeyAssigned, d.profileSummary, d.planPreferences];
  }
  if (sheet.getLastRow() === 0) sheet.appendRow(header);
  sheet.appendRow(row);
  return ContentService.createTextOutput("ok");
}
```

3. Click **Deploy → New deployment → Web app**. Set *Execute as* to **Me** and *Who has access* to **Anyone**, then deploy and copy the Web App URL.
4. In `obix-suite.html`, paste that URL here:

```javascript
const WEBHOOK_URL = "YOUR_GOOGLE_SCRIPT_WEB_APP_URL_HERE";
```

Results then land in three tabs: **ObixArchitect**, **ObixGuessVsReality** and **ObixRootCauseDetective**.

---

## Host it on GitHub Pages

1. Upload `obix-suite.html` to this repository. Also upload a copy named `index.html` if you want the short link to work.
2. Go to **Settings → Pages**, set *Source* to **Deploy from a branch**, choose **main** and **/ (root)**, and click **Save**.
3. After a minute or two, your app is live at `https://YOUR-USERNAME.github.io/obix-suite/`.

---

## Configuration

| Setting | Where | What it does |
|---|---|---|
| `WEBHOOK_URL` | Top of the first `<script>` | Sends results to your Google Sheet. Leave as is to keep everything local. |
| `MIRROR_URL` | Last `<script>` | Optional link to the separate Obix Mirror app. Empty hides the link. |

---

## Data & privacy

- **Optional details:** name and contact details are optional in the Curiosity Lab, and every experience has a *Skip* option.
- **Where data goes:** answers are sent only to the Google Sheet you connect. Nothing goes anywhere else, and there's no tracking or cookies.
- **Your Sheet link is visible:** in a public repository, anyone can see your `WEBHOOK_URL`. For a prototype that's usually fine. Check your Sheet now and then and remove any junk rows.

---

## Built with

- **Code:** plain HTML, CSS and JavaScript in a single file, with no libraries or CDNs.
- **Graphics:** inline SVG for the diagrams and icons, and the Canvas API for share images.
- **Data:** a Google Apps Script webhook for result logging.

---

## About

Designed by **Jagadish**, Behavioral Architect & OD Product Designer.

Part of the **Obix Behavioral & Leadership Product Suite**, which also includes Obix Mirror (a baseline diagnostic, hosted separately).

> *The only wrong answer is the one you think you should give.*
