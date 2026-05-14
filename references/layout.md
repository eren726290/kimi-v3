# Layout · Complex Panel Reference

Structural templates for multi-panel report pages. Always used together with references/plan.md.

## Critical rule

This file provides structure only.
All font sizes, colors, and spacing must come from the template's existing CSS variables.
layout.md is a supporter, not an overrider. It never takes precedence over the template CSS or design.md.

## When to use

| Situation | Layout |
|---|---|
| key findings| L05 — Executive Snapshot |
| One chart is the whole story | L03 — Hero Visual |
| Data table + supporting chart | L04 — Strategic Matrix |
| Text argument + chart proof | L01 — SCR TwoColumn |

---

## L01 — SCR TwoColumn (40 / 60 Split)

**When to use:** Text argument left, chart proof right.

```

┌─────────────────────────────────────────────────────────────────────────────────────┐
│   ......                                                                                    ...│
│   .....                                                                                     ....│
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
.left-panel {
  width: 40%;
  padding: var(--space-md) var(--space-lg) var(--space-sm) var(--space-xl);
  display: flex;
  flex-direction: column;
  border-right: 1px solid var(--border);
  overflow: hidden;
}
.right-panel {
  width: 60%;
  padding: var(--space-md) var(--space-xl) var(--space-sm) var(--space-lg);
  display: flex;
  flex-direction: column;
  background: var(--parchment);
}
.scr-block  { margin-bottom: 8px; flex-shrink: 0; }
.scr-label  {
  font-family: var(--sans); font-weight: 600;
  text-transform: uppercase; letter-spacing: 1.5pt;
  color: var(--brand); margin-bottom: 2px;
  /* font-size: use template --label variable */
}
.scr-text   { line-height: 1.55; color: var(--olive); }
.risk-grid  { display: grid; grid-template-columns: 1fr 1fr; gap: var(--space-xs); flex: 1 1 0; min-height: 0; }
.rc         { background: var(--ivory); padding: 6px 8px; border-radius: 3pt; display: flex; flex-direction: column; gap: 2px; }
.rc-name    { font-weight: 500; color: var(--brand); line-height: 1.25; }
.rc-desc    { line-height: 1.45; color: var(--stone); }
/* Severity tags — solid hex only, never rgba (see production.md Pitfall 1) */
.tag        { font-family: var(--sans); font-weight: 600; letter-spacing: .06em; text-transform: uppercase; padding: 1px 5px; border-radius: 3px; }
.tag-crit   { color: #B53333; background: #F5E4E4; }
.tag-high   { color: #7A4A00; background: #F5EDD4; }
.tag-med    { color: var(--brand); background: var(--brand-tint-strong); }
.imp-grid   { display: grid; grid-template-columns: 1fr; gap: var(--space-sm); flex-shrink: 0; margin-top: 7px; }
.imp        { border-top: 2px solid var(--brand); padding-top: 7px; display: flex; flex-direction: column; gap: 3px; }
.imp-num    {
  width: 18px; height: 18px; border-radius: 50%;
  background: var(--brand); color: var(--parchment);
  font-family: var(--sans); font-weight: 600;
  display: flex; align-items: center; justify-content: center;
  margin-bottom: 2px; flex-shrink: 0;
}
.imp-title  { font-weight: 500; color: var(--near-black); line-height: 1.25; }
.imp-text   { line-height: 1.48; color: var(--olive); }
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
.slide-body {
  flex-direction: column;
  padding: var(--space-sm) var(--space-xl) var(--space-xs) var(--space-xl);
}
.hero-block     { display: flex; flex-direction: column; flex: 1 1 0; min-height: 0; }
.hero-block img { width: 100%; flex: 1 1 0; min-height: 0; object-fit: fill; display: block; }
.annotation-row {
  display: flex; flex-direction: row;
  border-top: 1px solid var(--border);
  padding-top: var(--space-xs);
  flex-shrink: 0;
}
.ann-item {
  flex: 1;
  padding-right: var(--space-lg);
  border-right: 1px solid var(--border);
  margin-right: var(--space-lg);
}
.ann-item:last-child { border-right: none; margin-right: 0; padding-right: 0; }
.ann-label {
  font-family: var(--sans); font-weight: 600;
  text-transform: uppercase; letter-spacing: 1.5pt;
  color: var(--brand); margin-bottom: 3px;
}
.ann-body { line-height: 1.5; color: var(--olive); }
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
.slide-body {
  flex-direction: column;
  padding: var(--space-sm) var(--space-xl) var(--space-xs) var(--space-xl);
}
table       { width: 100%; border-collapse: collapse; flex-shrink: 0; font-family: var(--sans); }
thead tr    { background: var(--brand); }
th          { font-weight: 600; letter-spacing: .08em; text-transform: uppercase; color: #fff; padding: 6px 9px; text-align: left; white-space: nowrap; }
td          { padding: 5px 9px; color: var(--near-black); border-bottom: .5px solid var(--border); font-family: var(--serif); }
tr:nth-child(even) td { background: rgba(27,54,93,0.03); }
td:first-child        { font-weight: 500; }
.stars      { color: var(--brand); letter-spacing: 1px; }
.chart-fill     { flex: 1 1 0; min-height: 0; display: flex; flex-direction: column; }
.chart-fill img { width: 100%; flex: 1 1 0; min-height: 0; object-fit: fill; display: block; }
```

