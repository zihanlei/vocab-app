# Change Log

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/)
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).


## [1.0.0] - 2026-10-04

### Added
**Flashcards and Study:**
- Minimalist single-page flashcard app for Arabic–Chinese vocabulary, rendered as one static HTML file with no build step.
- 3D flip animation (CSS transforms) with a warm paper palette; Amiri for Arabic (full harakat), Noto Serif SC for Chinese, pinyin shown above the Chinese.
- Bilingual study directions — CN → AR and AR → CN — with the preference persisted per device via localStorage.
- Keyboard-first controls: Space flips the card, ← / → navigate with wraparound; on-screen navigation buttons for touch/mobile.
- Shuffle (Fisher–Yates) for randomized review order.
- Progress indicator: card counter plus a thin progress bar.
- Small hint on the answer side showing the prompt word for self-checking.
- Responsive layout down to mobile; prefers-reduced-motion disables animations.

**Vocabulary Management:**
- Bulk import dialog: paste one word per line and the parser splits Chinese from Arabic automatically (mixed-script lines, tab, and | separators supported; sides auto-swapped if pasted in reverse; # lines ignored).
- Automatic pinyin generation at import time via pinyin-pro, with a fallback that preserves manually typed pinyin.
- Arabic plural extraction: "، ج. X" notation is split into a dedicated plural column and displayed beneath the singular.
Pre-save preview showing every recognized word (with pinyin and plural) plus a count of skipped lines.
- Sets: arbitrary set names (e.g. "Week 12") with an autocomplete list of existing sets, an "All words" combined view, and the last-selected set persisted between visits.
- Word Bank dialog listing all words in the current set with per-word delete (with confirmation).

**Accounts and Data:**
- Persistence in Supabase (PostgreSQL): a single words table (set_name, zh, pinyin, ar, plural, created_at).
- Email/password authentication with sessions persisting across reloads; login errors mapped to plain-English messages.
- Row-level security enabled — all reads and writes restricted to authenticated users only; public sign-ups disabled (accounts created manually in the Supabase dashboard).
- Toast notifications for save / delete / load outcomes, including raw database errors when they occur.

**Deployment and Infrastructure:**
- Hosted on Vercel with automatic deploys on every push to the production branch.
- vercel.json rewrite serving the app at the root URL (vocarb.vercel.app).
- CDN dependencies only: supabase-js, pinyin-pro, Google Fonts (Amiri, Noto Serif SC).
- README with full setup guide (Supabase + Vercel) and MIT license.