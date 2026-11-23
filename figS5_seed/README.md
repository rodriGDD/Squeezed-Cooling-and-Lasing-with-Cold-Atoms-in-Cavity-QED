# Fig. S5 — Squeezing spectrum of the seeded system

Squeezing spectrum $S^{\rm sq}_{\hat X}(\nu)$ of the laser with a weak coherent seed ($\Lambda = 10^{-2}$), as a function of the cavity decay $\kappa$, for $N_c = 5000$, $N_g = 300$ and $r = 0.8$.

| Element | Content | Produced by |
|---|---|---|
| Map | $S^{\rm sq}_{\hat X}(\nu)$ vs. $\nu$ and $\kappa$, full model | `notebooks/1_full_model_seeded.ipynb` |
| Black lines | Mode frequencies of the correlation-function equations, effective model | `notebooks/2_effective_model_seeded.ipynb` |
| Dashed line | $\kappa = \tilde\kappa$ | `notebooks/1_full_model_seeded.ipynb` |
| Top panel | Cuts at $\kappa$ = 20, 450, 1500 kHz: full model (dots) and effective model (lines) | both notebooks |

The figure is drawn by `plot_figS5.ipynb` into `figures/panels.svg` and annotated in Inkscape into `figures/figS5.svg`, exported as `figures/figS5.pdf`.

## How to reproduce

1. Run `notebooks/1_full_model_seeded.ipynb` and `notebooks/2_effective_model_seeded.ipynb` (Julia, independent of each other). Start Julia with several threads (`julia -t auto`): the loop over $\kappa$ is parallel.
2. Run `plot_figS5.ipynb` (Python).

All notebooks use paths relative to their own folder.

The spectra are obtained by integrating the two-time correlation functions up to $\tau = 10^6$ with $\Delta\tau = 2$ and Fourier-transforming them, which gives a resolution of 1 kHz over ±250 MHz. Only the plotted window $|\nu| \le 2$ MHz is saved.

## Data

All arrays are `.npy`. Rates and frequencies are angular frequencies in units of 2π·GHz.

| File | Content | Shape |
|---|---|---|
| `kappa.npy` | Cavity decay $\kappa$ | (100,) |
| `freqs.npy` | Frequency $\nu$, $|\nu| \le 2$ MHz | (4001,) |
| `Ssq_full.npy`, `Ssq_eff.npy` | $S^{\rm sq}_{\hat X}(\nu)$ in dB, full / effective model, as a function of $(\kappa, \nu)$ | (100, 4001) |
| `eff_positions.npy` | Imaginary parts of the eigenvalues of the correlation-function equations, effective model | (100, 5) |
| `kappa_ratio.npy` | $|\kappa/\tilde\kappa - 1|$ (the dashed line is its 0.04 contour) | (100,) |

Spectra are stored as $10\log_{10} S$, so negative values mean squeezing.
