# Vocarb
> Minimalist Arabic–Chinese vocabulary flashcards.

**Live: [vocarb.vercel.app](https://vocarb.vercel.app/)**

A single-page flashcard app for studying Arabic vocabulary with Chinese translations. Vocabulary lives in Supabase (PostgreSQL), the site is hostedon Vercel, and new words are added inside the app — so the code isdeployed once and never touched again.

---

## Features
- **Bulk import** — paste a weekly word list (Chinese + Arabic per line); theparser splits each line, extracts ج. plural forms, and auto-generates pinyin
- **Sets** — organize words into sets (Week 12, Week 13, …) or review everything
- **Both directions** — CN → AR or AR → CN; pinyin shown above Chinese, fullharakat on the Arabic
- **Keyboard-first** — Space to flip, arrow keys to navigate
- **Shuffle** for randomized review
- **Word bank** — browse and delete entries
- **Private** — email/password auth via Supabase, with row-level security onall data
- **Responsive** — works on desktop and mobile

---

## Tech stack
| Layer | Tool |
| :--- | :--- |
| **Frontend** | Single-file static HTML/CSS/JS (`index.html`) |
| **Database** | Supabase (PostgreSQL + row-level security) |
| **Auth** | Supabase email/password |
| **Hosting** | Vercel |
| **Pinyin** | `pinyin-pro` |
| **Fonts** | Amiri (Arabic) · Noto Serif SC (Chinese) |

---

## Database Schema
| Column | Type | Notes |
| :--- | :--- | :--- |
| **id** | uuid | Primary key |
| **set_name** | text | Set label, e.g. Week 12 |
| **zh** | text | Chinese |
| **pinyin** | text | Auto-generated on import |
| **ar** | text | Arabic (with harakat) |
| **plural** | text | Extracted from ج. notation |
| **created_at** | timestamptz | Insertion time |


---

## Usage
1. **＋ Add Words** → paste the list, one entry per line:
```
提供、具备 تَوَفَّرَ يَتَوَفَّرُ تَوَفُّرًا
食物、食品 غِذَاءٌ، ج. أَغْذِيَةٌ
```
2. Name the set → Save. Pinyin and plurals are handled automatically.
3. Study.
### Keyboard shortcuts
| Key | Action |
| :--- | :--- |
| **Space** | Flip card |
| **← / →** | Prev / next |

---

## Versioning
This project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html)

All notable changes are documented in [CHANGELOG.md](https://github.com/zihanlei/vocab-app/blob/main/CHANGELOG.md)

## License
[MIT](https://github.com/zihanlei/vocab-app/blob/main/LICENSE)
