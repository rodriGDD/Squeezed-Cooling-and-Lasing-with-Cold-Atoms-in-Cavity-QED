# Fig. 3: Phases of the squeezed laser

| Panel | Content | Produced by |
|---|---|---|
| (a) | Photon number $n_s$ vs. pump rate $w^{\rm p}$ and gain atoms $N_g$ ($N_c = 3000$), with the phase boundaries | `notebooks/4_phase_diagram_P_Ng.ipynb`, `notebooks/5_cumulants_P_Ng.ipynb` |
| (b) | Rates and output power along the cut $N_g = 400$ | `notebooks/5_cumulants_P_Ng.ipynb`, `notebooks/6_effective_model_cut.ipynb` |
| (c) | Emission linewidth $\Delta\nu$ along the cut $N_g = 400$ | `notebooks/5_cumulants_P_Ng.ipynb`, `notebooks/6_effective_model_cut.ipynb` |
| (d) | Phase diagram vs. cooling atoms $N_c$ and gain atoms $N_g$ | `notebooks/1_phase_diagram_Nc_Ng.ipynb`, `notebooks/2_cumulants_Nc_Ng.ipynb` |
| (e) | $\Delta\hat X$ and $n_s$ vs. $N_c$ and $N_g$ | `notebooks/2_cumulants_Nc_Ng.ipynb`, `notebooks/3_cumulants_Nc_Ng_seeded.ipynb` |

All panels are drawn by `plot_fig3.ipynb` into `figures/panels_abc.svg` and `figures/panels_de.svg`, and combined (and annotated) in Inkscape into `figures/fig3.svg`, exported as `figures/fig3.pdf`.

## How to reproduce

1. Run the Julia notebooks in `notebooks/`. They are independent except that `3_cumulants_Nc_Ng_seeded.ipynb` needs the output of `2_cumulants_Nc_Ng.ipynb`. The phase-diagram notebooks (1, 4) only compute eigenvalues and are fast; the cumulant notebooks (2, 3, 5) are expensive: start Julia with several threads (`julia -t auto`).
2. Run `plot_fig3.ipynb` (Python).

## Data

All arrays are `.npy`, with shapes as saved from Julia (the plotting notebook transposes the maps). Rates and frequencies are angular frequencies, with the frequency in GHz.

### `data/Nc_Ng/` (panels d, e)

Grid: $N_c$ = `logspace(2, log10(2e4))`, $N_g$ = `logspace(1, log10(2e4))`; 1000 points per axis for the mean-field maps, 150 for the cumulant expansion.

| File | Content | Shape |
|---|---|---|
| `mf_unstable_normal.npy` | Number of unstable eigenvalues of the non-lasing solution (full model) | (1000, 1000) |
| `mf_unstable_lasing.npy` | Number of unstable eigenvalues of the lasing solution (effective model) | (1000, 1000) |
| `n.npy` | Photon number of the squeezed mode $n_s$ (NaN at non-stationary points) | (150, 150) |
| `iterations.npy` | Integration windows needed to converge (> 10: non-stationary) | (150, 150) |
| `dX2_seed.npy` | $\Delta\hat X^2$ (normalised to vacuum) of the seeded solution | (150, 150) |
| `cond_qubits.npy` | Excited-state population of the cooling atoms | (150, 150) |
| `cond_r.npy` | Squeezing condition $\tilde\kappa/[\kappa(e^{2r}-1)]$ | (150, 150) |
| `cond_adiab_r.npy`, `cond_adiab_u.npy` | Adiabatic-elimination conditions for levels $r$ and $u$ | (150, 150) |
| `cond_cool.npy` | Cooling condition | (150, 150) |

### `data/P_Ng/` (panels a–c)

Grid: $N_c = 3000$, $N_g$ = `logspace(1, 4)`, $w^{\rm p}$ = `logrange(1e-6, 1.798e-2)`; 1000 points per axis for the mean-field maps, 150 for the cumulant expansion. The effective-model cut is at $N_g = 400$.

| File | Content | Shape |
|---|---|---|
| `P_mf.npy`, `P.npy` | Pump rate $w^{\rm p}$ of the mean-field and cumulant grids | (1000,), (150,) |
| `mf_unstable_normal.npy` | Number of unstable eigenvalues of the non-lasing solution (full model) | (1000, 1000) |
| `mf_cond_chaos.npy` | Stationarity condition of the lasing solution | (1000, 1000) |
| `mf_cond_pump.npy` | $w^{\rm p}$ minus the pump cap (200 kHz) | (1000, 1000) |
| `mf_wmin.npy`, `mf_wmax.npy` | Characteristic pump rates $w_{\min}$, $w_{\max}$ as a function of $N_g$ | (1000,) |
| `n.npy` | Photon number of the squeezed mode $n_s$ | (150, 150) |
| `iterations.npy` | Integration windows needed to converge (> 10: non-stationary) | (150, 150) |
| `linewidth.npy` | Emission linewidth $\Delta\nu$ | (150, 150) |
| `SdagS.npy` | Collective correlation $\langle\hat S^\dagger\hat S\rangle$ of the gain atoms | (150, 150) |
| `pop_gain.npy` | Excited-state population of one gain atom | (150, 150) |
| `purcell.npy` | Purcell rate $\Gamma_p$ of the gain atoms | (1, 150) |
| `cond_qubits.npy` | Excited-state population of the cooling atoms | (150, 150) |
| `cond_adiab_r.npy`, `cond_adiab_u.npy` | Adiabatic-elimination conditions for levels $r$ and $u$ | (150, 150) |
| `eff_n.npy`, `eff_linewidth.npy`, `eff_SdagS.npy`, `eff_pop_gain.npy` | Same quantities from the effective model at $N_g = 400$ | (150, 1) |

The dotted line in panels (a), (d) and (e) is drawn where the more restrictive of `cond_adiab_r` and `cond_adiab_u` reaches 1.
