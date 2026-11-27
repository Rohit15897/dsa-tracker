# CLAUDE.md — DSA Progress Tracker

## Project Overview

**DSA Progress Tracker** is a single-page web application for tracking progress solving Data Structures & Algorithms problems. It runs entirely in the browser with no backend, using local storage for persistence.

**Tech Stack:** HTML + CSS + vanilla JavaScript (no build step, no dependencies)

**Repository:** https://github.com/Rohit15897/dsa-tracker

---

## Code Style & Conventions

### HTML/CSS/JavaScript
- **No frameworks or build tools** — keep it simple and self-contained
- **Single file deployment** — `index.html` includes all CSS and JavaScript inline
- **CSS Variables** — use `var(--color-name)` for consistent theming
- **CSS Naming** — BEM-like naming for utility classes (e.g., `.status-badge`, `.difficulty-badge`)
- **JavaScript** — vanilla JS, no jQuery or other libraries
- **Comments** — only when the WHY is non-obvious; default: no comments

### File Organization
- **index.html** — All HTML, CSS, and JavaScript in a single file
  - `<style>` section at top (after `<head>`)
  - `<script>` section at bottom (before `</body>`)
- **README.md** — User-facing documentation
- **CLAUDE.md** — This file; Claude-specific guidelines

---

## Data Model

### Problem Object
```javascript
{
  id: number,              // Unix timestamp (Date.now())
  name: string,            // Problem title
  link: string,            // URL to problem (optional)
  topic: string,           // Category: Arrays, Trees, DP, etc.
  difficulty: string,      // Easy | Medium | Hard
  status: string,          // To Do | In Progress | Solved | Revisit
  notes: string,           // Solution approach/patterns
  dateSolved: string | null // Auto-filled when status = Solved
}
```

### Storage
- **Key:** `dsa_problems`
- **Value:** JSON stringified array of problem objects
- **Persistence:** Browser localStorage (automatic on every change)

---

## UI Conventions

### Colors & Status Badges
- **Easy:** Green (`#d4edda` bg, `#155724` text)
- **Medium:** Yellow/Orange (`#fff3cd` bg, `#856404` text)
- **Hard:** Red (`#f8d7da` bg, `#721c24` text)
- **Solved:** Green
- **In Progress:** Yellow
- **To Do:** Gray
- **Revisit:** Red

### Supported Topics
Arrays, Strings, Trees, Graphs, Linked Lists, Dynamic Programming, Stacks & Queues, Heaps, Hashing, Sorting, Searching, Greedy, Recursion, Bit Manipulation

Add new topics by editing the `topics` array in the JavaScript section.

---

## Feature Guidelines

### Adding Features
1. **Keep it in one file** — no separate JS/CSS files
2. **No external dependencies** — use vanilla JavaScript only
3. **Local storage only** — no backend or server calls
4. **Mobile responsive** — test at 375px+ viewport width
5. **Accessibility** — use semantic HTML, label form inputs

### Common Tasks

**Adding a new filter:**
- Create filter buttons in the HTML
- Add a new filter category to `currentFilter` object
- Create a `filterBy[Category]()` function
- Call `renderProblems()` after filter changes

**Adding a new field to problems:**
- Add input to the HTML form
- Update the Problem Object model above
- Update add/edit form handlers
- Add to table display if user-visible
- Update stats if relevant

**New status or difficulty:**
- Add to respective dropdown options in HTML
- Add CSS class for the badge (`.status-*` or `.difficulty-*`)
- Update stats calculation if needed

### Testing
- **Manual testing:** Add problems, edit, delete, filter, reload page
- **Data persistence:** Add problem, refresh page, verify it's still there
- **Filter accuracy:** Use all filter combinations
- **Edge cases:** Empty state, no results after filter, long text

---

## Common Changes & How to Approach Them

### Bug Fixes
- Verify the bug with manual testing first
- Check localStorage for data integrity
- Ensure filter state resets correctly
- Test across different browsers (Chrome, Firefox, Safari)

### Performance
- This app is lightweight — no optimization needed
- Local storage operations are O(1) for this scale
- If problems exceed 1000+, consider pagination

### Mobile Support
- Test at viewport width 375px (mobile preset)
- Ensure buttons are touchable (min 48px)
- Check form inputs work on mobile keyboard
- Test landscape orientation

---

## Commit Guidelines

- **Commits:** One logical change per commit
- **Messages:** Clear, imperative tone
  - Bad: "fixed the filter thing"
  - Good: "Fix topic filter not resetting on page reload"
- **Attribution:** Include co-author line:
  ```
  Co-Authored-By: Claude Haiku 4.5 <noreply@anthropic.com>
  ```

---

## Deployment

**How to deploy:**
1. Push to GitHub (main branch)
2. Enable GitHub Pages:
   - Settings → Pages
   - Source: Deploy from a branch
   - Branch: main, folder: / (root)
3. Access at: `https://rohit15897.github.io/dsa-tracker/`

**No build step required** — `index.html` is served directly.

---

## Known Limitations & Future Ideas

### Current Limitations
- No cross-device sync (browser-specific storage)
- No offline fallback beyond first load
- No search functionality
- No bulk operations (export/import)

### Future Enhancements
- CSV export / import
- LeetCode API sync
- Analytics dashboard (time trends, topic coverage)
- Dark mode toggle
- Multi-browser sync via GitHub Gist or personal server

---

## Resources

- **Repo:** https://github.com/Rohit15897/dsa-tracker
- **Local Dev:** Double-click `index.html` or start dev server on port 8000
- **MDN Docs:** localStorage, fetch API, DOM manipulation

---

## Questions for Claude

When making changes:
1. **Will this break existing data?** Check localStorage compat
2. **Is this mobile-friendly?** Test at 375px width
3. **Can this run without a backend?** It must
4. **Will the file still be valid HTML if served from GitHub Pages?** Yes

Default to keeping it simple. Avoid premature abstractions.
