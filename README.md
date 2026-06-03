Here is a complete `README.md` template for your new GitHub repository. 

This is designed to be very welcoming to non-programmers (since most achievement hunters aren't necessarily software developers) while providing strict guidelines so they don't accidentally break your JSON file.

***

# 🏆 Trophy Scavenger - Community Database

Welcome to the official community-driven database for **Trophy Scavenger**! 

Trophy Scavenger is a desktop app that instantly detects what Steam game you are playing and overlays a live-updating achievement roadmap. While the app automatically fetches official titles, descriptions, and icons directly from Steam, it relies on this repository to provide "Smart" data: **Missable warnings, chapter groupings, hints, and video guides.**

Because this file is hosted on GitHub, anytime a roadmap is added or updated here, it **instantly updates for all Trophy Scavenger users worldwide.**

---

## 🤝 How to Contribute (Add or Edit a Game)

You don't need to be a programmer to add a game to the database! You can do it right here in your web browser.

1. **Log in** to your GitHub account.
2. Open the [`database.json`](./database.json) file in this repository.
3. Click the ✏️ **Pencil Icon** in the top right corner of the file to edit it.
4. Add your game using the format guide below.
5. Scroll to the bottom, click **Commit Changes...**, and submit a **Pull Request**. 

Once approved, your guide will be live for everyone!

*(⚠️ **CRITICAL:** Please ensure your formatting is correct. If you miss a comma or bracket, it will break the file. We highly recommend pasting your work into [JSONLint](https://jsonlint.com/) to verify it is "Valid JSON" before submitting!)*

---

## 📝 Formatting Guide (JSON Schema)

Every game is stored inside the database under its **Steam App ID** (e.g., `2379780` for Balatro). Inside that ID is an array of achievement objects. 

You do **not** need to map every achievement! If an achievement doesn't need a hint or a missable tag, you can leave it out. Trophy Scavenger will still show it using default Steam data.

### Example Entry:

```json
{
  "2379780": [
    {
      "apiname": "1",
      "display_name": "Ante Up!",
      "description": "Reach Ante 4",
      "is_missable": false,
      "chapter": "Early Game",
      "hint": "Just play naturally. Focus on a single strong hand type like Flushes or Two Pair early on.",
      "video_url": "https://www.youtube.com/watch?v=dQw4w9WgXcQ"
    },
    {
      "apiname": "2",
      "is_missable": true,
      "chapter": "Mid Game",
      "hint": "You only have one chance to do this during the boss blind!"
    }
  ]
}
```

### Data Fields Explained:

*   `"apiname"` **(REQUIRED)**: This is Steam's hidden internal name for the achievement. **(See below on how to find this).**
*   `"display_name"` *(Optional)*: A fallback title just in case Steam API is down.
*   `"description"` *(Optional)*: A fallback description.
*   `"is_missable"` *(Optional)*: `true` or `false`. If true, attaches a red MISSABLE tag to the app.
*   `"chapter"` *(Optional)*: A short string (e.g., "Act 1", "Story", "Collectibles") that shows up next to the title.
*   `"hint"` *(Optional)*: Your personal tip on how to unlock the achievement.
*   `"video_url"` *(Optional)*: A standard YouTube URL. The app will automatically convert this into an embedded video player.

---

## 🔍 How to find the `apiname`

The biggest mistake people make is using the public name (e.g., "Defeat the Dragon") instead of Steam's internal API name (e.g., `ACH_KILL_DRAGON_01`). **Trophy Scavenger relies entirely on the `apiname` to track live progress.**

Here is how to find the exact `apiname` for any game:

1. Go to [SteamDB.info](https://steamdb.info/) and search for your game.
2. Click on the game to open its page.
3. On the left-hand sidebar, click on **User Stats**.
4. Look at the table. The column labeled **Name** is the exact string you must use for `"apiname"` in the JSON.

---

## 📜 Community Rules & Guidelines

1. **No Unmarked Spoilers:** If a hint contains massive story spoilers, please write `[SPOILER]` at the beginning of the `"hint"` text so users are warned.
2. **Keep Hints Concise:** Don't paste a 5-paragraph essay. Keep hints punchy, helpful, and to the point. For longer explanations, link a `"video_url"`.
3. **Valid YouTube Links:** Please use standard `youtube.com/watch?v=...` or `youtu.be/...` links to ensure the app can embed them properly.
4. **App ID Verification:** Ensure the Steam App ID is wrapped in quotes (e.g., `"1091500": [...]`) because JSON keys must be strings.

Happy Hunting! 🏆
