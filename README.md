# fisheries-data-repo

Fisheries' **management areas**: FAO's fishing areas and the regional fishery bodies', the U.S. councils' and regions', ICES's and Canada's: a data repository of the oceansensing ocean map system, with its own
Pages site, its own schedule and its own gigabyte, and no code of its own.

**Publishing since 2026-11-20**, daily. `PLAN.md` is the founding plan; `CLAUDE.md` carries what must not be
got wrong and the shared doc doctrine.

## What it publishes

Fifteen products, each a root of every record (`<product>.json`: its shape as GeoJSON and what its source says of it) and the same records as a pyramid of Mapbox vector tiles beside it (uncompressed, extent 4096, Web Mercator, the XYZ scheme; `land/<product>/index.json` naming the version, the tiles' own hash, and every tile to zoom 8), R2's alone: **`fao-areas`**, zooms 0 to 6, FAO's Major Fishing Areas for Statistical Purposes from the 19 major areas to their subunits, each with its code, level, names and status; **`fishery-bodies`**, zooms 0 to 6, the regional fishery bodies' areas of competence, each body whose FAO record licenses it CC BY 4.0, with that body's citation; **`council-regions`**, zooms 1 to 8, the eight U.S. Regional Fishery Management Councils' regions; **`groundfish-areas`**, zooms 4 to 11, NOAA Fisheries West Coast Region's groundfish conservation areas with their whole schema (group, constancy, seasonal and effective dates, status, FMP, the Federal Register citation and link, the CFR's, the boundary's last update); **`garfo-areas`**, zooms 7 to 9, NOAA Fisheries Greater Atlantic Regional Fisheries Office's regulated areas merged from its services, each with its group, its recurring season, its CFR paragraph and its Federal Register citation, the reference lines as lines; **`statistical-areas`**, zooms 3 to 8, the Greater Atlantic Region's statistical areas; **`hapc`**, **`efh-closed-areas`** and **`fishing-restrictions`**, zooms 3 to 10, NOAA Fisheries' habitat areas of particular concern, its essential fish habitat areas protected from fishing, and its Office of Habitat Conservation's compilation of the areas where bottom-tending gear or trawling is prohibited; **`coral-protection`**, zooms 4 to 11, the deep-sea coral protection areas of 50 CFR 648.372; **`ices-areas`**, zooms 2 to 7, and **`ices-rectangles`**, zooms 4 to 7, ICES's areas and its statistical rectangles; **`dfo-areas`**, zooms 3 to 9, Atlantic and Arctic Canada's fisheries management areas, species by species; **`nafo-divisions`**, zooms 2 to 7; and **`marine-refuges`**, zooms 4 to 10, Canada's marine refuges and other effective area-based conservation measures with their prohibitions. Every root says, in its publisher's words, what its GIS is not, and in a sentence of its own that emergency and in-season closures are never in it. A set's version is its tiles' own hash, so an unchanged rebuild publishes nothing new.

These products are published **operationally but not drawn on the
website's map**. R2 alone carries them, so this repository's Pages status names none of
them: the map's status line and the site's watchdog see only whether the
origin publishes. Their fates are in the status on R2 and on the
`published` branch.

## Where the data comes from

Each source is read from its publisher's own service. **FAO** (`www.fao.org/fishery/geoserver`): the Major Fishing Areas (`FAO_AREAS_ERASE`) and the regional fishery bodies' areas of competence (`RFB_COMP_CLIP`), CC BY 4.0 under each dataset's mandatory citation — *"FAO. 2024. FAO Major Fishing Areas for Statistical Purposes. In: FAO Fisheries and Aquaculture Division [online]"*, and for each body *"© FAO, 2025. FAO Regional Fishery Bodies. Geographic Area of Competence of …"*, read from each record on every read; a body whose record does not say CC BY 4.0 is left out. FAO's disclaimer: *"The designations employed and the presentation of material in the map(s) are for illustration only and do not imply the expression of any opinion whatsoever on the part of FAO concerning the legal or constitutional status of any country, territory or sea area or concerning the delimitation of frontiers or boundaries."* **NOAA Fisheries** (`services2.arcgis.com`, `maps.fisheries.noaa.gov`): the councils' regions, the Greater Atlantic Region's regulated and statistical areas, the habitat areas of particular concern, the essential fish habitat areas protected from fishing and the Office of Habitat Conservation's compilation of bottom-gear and trawl restrictions (the layer behind its story map *Deep-Sea Coral Protection in U.S. Waters*) — U.S. Government works — and the West Coast Region's groundfish conservation areas, CC0 1.0. GARFO: *"This Geographic Information System (GIS) dataset is not the legal definition of the Regulated Area. The description published in the U.S. Code of Federal Regulations is the only legal definition."* The West Coast Region: *"These spatial data are considered to be approximate representations and are NOT an OFFICIAL record for the exact regulated area boundaries."* **NOAA's Office for Coastal Management**, MarineCadastre.gov's *Coral Protection Areas* (`coast.noaa.gov`), under its 17 U.S.C. 403 notice. **ICES** (`gis.ices.dk`), its areas and statistical rectangles, CC BY 4.0, credit ICES. **Fisheries and Oceans Canada** (`egisp.dfo-mpo.gc.ca`), its Atlantic and Arctic fisheries management areas, NAFO subareas and divisions and other effective area-based conservation measures: *"Contains information licensed under the Open Government Licence – Canada."* None of it is the regulation it maps, and none of it says whether an area is open or closed today. Terms read 2026-11-20.

## How it runs

The orchestrator (the site's private `pipeline/`), the fetchers and the
published-file contract all come from `oceansensing.github.io`, checked out at
run time. This repository carries `pipeline/products.toml` and its publish
workflow, and nothing else executable. Each run publishes to GitHub Pages and
to Cloudflare R2 from one build. Related repositories: `maritime-data-repo` (its machinery, the same pyramids), `public-lands-data-repo` (polygons and lines on the same machinery).

**Which document gets what, and what "update docs" means across every
repository of this project, is the doctrine block at the top of `CLAUDE.md`**: the
same text in each, held equal by the site's `check:docs`.

## Structure

```
README.md       what this is
CLAUDE.md       what must not be got wrong, and the shared doc doctrine
PLAN.md         the founding plan and running record
DECISIONS.md    dated one-way decisions, D1 onward
pipeline/       products.toml, the declaration the orchestrator reads
.github/        the publish workflow
```
