# Achievement Scavenger Community Database
Welcome to the Community Database for Achievement Scavenger! This repository houses crowdsourced achievement guides, hints, missable warnings, and curated guide links for Steam games.

## 📂 How it works
To keep the app fast, data is split into individual JSON files based on the game's **Steam AppID**.
All game data is located inside the [`/games/`](./games/) folder.

For example, Balatro's App ID is `2379780`, so its data lives in `/games/2379780.json`.

Each file uses an object format with two top-level keys: `links` and `achievements`.

## 🛠️ How to Contribute a Game Guide
1. **Fork** this repository.
2. Find the game's **Steam AppID** (visible in the game's Steam Store URL).
3. Create a new file in the `/games/` directory named `[AppID].json`.
4. Open the Achievement Scavenger App while playing the game to find the exact internal **API Names** for the achievements.
5. Fill out the JSON using the template below.
6. Submit a **Pull Request**!

## 📋 JSON Template

```json
{
  "links": [
    {
      "title": "100% Achievement Guide (Steam)",
      "url": "https://steamcommunity.com/sharedfiles/filedetails/?id=YOUR_GUIDE_ID"
    },
    {
      "title": "Video Walkthrough (YouTube)",
      "url": "https://www.youtube.com/watch?v=YOUR_VIDEO_ID"
    }
  ],
  "achievements": [
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
}
```

## 📋 Field Reference

### Top-level fields

| Field | Type | Description |
|---|---|---|
| `links` | Array | A list of curated guides or resources for the game. These appear in the **Community Guides** section of the app, separate from the user's personal shortcuts. |
| `achievements` | Array | The list of achievement entries (see below). |

### `links` entries

| Field | Type | Description |
|---|---|---|
| `title` | String | **(REQUIRED)** The display name for the link (e.g. `"Full Achievement Guide"`). |
| `url` | String | **(REQUIRED)** The full URL. |

### `achievements` entries

| Field | Type | Description |
|---|---|---|
| `apiname` | String | **(REQUIRED)** The internal ID Steam uses for the achievement. |
| `display_name` | String | Overrides the default Steam achievement title. |
| `description` | String | Overrides the default Steam achievement description. |
| `is_missable` | Boolean | `true` adds a red MISSABLE badge to the achievement card. |
| `chapter` | String | Adds a grey category tag (e.g., `"Grinding"`, `"Multiplayer"`, `"Chapter 4"`). |
| `hint` | String | The text that appears in the yellow hint box. |
| `video_url` | String | A YouTube URL. The app automatically embeds it as a playable video. |
| `is_spoiler` | Boolean | `true` blurs the hint text until the user hovers their mouse over it. |

## 🔄 Export & Import

When you use **Export JSON** inside Achievement Scavenger, the exported file uses this same format — including any personal shortcuts you've added and all your local edits to achievements. This means you can directly submit your export as a pull request to share your work with the community.
