[![DOI](https://zenodo.org/badge/1468941896.svg)](https://doi.org/10.5281/zenodo.24473853)

# Squeezed Cooling and Lasing — code and data

This repository contains the code and data required to reproduce the figures of the paper [Squeezed Cooling and Lasing with Cold Atoms in Cavity-QED](https://arxiv.org/abs/2611.24743) (arXiv:2611.24743). The code and data are archived on Zenodo: [doi:10.5281/zenodo.24473853](https://doi.org/10.5281/zenodo.24473853).

The simulations are Julia notebooks (cumulant expansions with [QuantumCumulants.jl](https://github.com/qojulia/QuantumCumulants.jl), exact steady states with [QuantumToolbox.jl](https://github.com/qutip/QuantumToolbox.jl)) and the figures are drawn with Python (matplotlib).

<p align="center">
  <img src="fig1_scheme/fig1.png" width="900" alt="Fig. 1"><br>
  <em>Fig. 1 — (a) Atoms in a two-mode cavity (decay rates κ and κ<sub>b</sub>) driven by Raman drives (Ω<sub>r</sub>, Ω<sub>s</sub>), a cooling drive (Ω<sub>b</sub>) and repumping drives. (b) Level scheme for squeezed cooling of the cavity field. (c) Level scheme for squeezed lasing, with incoherent pumping w<sup>p</sup>. The insets show the Wigner function of the cavity field in each case.</em>
</p>

## How to use

Clone the repository (`git clone`) or download the archived version from [Zenodo](https://doi.org/10.5281/zenodo.24473853).

**Julia** (1.11). The environment is pinned in `Project.toml` / `Manifest.toml`. From the repository root:

```bash
julia --project=. -e 'using Pkg; Pkg.instantiate()'
```

Run the notebooks with this environment and several threads, e.g. register a Jupyter kernel (requires [IJulia](https://github.com/JuliaLang/IJulia.jl)):

```bash
julia -e 'using IJulia; installkernel("Julia (squeezed laser)", "--project=$(pwd())", "--threads=auto")'
```

**Python** (3.11). The packages used by the plotting notebooks are pinned in `requirements.txt`:

```bash
pip install -r requirements.txt
```

The folders of Figs. 2–4 and S5 have the same layout:

* `notebooks/` — Julia simulations, numbered in the order they should be run; they write to `data/`.
* `data/` — the arrays used for the figure (`.npy`).
* `plot_figX.ipynb` — draws the panels from `data/` into `figures/`.
* `figures/` — the panels and the final figure (assembled in Inkscape).
* `README.md` — which notebook produces each panel, and the content of every data file.

The saved data are included, so the figures can be redrawn without running the simulations.

## Contents

| Folder | Figure |
|---|---|
| `fig1_scheme/` | Fig. 1 — scheme of the system and level schemes for squeezed cooling and squeezed lasing (drawing only: `fig1.svg`, `fig1.pdf`). |
| `fig2_cooling/` | Fig. 2 — squeezing of the cavity field by the cooling atoms: quadrature fluctuations, Wigner functions and squeezing spectrum. |
| `fig3_lasing/` | Fig. 3 — phases of the squeezed laser as a function of pump rate and atom numbers: photon number, rates, linewidth and squeezing. |
| `fig4_spectra/` | Fig. 4 — squeezing and emission spectra as a function of pump rate and cavity decay. |
| `figS5_seed/` | Fig. S5 — squeezing spectrum of the laser with a coherent seed as a function of cavity decay. |

## Contact

Rodrigo Grande de Diego — rodrigo.grande@iff.csic.es

## How to cite this code

If you use this code or data, please cite the paper ([arXiv:2611.24743](https://arxiv.org/abs/2611.24743)) and this repository:

```bibtex
@software{GrandeDeDiego2026code,
  author    = {Grande de Diego, Rodrigo and S{\'a}nchez Mu{\~n}oz, Carlos},
  title     = {Code and data for "Squeezed Cooling and Lasing with Cold Atoms in Cavity-QED"},
  year      = {2026},
  publisher = {Zenodo},
  doi       = {10.5281/zenodo.24473853},
  url       = {https://doi.org/10.5281/zenodo.24473853}
}
```