---

## L05 — Executive Snapshot (Cover / KPI Strip)

**When to use:** 4 key findings.

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│   ......                                                                                    ...│
│   .....                                                                                     ....│
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                      │
│   SUMMARY                                                                            │
│  3–4 sentence overview paragraph providing strategic context and key takeaways.      │
│                                                                                      │
│  ┌────────────────────────────────────────┐  ┌────────────────────────────────────┐ │
│  │  FINDING 01                                   │  │  FINDING 02                        │ │
│  │                                               │  │                                    │ │
│  │                                                │  │                                    │ │
│  │  Finding title — short noun phrase             │  │  Finding title — short noun phrase │ │
│  │  Body text 2 sentences. Concise.               │  │  Body text 2 sentences. Concise.   │ │
│  └────────────────────────────────────────┘  └────────────────────────────────────┘ │
│                                                                                      │
│  ┌────────────────────────────────────────┐  ┌────────────────────────────────────┐ │
│  │  FINDING 03                                   │  │  FINDING 04                        │ │
│  │                                               │  │                                    │ │
│  │                                               │  │                          │ │
│  │  Finding title — short noun phrase             │  │  Finding title — short noun phrase │ │
│  │  Body text 2 sentences. Concise.               │  │  Finding title — short noun phrase │ │
│  └────────────────────────────────────────┘  └────────────────────────────────────┘ │
│                                                                                      │
├─────────────────────────────────────────────────────────────────────────────────────┤
│                                         .......                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘

**Structural CSS:**

```css
.slide-body {
  flex-direction: column;
  padding: var(--space-md) var(--space-xl) var(--space-sm) var(--space-xl);
  gap: var(--space-sm);
}
.exec-block     { flex-shrink: 0; }
.exec-overline  {
  font-family: var(--sans); font-weight: 600;
  text-transform: uppercase; letter-spacing: 1.8pt; color: var(--brand);
  border-left: 2px solid var(--brand);
  padding-left: var(--space-xs); margin-bottom: var(--space-xs);
}
.exec-text      { line-height: 1.58; color: var(--olive); }
.findings-grid  {
  display: grid; grid-template-columns: 1fr 1fr;
  gap: var(--space-sm);
  flex: 1 1 0; min-height: 0;
}
.finding        {
  border-top: 2px solid var(--brand);
  padding: var(--space-sm) var(--space-sm) var(--space-sm) 0;
  display: flex; flex-direction: column; gap: 4px;
}
.finding-num    { font-family: var(--sans); font-weight: 600; text-transform: uppercase; letter-spacing: 1.5pt; color: var(--stone); }
.finding-metric { font-weight: 500; color: var(--brand); line-height: 1; font-variant-numeric: tabular-nums; letter-spacing: -0.3pt; }
.finding-title  { font-weight: 500; color: var(--near-black); line-height: 1.25; }
.finding-body   { line-height: 1.5; color: var(--olive); }
```

---

## Layout decision guide

1. key findings→ L05
2. Single chart dominates → L03
3. Table + chart → L04
4. Text argument + chart → L01
5. When unsure between L01 and L03: if chart needs more than 50% page height to read clearly → L03
