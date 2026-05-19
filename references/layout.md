# Layout · Complex Panel Reference

Structural templates for multi-panel report pages. Always used together with references/plan.md.

## Critical rule

This file provides structure only.
All font sizes, colors, and spacing must come from the template's existing CSS variables.
layout.md is a supporter, not an overrider. It never takes precedence over the template CSS or design.md.

All layout classes use the .l- prefix (e.g. .l-left-panel, .l-hero-block) to prevent conflicts with template classes. Never rename them when copying into a template <style> block.

## When to use

| Situation | Layout |
|---|---|
| One chart is the whole story | L03 — Hero Visual |
| Data table + supporting chart | L04 — Strategic Matrix |
| Text argument + chart proof | L01 — SCR TwoColumn |

---

## L01 — SCR TwoColumn (40 / 60 Split)

**When to use:** Text argument left, chart proof right.

```

┌─────────────────────────────────────────────────────────────────────────────────────┐
│  ......                                                                        ...... │
│   ......                                                                        ......│
├──────────────────────────────────────────┬──────────────────────────────────────────┤
│  LEFT 40%                                │  RIGHT 60%                               │
│                                          │                                           │
│  SITUATION                               │  [ Chart PNG — fills all height ]        │
│  2–3 sentences of context.               │                                           │
│                                          │                                           │
│  COMPLICATION                            │  ─────────────────────────────────────   │
│  2–3 sentences of tension.               │                                           │
│                                          │  ①  Imperative one — action headline     │
│  RESOLUTION                              │                                           │
│  2–3 sentences of answer.                │  ②  Imperative two — action headline     │
│                                          │                                           │
│  ── Risk Matrix ──────────────────   │  ③  Imperative three — action headline   │
│  ┌─────────────┐  ┌─────────────┐  │                                           │
│  │ Risk card 1   │  │ Risk card 2 │     │                                           │
│  ├─────────────┤  ├─────────────┤  │                                           │
│  │ Risk card 3   │  │ Risk card 4 │     │                                           │
│  └─────────────┘  └─────────────┘   │                                           │
├──────────────────────────────────────────┴──────────────────────────────────────────┤
│  Takeaway — one sentence with brand left border                                      │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                         .......                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘

**Structural CSS:**

```css
/* slide-body stays flex-direction: row (default) */
.l-left-panel {
  width: 40%;
  padding: var(--space-md) var(--space-lg) var(--space-sm) var(--space-xl);
  display: flex;
  flex-direction: column;
  border-right: 1px solid var(--border);
  overflow: hidden;
}
.l-right-panel {
  width: 60%;
  padding: var(--space-md) var(--space-xl) var(--space-sm) var(--space-lg);
  display: flex;
  flex-direction: column;
  background: var(--parchment);
}
.l-scr-block  { margin-bottom: 8px; flex-shrink: 0; }
.l-scr-label  {
  font-family: var(--sans); font-weight: 600;
  text-transform: uppercase; letter-spacing: 1.5pt;
  color: var(--brand); margin-bottom: 2px;
  /* font-size: use template --label variable */
}
.l-scr-text   { line-height: 1.55; color: var(--olive); }
.l-risk-grid  { display: grid; grid-template-columns: 1fr 1fr; gap: var(--space-xs); flex: 1 1 0; min-height: 0; }
.l-rc         { background: var(--ivory); padding: 6px 8px; border-radius: 3pt; display: flex; flex-direction: column; gap: 2px; }
.l-rc-name    { font-weight: 500; color: var(--brand); line-height: 1.25; }
.l-rc-desc    { line-height: 1.45; color: var(--stone); }
/* Severity tags — solid hex only, never rgba (see production.md Pitfall 1) */
.l-tag        { font-family: var(--sans); font-weight: 600; letter-spacing: .06em; text-transform: uppercase; padding: 1px 5px; border-radius: 3px; }
.l-tag-crit   { color: #B53333; background: #F5E4E4; }
.l-tag-high   { color: #7A4A00; background: #F5EDD4; }
.l-tag-med    { color: var(--brand); background: var(--brand-tint-strong); }
.l-imp-grid   { display: grid; grid-template-columns: 1fr; gap: var(--space-sm); flex-shrink: 0; margin-top: 7px; }
.l-imp        { border-top: 2px solid var(--brand); padding-top: 7px; display: flex; flex-direction: column; gap: 3px; }
.l-imp-num    {
  width: 18px; height: 18px; border-radius: 50%;
  background: var(--brand); color: var(--parchment);
  font-family: var(--sans); font-weight: 600;
  display: flex; align-items: center; justify-content: center;
  margin-bottom: 2px; flex-shrink: 0;
}
.l-imp-title  { font-weight: 500; color: var(--near-black); line-height: 1.25; }
.l-imp-text   { line-height: 1.48; color: var(--olive); }
```

---

## L03 — Hero Visual (Full Canvas)

**When to use:** One chart is the primary story. Annotation row sits below.

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│   ......                                                                                    ...│
│   .....                                                                                     ....│
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│  Intro text — 2 sentences max, states what the chart shows                          │
│                                                                                      │
│  CHART LABEL                                                                         │
│  ┌───────────────────────────────────────────────────────────────────────────────┐  │
│  │                                                                               │  │
│  │                  [ Hero Chart PNG — grows to fill all available space ]       │  │
│  │                                                                               │  │
│  │                                                                               │  │
│  └───────────────────────────────────────────────────────────────────────────────┘  │
│  Caption — states the insight, not just the data range                               │
│                                                                                      │
│  ── Annotation row ────────────────────────────────────────────────────────────────  │
│  ┌───────────────┐   ┌───────────────┐   ┌───────────────┐   ┌───────────────┐     │
│  │  LABEL        │   │  LABEL        │   │  LABEL        │   │  LABEL        │     │
│  │  Body text    │   │  Body text    │   │  Body text    │   │  Body text    │     │
│  └───────────────┘   └───────────────┘   └───────────────┘   └───────────────┘     │
├─────────────────────────────────────────────────────────────────────────────────────┤
│  Takeaway — one sentence with brand left border                                      │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                         .......                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘

**Structural CSS:**

```css
.l-slide-body {
  flex-direction: column;
  padding: var(--space-sm) var(--space-xl) var(--space-xs) var(--space-xl);
}
.l-hero-block     { display: flex; flex-direction: column; flex: 1 1 0; min-height: 0; }
.l-hero-block img { width: 100%; flex: 1 1 0; min-height: 0; object-fit: fill; display: block; }
.l-annotation-row {
  display: flex; flex-direction: row;
  border-top: 1px solid var(--border);
  padding-top: var(--space-xs);
  flex-shrink: 0;
}
.l-ann-item {
  flex: 1;
  padding-right: var(--space-lg);
  border-right: 1px solid var(--border);
  margin-right: var(--space-lg);
}
.l-ann-item:last-child { border-right: none; margin-right: 0; padding-right: 0; }
.l-ann-label {
  font-family: var(--sans); font-weight: 600;
  text-transform: uppercase; letter-spacing: 1.5pt;
  color: var(--brand); margin-bottom: 3px;
}
.l-ann-body { line-height: 1.5; color: var(--olive); }
```

---

## L04 — Strategic Matrix (Table Top + Chart Bottom)

**When to use:** Data table is the primary reference, chart fills space below.

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│   ......                                                                                    ...│
│   .....                                                                                     ....│
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│  Intro text — 2 sentences max                                                        │
│                                                                                      │
│  TABLE LABEL                                                                         │
│  ┌───────────────┬────────────────────────┬─────────────┬─────────────┬──────────┐  │
│  │  Column       │  Column                │  Column     │  Column     │  Stars    │  │
│  ├───────────────┼────────────────────────┼─────────────┼─────────────┼──────────┤  │
│  │  Row value    │  Row value             │  [badge]    │  Row value  │  ★★★★☆   │  │
│  │  Row value    │  Row value             │  [badge]    │  Row value  │  ★★★☆☆   │  │
│  │  Row value    │  Row value             │  [badge]    │  Row value  │  ★★☆☆☆   │  │
│  └───────────────┴────────────────────────┴─────────────┴─────────────┴──────────┘  │
│                                                                                      │
│  CHART LABEL                                                                         │
│  ┌───────────────────────────────────────────────────────────────────────────────┐  │
│  │                [ Chart PNG — fills all remaining vertical space ]                 │  │
│  └───────────────────────────────────────────────────────────────────────────────┘  │
│  Caption                                                                             │
├─────────────────────────────────────────────────────────────────────────────────────┤
│  Takeaway — one sentence with brand left border                                      │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                         .......                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘

**Structural CSS:**

```css
.l-slide-body {
  flex-direction: column;
  padding: var(--space-sm) var(--space-xl) var(--space-xs) var(--space-xl);
}
table       { width: 100%; border-collapse: collapse; flex-shrink: 0; font-family: var(--sans); }
thead tr    { background: var(--brand); }
th          { font-weight: 600; letter-spacing: .08em; text-transform: uppercase; color: #fff; padding: 6px 9px; text-align: left; white-space: nowrap; }
td          { padding: 5px 9px; color: var(--near-black); border-bottom: .5px solid var(--border); font-family: var(--serif); }
tr:nth-child(even) td { background: rgba(27,54,93,0.03); }
td:first-child        { font-weight: 500; }
.l-stars      { color: var(--brand); letter-spacing: 1px; }
.l-chart-fill     { flex: 1 1 0; min-height: 0; display: flex; flex-direction: column; }
.l-chart-fill img { width: 100%; flex: 1 1 0; min-height: 0; object-fit: fill; display: block; }
```



---

## Layout decision guide

1. Single chart dominates → L03
2. Table + chart → L04
3. Text argument + chart → L01
4. When unsure between L01 and L03: if chart needs more than 50% page height to read clearly → L03
