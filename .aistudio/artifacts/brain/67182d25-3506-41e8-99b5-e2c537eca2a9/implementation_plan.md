# Left-Hand Links Menu & Social Profile Navigation

Implement a clean, understated left-hand menu of profile and external links (GitHub, X `@daveeeh`, Google Play, and future additions), driven by a maintainable vanilla JavaScript `LINKS` array and responsive across desktop and mobile.

## User Review & Critical Decisions

> [!IMPORTANT]
> The following design decisions were confirmed during the planning clarification:

- **Placement**: Clean list on the left-hand side (like an editorial sidebar menu) on desktop, transitioning to a clean, accessible layout on mobile devices.
- **Link Styling**: Uncluttered text links with subtle arrow indicators (`↗`), hover transitions, and clean typography matching the British minimalist design.
- **Maintenance**: Driven by a clean, self-contained `const LINKS = [...]` array at the bottom of `index.html` so you can add, remove, or edit links in seconds.

---

## 1. Overview & Core Concept

- **What It Does**: Enhances the portfolio with a dedicated navigation column on desktop displaying David's online presence (GitHub, X, Google Play, Email) and makes future additions trivial.
- **Target Audience**: Visitors, recruiters, and fellow developers browsing Hodges.dev who want to view David's open-source repositories, social updates, and developer profiles.
- **Key Value**: Organises profile links in a natural, persistent position on desktop without cluttering the main app cards list or hiding them in the footer.

---

## 2. User Experience & Visual Design

### Desktop Layout ($>768\text{px}$)
- The `#3F51B5` Android-style collapsing toolbar remains pinned at the very top.
- The content area below the toolbar adopts a 2-column layout:
  - **Left Column (Sidebar Menu ~220px)**:
    - Sticky or persistent column featuring the bio paragraph.
    - A dedicated **"Links"** section featuring:
      - GitHub
      - X (`@daveeeh`)
      - Google Play Profile
      - Email (`david+website@hodges.dev`)
      - Space for future links (LinkedIn, Blog, etc.)
  - **Right Column (Main Content)**:
    - The dynamic "Apps" header with the active project count.
    - The interactive app cards list (*andMoney*, *VolumeLink*, *TFC Tracker*, *BusWatch*, *Exchange Folder Sync*, *Song Notifications*).
    - Privacy note and footer.

### Mobile Layout ($<768\text{px}$)
- Stacks cleanly into a natural single column.
- The Links menu displays as an elegant horizontal scrolling bar or a tidy 2-column grid of text links right below the bio, before the Apps list.
- Maintains touch-friendly targets ($\ge 44\text{px}$) and zero overflow.

---

## 3. Data Model & Maintainability

All links are defined in a clean array right next to `APPS`:

```javascript
const LINKS = [
  { label: "GitHub", url: "https://github.com/davidhodges", note: "Source code & repos" },
  { label: "X / Twitter", url: "https://x.com/daveeeh", note: "@daveeeh" },
  { label: "Google Play", url: "https://play.google.com/store/apps/dev?id=4749300962545882389", note: "Developer Profile" },
  { label: "Email", url: "mailto:david+website@hodges.dev", note: "david+website@hodges.dev" }
];
```

To add a new link in the future, you simply paste one more `{ label: "...", url: "..." }` item into the array.

---

## 4. Technical Architecture & Component Layout

```
┌─────────────────────────────────────────────────────────────┐
│ Android App Toolbar (#3F51B5 - Sticky CollapsingToolbar)     │
└─────────────────────────────────────────────────────────────┘
                              │
            ┌─────────────────┴─────────────────┐
            ▼                                   ▼
┌───────────────────────┐           ┌─────────────────────────┐
│ Left Sidebar (Desktop)│           │ Main Content Column     │
│                       │           │                         │
│ • Bio & Background    │           │ • Apps Header & Count   │
│ • Links Menu:         │           │ • App Cards (andMoney,  │
│   - GitHub ↗          │           │   VolumeLink, etc.)     │
│   - X (@daveeeh) ↗    │           │ • Privacy Note          │
│   - Google Play ↗     │           │ • Footer                │
│   - Email ↗           │           │                         │
│   (Rendered via LINKS)│           │                         │
└───────────────────────┘           └─────────────────────────┘
```

- **Zero Build Requirement**: Kept 100% inside `index.html` with Tailwind CDN and vanilla JS, preserving full compatibility with GitHub Pages.
- **Progressive Enhancement**: Automatically populates `renderLinks()` alongside `renderApps()`.
