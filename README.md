# Achievement Scavenger Community Database

Welcome to the Community Database for Achievement Scavenger! This repository houses crowdsourced achievement guides, hints, missable warnings, collectible checklists, and curated guide links for **Steam**, **RetroAchievements**, **PlayStation**, and **Xbox Live** games.

## 📂 How it works

To keep the app lightning-fast, data is split into individual JSON files based on the game's unique platform ID. 

* **General Game Data (Hints, Chapters, Checklists)** is located inside the [`/games/`](./games/) folder.
* **Step-by-step Playthroughs (Guided Mode)** are located inside the [`/guides/`](./guides/) folder.

The file naming convention depends on the platform:
- **For Steam:** `[AppID].json` (e.g., Balatro's AppID is `2379780`, so its data lives in `/games/2379780.json`).
- **For RetroAchievements:** `RA_[GameID].json` (e.g., Chrono Trigger is `2`, so its data lives in `/games/RA_2.json`).
- **For Xbox Live:** `XBOX_[TitleID].json` (e.g., Halo Infinite is `1149954044`, so its data lives in `/games/XBOX_1149954044.json`).
- **For PlayStation:** `PSN_[npCommunicationId].json` (e.g., Astro's Playroom is `NPWR20731_00`, so its data lives in `/games/PSN_NPWR20731_00.json`).

---

## 🛠️ How to Contribute to the Database

### Method 1: The Easy Way (Using the App) 🌟
You don't need to write JSON by hand! Achievement Scavenger has built-in tools for contributing.
1. Open the game in the **Achievement Scavenger** app.
2. Click **Edit DB** to toggle edit mode.
3. Add your chapters, hints, video links, mark missable/spoiler achievements, and set up prerequisite chains. You can also build interactive Checklists from the Checklists tab!
4. Open the **My Shortcuts & Tools** accordion and click the **Create PR** button.
5. The app will automatically copy your perfectly formatted JSON to your clipboard and open the correct GitHub submission page. Just paste and submit!

### Method 2: Manual Submission
1. **Fork** this repository.
2. Find the game's ID (Steam AppID, RA GameID, Xbox TitleID, or PSN ID).
3. Create a new file in the `/games/` directory named according to the platform rules above.
4. Fill out the JSON using the template below.
5. Submit a **Pull Request**.

---

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
      "url": "https://youtube.com/watch?v=YOUR_VIDEO_ID"
    }
  ],
  "checklists": [
    {
      "id": "list_collectibles",
      "title": "All Memory Sticks",
      "items": [
        {
          "id": "item_mem_1",
          "name": "Memory Stick #12",
          "desc": "Found on a body leaning against the ruined car.",
          "category": "Xion City",
          "location": "Alleyway",
          "chapter": "Chapter 2: The Dark Forest",
          "imageUrl": "https://example.com/image.png",
          "videoUrl": "https://youtube.com/watch?v=YOUR_VIDEO_ID"
        }
      ]
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
      "video_url": "https://youtube.com/watch?v=YOUR_VIDEO_ID",
      "requires": ["PROLOGUE_ACHIEVEMENT_API_NAME"]
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

| Field | Type | Description |
| :--- | :--- | :--- |
| `chapters` | Array of Strings | **(Recommended)** An ordered list of chapter/category names. This populates the Chapter dropdown and defines the default achievement sort order in the app. |
| `links` | Array of Objects | A list of curated guides or resources. These appear in the **Community Guides** section of the app, separate from the user's personal shortcuts. |
| `checklists` | Array of Objects | Collections of trackable in-game items, collectibles, or side-tasks. |
| `achievements` | Array of Objects | The list of achievement entries (see below). |

### `checklists` entries

| Field | Type | Description |
| :--- | :--- | :--- |
| `id` | String | A unique string identifier for the checklist. |
| `title` | String | The display name for the checklist tab (e.g., `"Cans"` or `"Memory Sticks"`). |
| `items` | Array of Objects | The individual items inside the checklist. |

#### `checklists.items` fields

| Field | Type | Description |
| :--- | :--- | :--- |
| `id` | String | A unique string identifier for the item. |
| `name` | String | The name of the item. |
| `desc` | String | *(Optional)* A description of how or where to find it. |
| `category` | String | *(Optional)* Groups items together in accordion drop-downs. |
| `location` | String | *(Optional)* Specific location tag. |
| `chapter` | String | *(Optional)* Ties the item to a specific chapter for easy filtering. |
| `imageUrl` | String | *(Optional)* URL for an image or GIF showing the location. |
| `videoUrl` | String | *(Optional)* URL for a YouTube or raw video file. |

### `achievements` entries

| Field | Type | Description |
| :--- | :--- | :--- |
| `apiname` | String | **(REQUIRED)** The internal ID for the achievement.<br>• **Steam:** String (e.g., `"ACH_WIN_GAME"`).<br>• **RetroAchievements:** Numeric ID as a string (e.g., `"12345"`).<br>• **Xbox:** Title Achievement ID as a string.<br>• **PSN:** Trophy ID as a string. |
| `display_name` | String | Overrides the default achievement title. |
| `description` | String | Overrides the default achievement description. |
| `is_missable` | Boolean | `true` adds a red **MISSABLE** badge to the achievement card and alerts the user. |
| `is_spoiler` | Boolean | `true` blurs the hint text until the user hovers their mouse over it. |
| `chapter` | String | Adds a category tag. Must match a string from the top-level `chapters` array for proper sorting. |
| `hint` | String | The text that appears in the yellow hint box. Can contain URLs which the app will make clickable. |
| `video_url` | String | A YouTube URL. The app automatically embeds it as an interactive, playable video block. |
| `requires` | Array of Strings | A list of `apiname`s representing prerequisite achievements. Creates interactive "Requires" and "Unlocks" tracking chains inside the app. |

> **Note:** Private notes (`notes`) made in the app are kept strictly on your local machine and are deliberately excluded from Community DB exports.

---

## 🛡️ Guides

Guides allows users to create highly interactive, step-by-step walkthroughs that blend text, live achievement tracking, checklists, and media into a single timeline.

Because these guides can get quite long, they are stored separately from the main database in the [`/guides/`](./guides/) folder.

### Submitting a Guide
1. Open your game in the app and navigate to the **Guide** tab.
2. Click **+ New Guide** and fill in the Title, Author, and Description.
3. Build your guide using the **Edit Guide** mode. You can add Chapters, Text blocks, Link achievements to track progress live, insert Checklist items, and embed Media.
4. Click the **Publish** button (the GitHub icon). The app will automatically generate the JSON, copy it to your clipboard, and open your browser exactly where you need to create the file.
5. Paste the content, commit the new file, and submit your Pull Request!