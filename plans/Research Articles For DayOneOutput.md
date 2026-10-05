https://www.pythonanywhere.com/user/shas3/files/home/shas3 https://script.google.com/home/projects/1fjI1UIgHop5TZoAuUhgmGIQEVMikXfvgPYUwZTDyOAsmIs_y1KERt5o7/edit i want to use my python anywhere and google apps scripts to research the highest ranking articles in the productivity, health, ai and crypto niches and compile the urls for me to use to create better articles than the top ranked ones using you/claude/chat/deepseek and upload to my doy one output newsletter which i have not published for over 2 months now. can you help me

Yes — this is very doable, and your instinct to use these two tools is right. But let me fix the architecture before you build it, because there's one trap:

**The trap:** PythonAnywhere's free tier blocks most outbound internet (a whitelist system). Scraping Google directly will get your account flagged. So we flip the jobs:

- **Google Apps Script** = the research engine (fetches Google News RSS for your niches, daily, no API key needed, runs in Google's infrastructure — no blocks)
- **PythonAnywhere** = the prompt compiler (reads the results from your Google Sheet, generates ready-to-paste prompt packs for Claude/ChatGPT/DeepSeek)
- **Google Sheet** = your single source of truth (this also feeds straight into your lang-aios planning philosophy)

Here's the full build.

## Part 1 — Google Apps Script (the research engine)

Create a new Google Sheet (name it `DayOne_Research`), then **Extensions → Apps Script**, delete everything, paste this:

```javascript
const CONFIG = {
  PER_NICHE: 5,
  NICHES: {
    "Productivity": ["deep work", "time management systems", "morning routines", "focus science"],
    "Health":       ["sleep optimization", "longevity research", "exercise science", "gut health"],
    "AI":           ["AI agents business", "generative AI tools", "machine learning news", "AI automation"],
    "Crypto":       ["bitcoin news", "ethereum", "crypto regulation", "defi"]
  }
};

function runResearch() {
  const ss = SpreadsheetApp.getActiveSpreadsheet();
  const allRows = [];

  for (const [niche, queries] of Object.entries(CONFIG.NICHES)) {
    const seen = new Set();
    let rows = [];

    for (const q of queries) {
      const rssUrl = "https://news.google.com/rss/search?q="
        + encodeURIComponent(q)
        + "&hl=en-US&gl=US&ceid=US:en";

      try {
        const xml = UrlFetchApp.fetch(rssUrl, { muteHttpExceptions: true }).getContentText();
        const root = XmlService.parse(xml).getRootElement();
        const channel = root.getChild("channel");
        const items = channel.getChildren("item");

        items.forEach(item => {
          const title = item.getChildText("title") || "";
          const link  = item.getChildText("link") || "";
          const pub   = item.getChildText("pubDate") || "";
          const key = title.toLowerCase().replace(/[^a-z0-9]/g, "").slice(0, 60);
          if (!seen.has(key)) {
            seen.add(key);
            rows.push([new Date(), niche, title, link, pub, q]);
          }
        });
      } catch (e) {
        Logger.log("Failed: " + q + " — " + e);
      }
    }

    // Sort newest first, keep top N
    rows.sort((a, b) => new Date(b[4]) - new Date(a[4]));
    rows = rows.slice(0, CONFIG.PER_NICHE);

    // Write to a tab named after the niche
    let tab = ss.getSheetByName(niche);
    if (!tab) tab = ss.insertSheet(niche);
    tab.clearContents();
    tab.getRange(1, 1, 1, 6).setValues([["Pulled At", "Niche", "Title", "URL", "Published", "Query"]]);
    if (rows.length) tab.getRange(2, 1, rows.length, 6).setValues(rows);

    allRows.push(...rows);
  }

  // Master tab
  let master = ss.getSheetByName("MASTER");
  if (!master) master = ss.insertSheet("MASTER");
  master.clearContents();
  master.getRange(1, 1, 1, 6).setValues([["Pulled At", "Niche", "Title", "URL", "Published", "Query"]]);
  if (allRows.length) master.getRange(2, 1, allRows.length, 6).setValues(allRows);
}

function setDailyTrigger() {
  ScriptApp.getProjectTriggers().forEach(t => ScriptApp.deleteTrigger(t));
  ScriptApp.newTrigger("runResearch").timeBased().everyDays(1).atHour(8).create();
}
```

**Setup steps:**
1. Save, then run `runResearch` once manually (it'll ask for permissions — approve).
2. Run `setDailyTrigger` once. Now it refreshes every day at 8 AM automatically.
3. Your sheet now has 5 tabs: MASTER + one per niche, each with the top 5 freshest articles.

## Part 2 — PythonAnywhere (the prompt compiler)

This turns your sheet into a swipe file of ready-to-paste AI prompts. On PythonAnywhere, create `compile_prompts.py`:

```python
import csv, io, urllib.request, datetime, os

# Publish your sheet first: File → Share → Publish to web → MASTER tab → CSV
SHEET_CSV_URL = "PASTE_YOUR_PUBLISHED_CSV_URL_HERE"
OUT_DIR = "/home/shas3/prompt_packs"

PROMPT_TEMPLATE = """You are a world-class newsletter writer for "Day One Output".
Below is a top-performing article in the {niche} niche. Your job: write an ORIGINAL
piece on the same topic that is objectively better.

Reference article: {title}
URL: {url}

Rules:
- Do NOT copy structure, sentences, or phrasing. Research the topic, write fresh.
- Open with a personal, specific hook (not "In today's fast-paced world...")
- Add one contrarian angle or myth-busting point the original missed
- Include a named, memorable framework (3-5 steps, acronym if possible)
- End with one concrete 5-minute action the reader can take today
- Tone: direct, lived-experience, zero fluff. 700-900 words.
- Suggest 3 subject lines for the newsletter edition.
"""

def main():
    os.makedirs(OUT_DIR, exist_ok=True)
    try:
        data = urllib.request.urlopen(SHEET_CSV_URL, timeout=30).read().decode("utf-8")
    except Exception as e:
        print(f"Could not fetch sheet ({e}). If you're on the free tier, docs.google.com may be blocked — download the CSV manually from the sheet and save as research.csv, then uncomment the next line.")
        # data = open("research.csv", encoding="utf-8").read()
        return

    rows = list(csv.DictReader(io.StringIO(data)))
    today = datetime.date.today().isoformat()
    path = os.path.join(OUT_DIR, f"prompt_pack_{today}.md")

    by_niche = {}
    for r in rows:
        by_niche.setdefault(r["Niche"], []).append(r)

    with open(path, "w", encoding="utf-8") as f:
        f.write(f"# Day One Output — Prompt Pack ({today})\n\n")
        for niche, items in by_niche.items():
            f.write(f"\n## {niche}\n\n")
            for i, r in enumerate(items, 1):
                f.write(f"### {i}. {r['Title']}\n")
                f.write(f"- URL: {r['URL']}\n\n")
                f.write("**Prompt to paste into Claude/ChatGPT/DeepSeek:**\n\n")
                f.write("```\n" + PROMPT_TEMPLATE.format(
                    niche=niche, title=r["Title"], url=r["URL"]) + "```\n\n")

    print(f"Done → {path}")

