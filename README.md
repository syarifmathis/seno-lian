# 🌟 Seno & Lian Lernen

A gamified trilingual learning app for Seno and Lian — learning **English** and **Bahasa Indonesia** from their native **German**.

---

## 🚀 Quick Setup (5 minutes)

### 1 · Push files to GitHub

Your repo already has these files after cloning:
```
index.html        ← the complete app
data/data.json    ← 25 starter sentences + profiles
README.md
```

### 2 · Enable GitHub Pages

1. Go to **github.com/syarifmathis/seno-lian** → Settings → Pages  
2. Source: **Deploy from a branch** → Branch: `main` → Folder: `/ (root)`  
3. Save → your app will be live at **https://syarifmathis.github.io/seno-lian/**

### 3 · Create a GitHub Personal Access Token

The app saves progress back to `data/data.json` via the GitHub API.

1. Go to **github.com/settings/tokens/new**  
   - **Note**: "Seno Lian Learn"  
   - **Expiration**: No expiration (or 1 year)  
   - **Scope**: ✅ `repo`  
2. Copy the generated token (starts with `ghp_`)

### 4 · Get an ElevenLabs API Key

The app uses ElevenLabs for natural multilingual speech (German, English, Indonesian).

1. Sign up at **elevenlabs.io** (free tier available)  
2. Go to **Profile → API Key** → copy it

### 5 · Enter keys in the app

1. Open the app → **⚙️ Setup** tab  
2. Paste your **ElevenLabs API Key**  
3. Paste your **GitHub Token**  
4. Tap **💾 Einstellungen speichern**  
5. Tap **🔗 Verbindung testen** to verify GitHub works

---

## 🎮 How the App Works

### Profiles
- Tap **🦁 Seno** or **🌸 Lian** — each child has their own stars, streak & progress
- Profiles are stored independently in `data.json`

### Daily Sentence
- Every day a new sentence rotates automatically
- Tap **📖 Lernen** to open it
- Tap **🔊 Anhören** to hear it in German

### Sentence View
- Switch between 🇩🇪 German · 🇬🇧 English · 🇮🇩 Indonesian tabs
- Tap underlined words in the sentence to see their translation popup
- Or tap word chips below for word translations
- Hear any language with the speak buttons
- Tap **⭐ Ich kann das!** when the sentence is learned → earn **3 ⭐** stars

### Word Practice (Flashcard Mode)
- From any sentence's word popup, tap **🎯 Dieses Wort üben** to add a word
- Go to **🎯 Üben** tab
- See the German word → tap **👀 Aufdecken** → reveal English + Indonesian + audio
- Tap **✓ Kann ich!** → earn **1 ⭐** → word needs 3 correct answers to be "learned"
- Tap **↻ Nochmal** → word goes back to the queue

### Gamification
| Stars | Level |
|-------|-------|
| 0–4   | 🥚 Anfänger |
| 5–19  | 🌱 Sprössling |
| 20–49 | 🌟 Stern |
| 50–99 | 🚀 Rakete |
| 100–199 | 🏆 Champion |
| 200+  | 👑 König |

- 🔥 **Streak**: increases every day the app is opened
- ⭐ **Stars**: earned by learning sentences (+3) and words (+1)
- 🎉 **Confetti** celebration on achievements

---

## 📥 Importing Sentences

### Via the App
1. **⚙️ Setup** → **📥 Sätze importieren**
2. Select or drag a `.json` file

### File Format
```json
[
  {
    "de":  "Der Hund springt hoch.",
    "en":  "The dog jumps high.",
    "idn": "Anjing itu melompat tinggi.",
    "words": [
      { "de": "Hund",    "en": "dog",    "idn": "anjing"   },
      { "de": "springt", "en": "jumps",  "idn": "melompat" },
      { "de": "hoch",    "en": "high",   "idn": "tinggi"   }
    ]
  }
]
```

**Notes:**
- Indonesian can be `idn`, `id`, or `id_lang` — all work
- `words` array is optional but enables word-tap translations
- `category` and `difficulty` are optional metadata
- Duplicate sentences (same German text) are automatically skipped

### Bulk Import via `data/data.json`
You can also directly edit `data/data.json` and push to GitHub — the app will pick up the changes on next load.

---

## 🔊 ElevenLabs Voices

The app uses the `eleven_multilingual_v2` model which speaks German, English, and Indonesian naturally from a single voice.

**Recommended voices for kids:**
| Voice | ID | Character |
|-------|----|-----------|
| Rachel (default) | `21m00Tcm4TlvDq8ikWAM` | Warm, clear |
| Elli | `MF3mGyEYCl7XYWbV9V6O` | Friendly, young |
| Domi | `AZnzlk1XvdvUeBnXmlld` | Energetic |

Find more at [elevenlabs.io/voice-library](https://elevenlabs.io/voice-library) — filter by "multilingual v2" support.

---

## 📱 Mobile Tips

- Add to Home Screen (iOS: Share → Add to Home Screen) for an app-like experience
- The app works offline using cached data from the last sync
- Safe area insets are handled for iPhone notch/home bar

---

## 🏗 Architecture

```
index.html          Single-file SPA (HTML + CSS + JS)
data/data.json      Sentences + per-profile progress (synced via GitHub API)
```

**Data flow:**
1. App loads → fetches `data/data.json` from GitHub (public read, no auth)
2. Progress updates (known sentences, stars, streaks) → writes back to GitHub (requires PAT)
3. localStorage is used as a fast cache / offline fallback

**Security note:** Your GitHub Personal Access Token is stored only in your browser's `localStorage` and is never committed to the repository.

---

## 🛠 Troubleshooting

| Problem | Solution |
|---------|----------|
| No audio | Check ElevenLabs key in ⚙️ Setup → test with "🔊 Stimme testen" |
| Progress not saving | Check GitHub token in ⚙️ Setup → token needs `repo` scope |
| App shows old data | Pull latest `data.json` from GitHub; clear browser cache |
| 404 on GitHub Pages | Wait ~2 min after enabling Pages; check branch is `main` |
