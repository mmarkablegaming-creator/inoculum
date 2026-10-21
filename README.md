# Inoculum

An agent-based microbiology simulator that runs entirely in the browser. One HTML file, no build
step, no server, no dependencies, and no network traffic beyond an optional web font.

Open `index.html` locally, or publish this folder with GitHub Pages.

## What it is

A 480 × 320 × 10 µm field of view — about what a 40× objective shows, holding roughly 1.5 nanolitres
— simulated agent by agent against measured biology:

- growth by Monod kinetics and the adder rule of cell size
- temperature and pH by the Rosso cardinal models
- run-and-tumble chemotaxis with temporal, logarithmic sensing
- Hill-type kill curves at published MICs, with pharmacokinetics and the post-antibiotic effect
- phage adsorption rates, latent periods and burst sizes
- viral tropism decided by receptor, with interferon signalling and antigenic drift
- chemistry on a 4 µm grid, solved implicitly so large time steps stay stable

Forty bacteria and archaea, fourteen microbial eukaryotes, seventy-three human cell types, plant
and animal cells, thirty viruses, thirty-eight experiments, and instruments — a spectrophotometer,
broth microdilution, viable counts, plaque assays, replica plating — that measure the culture the
way a bench does rather than reading the answer out of the simulation's internals.

## Publishing it with GitHub Pages

1. Create a repository and copy the contents of this folder into it.
2. `git add . && git commit -m "Inoculum" && git push`
3. In the repository, open **Settings → Pages**, set **Source** to *Deploy from a branch*, choose
   your default branch and the `/ (root)` folder, and save.
4. The site appears at `https://<user>.github.io/<repo>/` within a minute or two.

The page is self-contained, so it works from any path and needs no configuration. `.nojekyll` is
included to stop GitHub preprocessing the repository.

## Browser support

Any current browser. It uses Canvas 2D, `localStorage` for saved cultures and settings, and
`CompressionStream` for save files. Nothing is uploaded; saved cultures live in your own browser.
