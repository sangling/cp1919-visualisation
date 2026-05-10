# CP1919 Visualisation

This repository contains files for reproducing the ridgeline plot of pulsar CP 1919 – the data behind the cover of Joy Division's *Unknown Pleasures* – using tools in the Microsoft ecosystem.

It accompanies a series of posts on [simonangling.com](https://simonangling.com) exploring how the same dataset can be visualised using different tools, starting with Excel and working up through the Microsoft and Azure stack.

## Background

The image on the cover of *Unknown Pleasures* (Factory Records, 1979) is a stacked plot of 80 radio pulses from PSR B1919+21, a rotating neutron star first observed by Jocelyn Bell Burnell in 1967. The plot was originally produced by Harold D. Craft Jr. as part of his doctoral dissertation at Cornell University in 1970, using data from the Arecibo Observatory.

The dataset used here is the same data, preserved and made available by [pachadotdev](https://github.com/pachadotdev/cp1919) under a CC0 licence.

## Contents

| File | Description |
|------|-------------|
| `cp1919.csv` | The raw dataset – 24,000 rows, three columns (x, y, z) representing 80 pulses of 300 amplitude samples each (from [pachadotdev](https://github.com/pachadotdev/cp1919) under a CC0 licence) |
| `cp1919-visualisation.xlsx` | Excel workbook containing the pivoted data, offset table, and ridgeline chart |

## The Excel workbook

The workbook contains three sheets:

- **cp1919** – the raw data pivoted from long to wide format using Power Query, giving 300 rows × 80 pulse columns
- **offsets** – a derived table that adds a vertical offset to each pulse column so the 80 series stack cleanly when charted; the offset step value in cell A2 can be tuned to adjust the vertical spacing
- **chart** – the resulting line chart formatted with a black background

A full walkthrough of how the workbook was built is available in the accompanying blog post: [PLACEHOLDER – link to post]

## Limitations

Excel can produce a recognisable approximation of the ridgeline plot, but it has two significant limitations compared to tools like R:

- **No masking.** The `geom_ridgeline` function in R automatically whites out the area below each curve so that overlapping lines from adjacent pulses don't bleed through. Excel has no equivalent, so lines from adjacent pulses cross and tangle where the signal amplitude is high.
- **Manual line colouring.** Excel assigns each of the 80 series its own colour from the default palette. Recolouring all 80 series to white requires either manually formatting each series or writing a short VBA macro.

## For R

If you want to reproduce the image properly, the pachadotdev repository includes R code using `ggplot2` and `ggridges` that produces a clean, print-quality result in a few lines:

[https://github.com/pachadotdev/cp1919](https://github.com/pachadotdev/cp1919)

## Licence

The `cp1919.csv` dataset is reproduced under the CC0 licence from the pachadotdev repository. The Excel workbook and any other original files in this repository are released under [MIT licence](LICENSE).

## Related

- [simonangling.com](https://simonangling.com) – the blog series this repository accompanies
- [jonzed.com](https://jonzed.com) – where the t-shirt ended up
- [pachadotdev/cp1919](https://github.com/pachadotdev/cp1919) – the original R code and dataset
