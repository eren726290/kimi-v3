# Plan · Page-by-Page Build Protocol

Use this protocol for any multi-page PDF report (2+ pages). Prevents content overflow and enforces clean WeasyPrint page boundaries.

## When to use

Trigger automatically when building:
- Equity reports
- Long-doc / white papers
- Any document where the user mentions a page count or multiple pages

Do NOT use for single-page documents (resume, one-pager, letter).

---

## Step P1 · Declare the job

Before writing any HTML, create PLAN.md in the working directory:

```
# Report Job: [Title]

## Project Details
- Subject: [Name]
- Total Pages: [N]
- Page size: 10in 7.5in (4:3 landscape)

## Pages
- [ ] page_01_cover.html
- [ ] page_02_exec_summary.html
- [ ] page_03_[section].html
- [ ] page_04_[section].html
- [ ] page_05_[section].html
- [ ] page_06_[section].html
- [ ] page_07_[section].html

## Rules
- One HTML file = one page exactly
- For complex panel layouts (two-column, hero chart, KPI grid,ect) consult references/layout.md for structure only — never copy font sizes from it
- Mark [x] after each page is verified
- Never build next page before marking current [x]
- Font sizes and CSS tokens come from the template only
```

---

## Step P2 · Build and verify each page

For each page:

1. Write the HTML file
2. Render it:
python3 -c "from weasyprint import HTML; HTML('page_01_cover.html').write_pdf('page_01_cover.pdf')"

3. Count pages — must be exactly 1:
python3 -c "from pypdf import PdfReader; print(len(PdfReader('page_01_cover.pdf').pages))"

4. If count is more than 1: reduce content until it fits. Do not proceed.
5. Mark [x] in PLAN.md for that page.

---

## Step P3 · Stitch all pages into final PDF

After all pages are marked [x]:

from pypdf import PdfWriter, PdfReader
import glob

writer = PdfWriter()
for path in sorted(glob.glob('page_*.pdf')):
    reader = PdfReader(path)
    for page in reader.pages:
        writer.add_page(page)

with open('report_final.pdf', 'wb') as f:
    writer.write(f)

print(f"Final PDF: {len(writer.pages)} pages")

Save as stitch.py and run:
python3 stitch.py
