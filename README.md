# Achievement Scavenger Community Database
Welcome to the Community Database for Achievement Scavenger! This repository houses crowdsourced achievement guides, hints, missable warnings, and curated guide links for **Steam** and **RetroAchievements** games.

## 📂 How it works
To keep the app fast, data is split into individual JSON files based on the game's unique ID. All game data is located inside the [`/games/`](./games/) folder.

The file naming convention depends on the platform:
-   **For Steam:** Files are named `[AppID].json`. For example, Balatro's AppID is `2379780`, so its data lives in `/games/2379780.json`.
-   **For RetroAchievements:** Files are named `RA_[GameID].json`. For example, Chrono Trigger's Game ID on RetroAchievements is `2`, so its data lives in `/games/RA_2.json`.

Each file uses an object format with three top-level keys: `chapters`, `links`, and `achievements`.

## 🛠️ How to Contribute a Game Guide
1.  **Fork** this repository.
2.  Find the game's ID:
    *   **Steam:** Find the **AppID** from the game's Steam Store URL (e.g., `store.steampowered.com/app/2379780/Balatro/`).
    *   **RetroAchievements:** Find the **GameID** from the game's page URL (e.g., `retroachievements.org/game/2`).
3.  Create a new file in the `/games/` directory named `[AppID].json` for Steam or `RA_[GameID].json` for RetroAchievements.
4.  Open the Achievement Scavenger App while playing the game to find the exact internal **API Names** for the achievements.
5.  Fill out the JSON using the template below.
6.  Submit a **Pull Request**!

## 📋 JSON Template

```json
{
  "chapters": [
    "Prologue",
    "Chapter 1: The Awakening",
    "Chapter 2: The Dark Forest",
    "Side Quests",
    "Multiplayer",
    "End-Game Grinding"
  ],
  "links": [
    {
      "title": "100% Achievement Guide (Steam)",
      "url": "https://steamcommunity.com/sharedfiles/filedetails/?id=YOUR_GUIDE_ID"
    },
    {
      "title": "Video Walkthrough (YouTube)",
      "url": "https://www.youtube.com/watch?v=VIDEO_ID"
    }
  ],
  "achievements": [
    {
      "apiname": "STEAM_API_NAME_1",
      "display_name": "Overridden Title (Optional)",
      "description": "Overridden Description (Optional)",
      "is_missable": true,
      "chapter": "Chapter 1: The Awakening",
      "hint": "Write your helpful community hint here.",
      "video_url": "https://www.youtube.com/watch?v=VIDEO_ID"
    },
    {
      "apiname": "12345",
      "hint": "This is a massive story spoiler! Hover to reveal.",
      "is_spoiler": true
    }
  ]
}
```

## 📋 Field Reference

### Top-level fields

| Field        | Type            | Description                                                                                                                                                    |
| :----------- | :-------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `chapters`   | Array of Strings | **(Recommended)** An ordered list of chapter/category names. This populates the Chapter dropdown and defines the default achievement sort order in the app. |
| `links`      | Array of Objects | A list of curated guides or resources. These appear in the **Community Guides** section of the app, separate from the user's personal shortcuts.                   |
| `achievements` | Array of Objects | The list of achievement entries (see below).                                                                                                                   |

### `links` entries

| Field   | Type   | Description                                                        |
| :------ | :----- | :----------------------------------------------------------------- |
| `title` | String | **(REQUIRED)** The display name for the link (e.g. `"Full Guide"`). |
| `url`   | String | **(REQUIRED)** The full URL.                                       |

### `achievements` entries

| Field          | Type    | Description                                                                                                                                                                                           |
| :------------- | :------ | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `apiname`      | String  | **(REQUIRED)** The internal ID for the achievement. **For Steam**, this is a string (e.g., `"ACH_UNLOCK_RED_SEAL"`). **For RetroAchievements**, this is the numeric Achievement ID as a string (e.g., `"12345"`). |
| `display_name` | String  | Overrides the default achievement title.                                                                                                                                                              |
| `description`  | String  | Overrides the default achievement description.                                                                                                                                                        |
| `is_missable`  | Boolean | `true` adds a red **MISSABLE** badge to the achievement card.                                                                                                                                           |
| `chapter`      | String  | Adds a grey category tag. Must match a string from the top-level `chapters` array for proper sorting.                                                                                                 |
| `hint`         | String  | The text that appears in the yellow hint box.                                                                                                                                                         |
| `video_url`    | String  | A YouTube URL. The app automatically embeds it as a playable video.                                                                                                                                   |
| `is_spoiler`   | Boolean | `true` blurs the hint text until the user hovers their mouse over it.                                                                                                                                  |

## 🔄 Export & Import

When you use **Export JSON** inside Achievement Scavenger, the exported file uses this same format — including your defined chapter order, any personal shortcuts, and all your local edits to achievements. This means you can directly submit your export as a pull request to share your work with the community.
