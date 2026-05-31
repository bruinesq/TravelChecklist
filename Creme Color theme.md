# Cream Color Theme — Style Guide

Warm, sand/cream palette. Light, airy, easy to read in daylight. Used in the Split tab of the Family Travel app.

## Color Palette

| Role | Hex | Usage |
|---|---|---|
| Page background | `#f5f0e8` | Main screen bg, alternating row A |
| Surface / row B | `#ede7d9` | Cards, stat boxes, alternating row B, sort pill |
| Border | `#cdc7bb` | All dividers, card borders |
| Stronger border | `#d4cfc6` | Phone/panel outer border |
| Label / muted text | `#8a7a60` | UPPERCASE labels, secondary info |
| Body text | `#5a4a38` | Meta lines, descriptions |
| Split detail text | `#7a6a58` | Per-family breakdown lines |
| Primary text | `#1a120a` | Names, amounts, headings |
| Accent / brand | `#7A4F0B` | Section titles, sort value, add button, active toggle bg |
| Amount highlight | `#7A4F0B` | Expense amounts |

## Semantic Colors (Settlement)

| State | Background | Border | Text |
|---|---|---|---|
| Positive (owed) | `#d4edda` | `#a8d5b5` | `#1B5E20` |
| Negative (owes) | `#fde8e8` | `#f5b8b8` | `#c0392b` |
| Neutral / zero | `#ede7d9` | `#cdc7bb` | `#7a6a58` |

## Family Colors (dots and accents)

| Family | Color |
|---|---|
| JMCR | `#534AB7` (purple) |
| Matthews | `#993C1D` (coral/red) |
| Silvermans | `#854F0B` (amber) |

## Category Badge Colors (color-blind safe)

| Category | Background | Text |
|---|---|---|
| Food | `#FFCCBC` | `#8B1A00` |
| Activity | `#BBDEFB` | `#003070` |
| Transport | `#FFF59D` | `#7A4F00` |
| Lodging | `#B2EBF2` | `#006064` |
| Docking | `#FCE4EC` | `#880041` |
| Restaurant | `#FFCCBC` | `#8B1A00` |
| Tour | `#B2EBF2` | `#006064` |

## Typography

- All labels: `9px`, `font-weight:700`, `text-transform:uppercase`, `letter-spacing:.05em`, color `#8a7a60`
- Body / meta: `12px`, color `#5a4a38`
- Split detail lines: `11px`, color `#7a6a58`, `line-height:1.5`
- Expense title: `15px`, `font-weight:700`, color `#1a120a`
- Amounts: `16–20px`, `font-weight:700`, color `#7A4F0B`
- Section accent title: `12px`, `font-weight:700`, `letter-spacing:.08em`, `text-transform:uppercase`, color `#7A4F0B`

## Component Specs

### Stat / Sort Row
```css
grid-template-columns: 1fr 1fr 1fr;
gap: 6px;
padding: 10px 12px 6px;
```
Each cell: `background:#ede7d9; border-radius:8px; padding:8px 10px; border:0.5px solid #cdc7bb`

### Toggle Bar (Expenses / Settlement)
```css
background: #ede7d9;
border: 1px solid #cdc7bb;
border-radius: 8px;
overflow: hidden;
margin: 2px 12px 8px;
```
Active button: `background:#7A4F0B; color:#fff`
Inactive button: `color:#a89880`

### Alternating Expense Rows
- Row A (odd): `background:#f5f0e8` (page bg — blends seamlessly)
- Row B (even): `background:#ede7d9` (slightly darker)
- Border between: `0.5px solid #cdc7bb`
- Padding: `12px 14px`

### Delete Button (ghost)
```css
font-size: 10px;
color: #a08060;
background: none;
border: 1px solid #cdc7bb;
border-radius: 99px;
padding: 2px 8px;
margin-top: 5px;
```

### Net Banner Cards (Settlement)
```css
border-radius: 8px;
padding: 8px 10px;
text-align: center;
border: 0.5px solid [semantic border];
```
- Name: `9px`, `font-weight:700`, `text-transform:uppercase`
- Amount: `15px`, `font-weight:700`
- Sub-label: `9px`

### Reimbursement Rows (Settlement)
Same alternating pattern as expense rows.
Amount column: `font-size:20px; font-weight:700; color:#1B5E20; margin-left:auto`
Family name: `font-size:14px; font-weight:700; color:#1a120a`
Arrow icon: `color:#cdc7bb`

## Rules

- No white (`#ffffff`) anywhere — use `#f5f0e8` (lightest cream) instead
- No pure black — use `#1a120a` for darkest text
- No gradients, no shadows (except the outer panel border)
- All borders `0.5px` except the toggle bar (`1px`)
- Border radius: `8px` for stat cards and net banner; `12px` for the outer panel
- Font weight: `700` for headings and amounts only; `600` for toggle active; everything else `400–500`
