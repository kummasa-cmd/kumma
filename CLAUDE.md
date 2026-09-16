# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project status

This repository currently contains only `requirements.md` — no code has been written yet. The project is a
single-page promotional landing site for author 검마사 홍성호 (Hong Seong-ho), who has published 12 e-books and
1 print book. `requirements.md` is the full spec (Korean) and is the source of truth for content, copy, data,
and design decisions — read it in full before implementing or modifying the page.

There is no build system, package manager, or test suite yet because no code exists. When the site is first
implemented, follow §6 of `requirements.md`: a single static HTML file (or standard static page) with CSS/JS
inlined, no framework required unless the user asks for one.

## Key constraints from requirements.md

- **Single page, section order matters** (§3): nav → hero → about → print-book section → e-book (12 books)
  section → coaching (e-book coaching / print-book coaching) → newsletter ("검레터") signup → author
  activity/SNS → footer. Print book and e-books must be in **separate** sections, not merged.
- **Brand palette** derives from the print book cover 《루틴의 설계》: deep teal backgrounds
  (`#007E9E`/`#006780`, darker `#04566B`/`#0A5C6F`), off-white sections (`#F5F7F8`/`#FBFCFC`), gold/yellow
  accent used sparingly for buttons/highlights (`#FCD33F`/`#E2C854`), teal-charcoal body text (`#17303B`) on
  light backgrounds, white text on teal backgrounds. Maintain WCAG AA contrast.
- **Typography**: Noto Serif KR for headings/quotes/emphasis (editorial, trustworthy feel), Pretendard
  (fallback Noto Sans KR) for body/UI/labels. Preload Google Fonts with `display=swap`.
- **Book/product data** (titles, publish dates, categories, sales links for all 12 e-books plus the print
  book) is fully enumerated in §4-5 and §4-4 of `requirements.md` — treat that table as authoritative rather
  than re-deriving or guessing links.
- **Image sourcing rule (§5)**: book thumbnails must be the actual representative cover image from each
  book's official detail page (Kyobo for the print book, YES24 for each e-book) — never generate or composite
  cover art. Use `loading="lazy"`, explicit `width`/`height`, and descriptive `alt` text.
- **External links**: all outbound links need `target="_blank" rel="noopener"`.
- **Accessibility**: correct heading hierarchy, semantic tags, `aria-label` on icon buttons, labeled form
  inputs with inline validation.

## Unresolved items requiring verification before shipping (§8 of requirements.md)

These are explicitly flagged as needing confirmation — do not silently resolve them with guesses:

1. E-book #10 (「코드를 짜던 사람이 삶을 기록하기 시작했다」) has a YES24 product ID that duplicates #8's ID in
   the source data — the real product ID must be re-verified against the actual YES24 listing (watch for
   collision with #11's ID `177256726`).
2. The newsletter ("검레터") subscription form/landing URL is a placeholder — must be replaced with the
   author's real subscription endpoint before launch.
3. The one-line descriptions for each of the 12 e-books in §4-5 are draft copy based on titles/categories
   only — should be refined against each book's actual YES24 detail-page description.
4. Additional SNS channels (YouTube/Facebook) should only be added if confirmed present on
   kummasa.com — do not add unconfirmed channels.
