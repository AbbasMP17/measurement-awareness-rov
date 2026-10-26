# The Observer Effect in Internet Measurement: A Case Study of Route Origin Validation

Code, data and paper sources for our HotNets '26 paper.

**Abbas Mohsenpour and Cristel Pelsser** (UCLouvain)  
*The 25th ACM Workshop on Hot Topics in Networks (HotNets '26), November 16–17, 2026, Salt Lake City, UT, USA*  
DOI: [10.1145/3847290.3859951](https://doi.org/10.1145/3847290.3859951)

## Summary

Internet observatories publish reports that shape how networks are assessed and perceived. To be transparent and reproducible, they rely on public, long-lived infrastructure that the measured networks can recognize. We study *measurement awareness*: a network treating recognizable measurement targets differently from functionally equivalent targets that are not associated with any measurement.

Using Route Origin Validation (ROV) as a case study, we compare the publicly known RPKI-invalid prefix used by ROV observatories (Is BGP Safe Yet?, APNIC, RoVista, MANRS) with *shadow targets*: equivalent RPKI-invalid prefixes that no observatory publishes. From 12,130 RIPE Atlas probes, we find 15 networks that drop the public target while still reaching the shadow targets, yet receive near-perfect ROV scores from existing observatories.

## Interactive lab

[`lab/index.html`](lab/index.html) is an interactive, animated companion to the paper. It shows two networks, one running ROV with RPKI and one filtering only the Cloudflare test prefix, and how traffic to the public, control and shadow targets reveals the difference.

**Play it online:** https://abbasmp17.github.io/measurement-awareness-rov/lab/ (press "Play the story", or click any target).

- Start the story automatically: https://abbasmp17.github.io/measurement-awareness-rov/lab/#play
- Repeat it in a loop (e.g. on a poster screen): https://abbasmp17.github.io/measurement-awareness-rov/lab/#loop

You can also download `lab/index.html` and open it in any browser. No installation is needed.

## Repository structure

```
.
├── hotnets26/                 Paper sources (LaTeX, bibliography, figures)
│   ├── hotnets26.tex
│   ├── hotnets26.bib
│   ├── hotnets26.pdf          Camera-ready paper
│   ├── figures/               Figures (.drawio sources and exported PDFs)
│   └── Makefile
├── dataset/
│   ├── measurement-ids/       RIPE Atlas measurement IDs used in the paper
│   └── rovista/               Daily snapshots of RoVista's RPKI-invalid test prefixes
├── scripts/
│   ├── rovista.py             Downloads RoVista's test prefixes for one date
│   ├── run.sh                 Runs rovista.py for every day of the study period
│   ├── figure2.py             Plots Figure 2 (RoVista test prefixes over time)
│   └── figure3.py             Plots Figure 3 (reachability of candidate prefixes)
└── lab/
    └── index.html             Interactive lab
```

## Reproducing the results

**RIPE Atlas measurements.** All traceroute measurement IDs are listed in `dataset/measurement-ids/measurement-ids.csv`. The results can be downloaded from the RIPE Atlas API, for example:

```
https://atlas.ripe.net/api/v2/measurements/<measurement_id>/results/
```

**Figure 2.** RoVista snapshots are already in `dataset/rovista/`. To download them again, run:

```bash
cd scripts
./run.sh
python3 figure2.py
```

**Figure 3.**

```bash
cd scripts
python3 figure3.py
```

**Paper.**

```bash
cd hotnets26
make
```

Building the figures from their `.drawio` sources requires the draw.io desktop app; otherwise the existing PDFs are used.

## Citation

```bibtex
@inproceedings{mohsenpour2026observer,
  author    = {Mohsenpour, Abbas and Pelsser, Cristel},
  title     = {The Observer Effect in Internet Measurement: A Case Study of Route Origin Validation},
  booktitle = {Proceedings of the 25th ACM Workshop on Hot Topics in Networks (HotNets '26)},
  year      = {2026},
  publisher = {ACM},
  doi       = {10.1145/3847290.3859951}
}
```

## License

The paper is published under a Creative Commons Attribution 4.0 International (CC BY 4.0) license.
