# Keypad Style Guide — CareConnect Theme

Preferred style, color theme, and design for any keypad/numeric input needed in this project.

## ⚠️ CRITICAL USER PREFERENCE: EXTREMELY HIGH CONTRAST

**This user requires maximum contrast on all keypad elements. This is non-negotiable and must be applied without being asked every time.**

- All labels must be `rgba(255,255,255,.75)` or brighter — never below `.5` opacity
- All body text and values must be pure `#ffffff` or bright gold `#f0e080`
- Key backgrounds must be clearly lighter than the sheet background — minimum 3:1 contrast ratio
- Unselected chips must be clearly visible: `rgba(255,255,255,.85)` text, `rgba(255,255,255,.5)` border
- Placeholder text minimum `rgba(255,255,255,.5)`
- Hint/sublabel text minimum `rgba(255,255,255,.65)`
- Never use `rgba(255,255,255,.28)` or lower for any visible text

## Reference
Based on Ryan's CareConnect app keypad (bruinesq.github.io).

## Layout

- **Position**: Centered on screen — `position:fixed; top:50%; left:50%; transform:translate(-50%,-50%)`
- **Width**: `min(96vw, 420px)`
- **Border radius**: `16px` (fully rounded, floating card)
- **Box shadow**: `0 8px 40px rgba(0,0,0,.55)`
- **Overlay**: Full-screen dark backdrop `rgba(0,0,0,.6)` with `backdrop-filter:blur(2px)`, z-index 900
- **Sheet z-index**: 910
- **Max height**: `92vh` with `overflow-y:auto`
- **Never at the bottom of screen** — always centered to avoid nav bar obstruction

## Color Theme (Dark Green — High Contrast)

| Element | Color |
|---|---|
| Sheet background | `#0d2b1f` |
| Field boxes | `#1e4a34` (lighter than sheet for contrast) |
| Field border | `rgba(255,255,255,.25)` |
| Active field border | `#e8c84a` (gold) |
| Key background | `#5a8a70` (clearly lighter than sheet) |
| Key text | `#ffffff` pure white, `font-weight:700` |
| Delete key | `#c0392b` (bright red) |
| Confirm button | `#e8c84a` background, `#0d2b1f` text |
| Labels (UPPERCASE) | `rgba(255,255,255,.75)` — **never below .5** |
| Hint/sub text | `rgba(255,255,255,.7)` — **never below .65** |
| Amount number | `#f0e080` bright gold |
| Amount symbol | `#f0e080` bright gold, 16px |
| Unselected chips | `rgba(255,255,255,.85)` text, `rgba(255,255,255,.5)` border |
| Selected chip | `#e8c84a` bg, `#0d2b1f` text |
| Split box background | `#2a5040` |
| Split family name | `rgba(255,255,255,.85)` uppercase bold |
| Split people count | `#ffffff` 26px bold |
| Split amount | `#f0e080` bold |
| Description text | `#ffffff`, 13px |
| Description placeholder | `rgba(255,255,255,.5)` |

## Key Specifications

```css
.key {
  height: 54px;
  border-radius: 10px;
  font-size: 26px;
  font-weight: 700;
  color: #ffffff;
  background: #5a8a70;  /* must be clearly lighter than #0d2b1f sheet bg */
}
.key-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 7px;
  padding: 6px 14px;
}
.key.delete { background: #c0392b; }
.key.dot { font-size: 22px; font-weight: 700; }
```

## Structure (top to bottom)

1. **Handle bar** — 32px wide, 3px tall, `rgba(255,255,255,.2)`, centered, `border-radius:99px`
2. **Header row** — title (gold, uppercase) + Cancel button (ghost, rounded pill)
3. **Input fields** — stacked cards with `1.5px border`, `10px border-radius`
   - Active field: gold border `#e8c84a`
   - Amount field: large number left, USD/EUR toggle top-right inside same box
   - Date field: narrower, auto-populates with local date/time
4. **Category chips** — single scrollable row, `overflow-x:auto`, no wrap
5. **Paid by / Split among** — chip selectors
6. **3×4 Key grid** — 1/2/3 · 4/5/6 · 7/8/9 · ./0/DEL
7. **Confirm button** — full width, gold, 50px height, shows running total

## Amount Display

```
[€ symbol] [large number]          [USD | EUR toggle]
```
- Symbol: 13px gold `#e8c84a`
- Number: 28-32px white bold
- Toggle: inside the amount box, top-right corner, pill style

## Behavior

- Tapping a field clears `currDigits` to `''` (replace, not append)
- Limit: 2 digits for people counts, unlimited for amounts
- Keypad context switches based on active field
- Hint line below split boxes shows: `N people · $X.XX/person`
- Confirm button echoes total: `Save · $420.00` or `Save · €350 → $381.50`

## Event Handling

- Use `data-*` attributes on all interactive elements
- Single delegated `document.addEventListener('click', handler, true)`
- Register listener only once (guard with `window._listenerAdded` flag)
- Check `[data-cur]` BEFORE `[data-kpf]` in handler to prevent currency toggle being swallowed by parent div

## Critical: No Re-render While Open

- Any `setInterval` polling must check `kpSheet.classList.contains('open')` and skip `renderPanel()` if true
- `refreshKP()` rebuilds only the sheet innerHTML — never calls `renderPanel()`
