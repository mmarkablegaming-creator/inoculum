# Inoculum

An agent-based microbiology simulator that runs entirely in the browser. One HTML file, no build
step, no server, no dependencies, and no network traffic beyond an optional web font.

Open `index.html` locally, or publish this folder with GitHub Pages.

## What it is

A 480 × 320 × 10 µm field of view — about what a 40× objective shows, holding roughly 1.5 nanolitres
— simulated agent by agent against measured biology:

- growth set by ribosome content, after the growth law of Scott et al. (2010): φR = 0.07 + µ/4.2
- the stringent response, so a starved cell stops committing to growth and lag phase is a
  construction project rather than a timer
- chromosome replication by Cooper and Helmstetter (1968), with C and D derived from genome length
  and fork speed, overlapping rounds when the doubling time is shorter than C + D, and initiation at
  Donachie's constant mass per origin — which makes cell size track growth rate as Schaechter,
  Maaløe and Kjeldgaard measured in 1958
- the SOS response, with SulA blocking division so a damaged cell filaments instead
- growth by Monod kinetics and the adder rule of cell size
- temperature and pH by the Rosso cardinal models
- run-and-tumble chemotaxis with temporal, logarithmic sensing
- Hill-type kill curves at published MICs, with pharmacokinetics and the post-antibiotic effect
- phage adsorption rates, latent periods and burst sizes
- viral tropism decided by receptor, with interferon signalling and antigenic drift
- chemistry on a 4 µm grid, solved implicitly so large time steps stay stable

Forty bacteria and archaea, fourteen microbial eukaryotes, seventy-three human cell types, plant
and animal cells, thirty viruses, forty-one experiments, and instruments — a spectrophotometer,
broth microdilution, a checkerboard for drug synergy, a flow cytometer reading per-cell DNA content,
the Luria–Delbrück fluctuation test, viable counts, plaque assays, replica plating — that measure
the culture the way a bench does rather than reading the answer out of the simulation's internals.

## How the biology is checked

Nothing here is asserted. Each claim the simulation makes is turned into a number that could
contradict it, and the test suites run in a headless browser:

| suite | what it checks |
| --- | --- |
| `?physcheck=1` | the growth law, Cooper–Helmstetter against its own closed form, the Schaechter size relation, lag, ppGpp, SOS filamentation, catalase, the cytometer |
| `?biocheck=1` | what each organism needs and what kills it — weak acids and pH, halophily, microaerophily, capnophily, thermophily, radiation, swarming |
| `?cellcheck=1` | plant against animal cells: osmosis, turgor, plasmolysis, photosynthesis, selective toxicity |
| `?toolcheck=1` | the chemicals and tools — detergents and charge, azide, UV dose-response, the proton motive force, the post-antibiotic effect |
| `?assaycheck=1` | the checkerboard against the microdilution panel, and the fluctuation test against a Poisson control |
| `?autotest=1` | every experiment, solved and unsolved, confirming each is winnable and none is winnable by doing nothing |
| `?savetest=<id>` | a full save and restore round-trip, down to the replication forks in progress |

Where a test and the simulation have disagreed, the disagreement was followed to whichever was
wrong. Several entries in the list above began as simulation bugs and several began as bad tests.

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
