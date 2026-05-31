# Keypad Style Guide — CareConnect Theme

Preferred style, color theme, and design for any keypad/numeric input needed in this project.

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

## Color Theme (Dark Green)

| Element | Color |
|---|---|
| Sheet background | `#0d2b1f` |
| Field boxes | `#1a3d2b` |
| Active field border | `#e8c84a` (gold) |
| Key background | `#4a6b58` (medium green) |
| Key text | `#ffffff` pure white |
| Delete key | `#c0392b` (bright red) |
| Confirm button | `#e8c84a` background, `#0d2b1f` text |
| Labels | `rgba(255,255,255,.38)` uppercase |
| Hint text | `rgba(255,255,255,.28)` |
| Active display value | `#e8c84a` gold |
| Currency/category chip active | `#e8c84a` bg, `#0d2b1f` text |

## Key Specifications

```css
.key {
  height: 54px;
  border-radius: 10px;
  font-size: 26px;
  font-weight: 600;
  color: #ffffff;
  background: #4a6b58;
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
