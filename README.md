# Trophy Scavenger Community Database

Welcome to the Community Database for Trophy Scavenger! This repository houses crowdsourced achievement guides, hints, and missable warnings for Steam games.

## 📂 How it works
To keep the app fast, data is split into individual JSON files based on the game's **Steam AppID**. 
All game data is located inside the [`/games/`](./games/) folder.

For example, Balatro's App ID is `2379780`, so its data lives in `/games/2379780.json`.

## 🛠️ How to Contribute a Game Guide
1. **Fork** this repository.
2. Find the game's **Steam AppID** (You can find this in the game's Steam Store URL).
3. Create a new file in the `/games/` directory named `[AppID].json`.
4. Open the Trophy Scavenger App while playing the game to find the exact internal **API Names** for the achievements (they appear in red text on the achievement cards).
5. Fill out the JSON using the template below.
6. Submit a **Pull Request**!

## 📋 JSON Template
Here is the structure you should use. **Only `apiname` is required.** You only need to add the fields you want to override or add hints to.

```json
[
  {
    "apiname": "ACH_1",
    "display_name": "Overridden Title (Optional)",
    "description": "Overridden Description (Optional)",
    "is_missable": true,
    "chapter": "Chapter 1",
    "hint": "Write your helpful community hint here.",
    "video_url": "https://www.youtube.com/watch?v=YOUR_LINK"
  },
  {
    "apiname": "ACH_2",
    "hint": "This is a massive story spoiler! Hover to reveal.",
    "is_spoiler": true
  }
]
```

### Explanation of Fields
| Field | Type | Description |
|---|---|---|
| `apiname` | String | **(REQUIRED)** The internal ID Steam uses for the achievement. |
| `display_name` | String | Overrides the default Steam achievement title. |
| `description` | String | Overrides the default Steam achievement description. |
| `is_missable` | Boolean | `true` adds a red MISSABLE badge to the achievement card. |
| `chapter` | String | Adds a grey category tag (e.g., "Grinding", "Multiplayer", "Chapter 4"). |
| `hint` | String | The text that appears in the yellow hint box. |
| `video_url` | String | A YouTube URL. The app automatically embeds it as a playable video. |
| `is_spoiler` | Boolean | `true` blurs the hint text until the user hovers their mouse over it. |