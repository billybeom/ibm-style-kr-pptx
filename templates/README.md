# IBM PPTX Template Repository

> Unpacked from `IBM_presentation_sample_layouts_v_2_1_Plex.pptx`

Each subdirectory contains the raw OpenXML slide files (`.xml`) for a specific template section.
Slides are numbered sequentially within each section (`slide-01.xml`, `slide-02.xml`, …).

For full style documentation, see [`../PPTX-STYLE.md`](../PPTX-STYLE.md).

---

## Directory Structure

```
templates/
├── IBM_presentation_sample_layouts_v_2_1_Plex.pptx     ← source file
├── IBM_pptx_extracted/                                   ← full zip extraction
├── Templates-Cover/               slides 1–12
├── Templates-Big-Trending/        slides 13–18
├── Templates-1-Column/            slides 19–22
├── Templates-2-Columns/           slides 23–38
├── Templates-3-Columns/           slides 39–53
├── Templates-4-Columns/           slides 54–60
├── Templates-2-Rows/              slide  61
├── Templates-3-Rows/              slides 62–65
├── Templates-2-Rows-2-Columns/    slides 66–69
├── Templates-2-Rows-3-Columns/    slide  70
├── Templates-2-Rows-4-Columns/    slides 71–72
├── Templates-3-Rows-3-Columns/    slide  73
├── Template-Project-Plan/         slides 74–75
├── Templates-Table/               slides 76–79
└── Template-Ending/               slide  80
```

---

## Section Summary

| Section | Files | Global Slides | Key Layouts |
|---------|-------|---------------|-------------|
| [Templates-Cover](Templates-Cover/) | 12 | 1–12 | Cover, imagery, half · Cover, plain, label · Cover, imagery, half, label · Cover, cyan |
| [Templates-Big-Trending](Templates-Big-Trending/) | 6 | 13–18 | Large text · Data, 2 callouts, vertical |
| [Templates-1-Column](Templates-1-Column/) | 4 | 19–22 | Video or imagery, half, inset · Text, 2 wide columns |
| [Templates-2-Columns](Templates-2-Columns/) | 16 | 23–38 | Text, 2 wide columns · Text, 2 columns, dividers, large title · Boxes, 4 stacked, large title |
| [Templates-3-Columns](Templates-3-Columns/) | 15 | 39–53 | Text, 4 columns · Boxes, 4 horizontal, large title · Data, 3 callouts, vertical |
| [Templates-4-Columns](Templates-4-Columns/) | 7 | 54–60 | Text, 4 columns · Boxes, 4 horizontal, large title |
| [Templates-2-Rows](Templates-2-Rows/) | 1 | 61 | Boxes, 4 stacked, small title |
| [Templates-3-Rows](Templates-3-Rows/) | 4 | 62–65 | Data, 3 callouts, horizontal |
| [Templates-2-Rows-2-Columns](Templates-2-Rows-2-Columns/) | 4 | 66–69 | Boxes, 4 stacked, small title · Boxes, 4 horizontal, large title |
| [Templates-2-Rows-3-Columns](Templates-2-Rows-3-Columns/) | 1 | 70 | Blank slide |
| [Templates-2-Rows-4-Columns](Templates-2-Rows-4-Columns/) | 2 | 71–72 | Boxes, 6 stacked, alternate, large title |
| [Templates-3-Rows-3-Columns](Templates-3-Rows-3-Columns/) | 1 | 73 | Boxes, 6 stacked, icons |
| [Template-Project-Plan](Template-Project-Plan/) | 2 | 74–75 | Blank slide (custom Gantt) |
| [Templates-Table](Templates-Table/) | 4 | 76–79 | Table · Text, 4 columns |
| [Template-Ending](Template-Ending/) | 1 | 80 | 1_End slide |

---

## How to Use These Files

The XML files are **partial slide references** — they reference media, layouts, and themes from the
original PPTX archive. The full extraction in `IBM_pptx_extracted/` contains all required assets:

- `ppt/slides/` — original slide XML files (numbered by global index)
- `ppt/slideLayouts/` — all 49 slide layout definitions
- `ppt/slideMasters/` — the slide master
- `ppt/theme/` — 3 theme files (colors, fonts)
- `ppt/media/` — all images referenced in slides

To reconstruct a slide from this repository, reference the corresponding layout from
`IBM_pptx_extracted/ppt/slideLayouts/` and the theme from `IBM_pptx_extracted/ppt/theme/theme1.xml`.
