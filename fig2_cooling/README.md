# Fig. 2: Squeezing of the cavity field by cooling atoms

| Panel | Content | Produced by |
|---|---|---|
| (a) | Quadrature fluctuations $\Delta\hat X$ vs. $r$ and $N_c$; cuts at $N_c$ = 500, 2000, 10000 | `notebooks/1_full_model_cumulants.ipynb` → `plot_fig2.ipynb` |
| (b) | Wigner functions of the cavity field at $N_c = 6162$ and $r$ = 1, 3, 6, 9 dB | `notebooks/3_wigner_functions.ipynb` |
| (c) | Minimum of the squeezing spectrum vs. $r$ and $N_c$; spectrum at $r \approx 8.7$ dB for $N_c$ = 150, 350, 1200 | `notebooks/1_full_model_cumulants.ipynb`, `notebooks/2_effective_model.ipynb` → `plot_fig2.ipynb` |

The panels are combined (and annotated) in Inkscape into `figures/fig2.svg`, exported as `figures/fig2.pdf`.

## How to reproduce

1. Run `notebooks/1_full_model_cumulants.ipynb` and `notebooks/2_effective_model.ipynb` (Julia, independent of each other). They write the arrays below to `data/`. Start Julia with several threads (`julia -t auto`): the 150 × 150 grid is expensive.
2. Run `notebooks/3_wigner_functions.ipynb` (Julia), which draws panel (b) directly.
3. Run `plot_fig2.ipynb` (Python) to draw panels (a) and (c) into `figures/`.

## Data

All arrays are `.npy`. Maps have shape `(r, N_c)` as saved from Julia (the plotting notebook transposes them).

| File | Content | Shape |
|---|---|---|
| `N_c.npy` | Number of cooling atoms $N_c$ | (150,) |
| `r.npy` | Squeezing parameter $r$ (natural units; in dB: $20\,r/\ln 10$) | (150,) |
| `freqs_MHz.npy` | Frequency $\nu$ of the squeezing spectrum (MHz) | (1000,) |
| `dX_full.npy` | $\Delta\hat X$ (normalised to vacuum), full model | (150, 150) |
| `dX_eff.npy` | $\Delta\hat X$, analytical effective model | (150, 150) |
| `Ssq_min_full.npy`, `Ssq_min_eff.npy` | $-\min_\nu S^{\rm sq}_{\hat X}(\nu)$ in dB, full / effective model | (150, 150) |
| `Ssq_cut_full.npy`, `Ssq_cut_eff.npy` | $-S^{\rm sq}_{\hat X}(\nu)$ in dB at $r \approx 8.7$ dB, as a function of $(N_c, \nu)$ | (150, 1000) |
| `cond_r.npy`, `cond_chi.npy`, `cond_g0.npy` | Validity conditions of the adiabatic eliminations (black dashed lines, drawn where they equal 1) | (150, 150) |

Spectra are stored as $-10\log_{10} S$, so positive values mean squeezing, as in Fig. 2 of the paper.