if __name__ == "__main__":
    main()
```

**Setup:**
1. In your Google Sheet: **File → Share → Publish to web → select "MASTER" → CSV**, copy that URL into `SHEET_CSV_URL`.
2. Run once: `python3 compile_prompts.py` (if the free tier blocks docs.google.com, just download the CSV from the sheet manually and use the fallback line in the code).
3. Optional: set it as a daily scheduled task on PythonAnywhere (Tasks tab).

## Part 3 — Your workflow from here

1. Open the prompt pack file → copy one prompt per AI (same prompt to Claude, ChatGPT, AND DeepSeek gives you 3 different drafts to blend — that's your "better than the top article" edge, free).
2. Edit into your voice. **Ground rule:** these URLs are research — never republish or closely paraphrase someone else's article. Beat them with angle and experience, not theft.
3. **Health niche caution:** avoid medical claims (cures, dosages). "What the research says about sleep + what I tried" is safe; "this supplement fixes X" can get you in newsletter-platform trouble.
4. Two months of silence means your first comeback issue should acknowledge it in one line ("been building — here's what I found") and move on. Don't apologize at length.

**Your single next action:** create the Google Sheet, paste the Apps Script, run `runResearch`, and tell me what shows up (or any error). That's it for today — everything else waits until that's working.
