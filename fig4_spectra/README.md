# Fig. 4 — Squeezing and emission spectra

Spectra of the squeezed laser with $N_c = 5000$ cooling atoms, $N_g = 300$ gain atoms and $r = 0.8$.

| Panel | Content | Produced by |
|---|---|---|
| (a) | Squeezing spectrum $S^{\rm sq}_{\hat X}(\nu)$ vs. pump rate $w^{\rm p}$ | `notebooks/1_full_model_pump.ipynb` (map), `notebooks/2_effective_model_pump.ipynb` (lines) |
| (b) | Emission spectrum $S(\nu)$ vs. $w^{\rm p}$ | `notebooks/1_full_model_pump.ipynb` (map), `notebooks/2_effective_model_pump.ipynb` (lines) |
| (c) | Linewidths $\Delta\nu$ vs. $w^{\rm p}$ | `notebooks/1_full_model_pump.ipynb` (dots), `notebooks/2_effective_model_pump.ipynb` (lines) |
| (d) | $S^{\rm sq}_{\hat X}(\nu)$ at $\kappa$ = 20, 450, 1500 kHz | `notebooks/3_full_model_kappa.ipynb` (dots), `notebooks/4_effective_model_kappa.ipynb` (lines) |
| (e) | $S^{\rm sq}_{\hat X}(\nu)$ vs. cavity decay $\kappa$ | `notebooks/3_full_model_kappa.ipynb` (map), `notebooks/4_effective_model_kappa.ipynb` (lines) |

All panels are drawn by `plot_fig4.ipynb` into `figures/panels_abc.svg` and `figures/panels_de.svg`, and combined (and annotated) in Inkscape into `figures/fig4.svg`, exported as `figures/fig4.pdf`.

## How to reproduce

1. Run the Julia notebooks in `notebooks/` (independent of each other). Start Julia with several threads (`julia -t auto`): the loops over $w^{\rm p}$ and $\kappa$ are parallel.
2. Run `plot_fig4.ipynb` (Python).

All notebooks use paths relative to their own folder.

## Data

All arrays are `.npy`, with shapes as saved from Julia. Rates and frequencies are angular frequencies in units of 2π·GHz. Spectra are stored as $10\log_{10} S$ in dB, so negative values mean squeezing.

### `data/pump/` — panels (a)–(c)

| File | Content | Shape |
|---|---|---|
| `P.npy` | Pump rate $w^{\rm p}$ | (150,) |
| `freqs.npy` | Frequency $\nu$ | (1000,) |
| `Ssq.npy` | $S^{\rm sq}_{\hat X}(\nu)$ in dB, full model | (150, 1000) |
| `emission.npy` | Emission spectrum $S(\nu)$, full model | (150, 1000) |
| `unstable_normal.npy` | Number of unstable eigenvalues of the non-lasing solution (dashed line: lasing threshold) | (1000, 150) |
| `linewidth.npy` | Decay rates of the linearised mean-field equations, full model | (150, 4) |
| `eff_positions.npy`, `eff_widths.npy` | Positions and widths of the two spectral lines, effective model | (150, 2) |

### `data/kappa/` — panels (d), (e)

| File | Content | Shape |
|---|---|---|
| `kappa.npy` | Cavity decay $\kappa$ | (100,) |
| `freqs.npy` | Frequency $\nu$ | (2000,) |
| `Ssq_full.npy`, `Ssq_eff.npy` | $S^{\rm sq}_{\hat X}(\nu)$ in dB, full / effective model | (100, 2000) |
| `eff_positions.npy` | Positions of the two spectral lines, effective model | (100, 2) |
| `kappa_ratio.npy` | $|\kappa/\tilde\kappa - 1|$ (the dashed line $\kappa = \tilde\kappa$ is its 0.04 contour) | (100, 2000) |
