

# Prior-Aware Bayesian Optimisation of Molecular PES Minima

This repository contains code and Jupyter notebooks implementing a reproducible workflow for Bayesian Optimisation (BO) of molecular potential energy surfaces (PES) using Gaussian Process (GP) surrogates.  
It adapts the BEACON framework from solid-state systems to molecular structure optimisation and includes code for prior-aware optimisation, hyperparameter tracking, and detailed post-analysis.

The repository is **code-only**. All molecule-specific geometries, minima references, and run outputs are expected to be provided locally and are not included here.

---

## Repository Contents

| File | Description |
|------|--------------|
| **best_so_far_plots(symlog)_mean_best_success_curve.ipynb** | Produces Panels A–C (ΔE symlog, ΔE linear, and success rate). Used for comparing BO performance across runs and priors. Requires local minima reference energies for plotting. |
| **BEACON_Script.ipynb** | Baseline BEACON workflow for PES optimisation using Gaussian Processes with configurable priors (No Prior, Lennard-Jones, or MACE). The only molecule-specific inputs are the XYZ geometries and the prior configuration block. |
| **GPvalue_length_scale_FP_distance.ipynb** | Median-run analysis showing three panels: (A) GP value and prior, (B) GP length scale evolution, (C) fingerprint (FP) distance to known minima. Reused across molecules by updating the minima fingerprint file. |
| **BEACON_ndft30_k_schedule_sweep.ipynb** | Parameter sweep notebook testing convergence behaviour at fixed evaluation budgets (e.g. ndft=30). Useful for comparing acquisition or kernel schedules. |
| **plot_linear_HFref_clipHF_MACE.ipynb** | Compares MACE and Hartree–Fock (HF/3-21G) energies along a bond-stretch coordinate (e.g. H–H distance). Demonstrates MACE stability beyond the HF convergence limit. |

---

## Usage

All notebooks are designed for reuse across molecular systems.  
The only molecule-specific inputs are:

1. **Input geometries (.xyz)** – for baseline optimisation runs  
2. **Reference minima (.xyz)** – for post-analysis plotting  
3. **Minima fingerprints (`minima_fps.csv`)** – for FP-distance analysis  

All other logic, parameters, and visualisation routines are molecule-independent.

---

### Typical Workflow

1. **Run BEACON optimisation**  
   Execute the baseline script or notebook (`BEACON_Script.ipynb`) with chosen priors and molecule-specific input structures.  
   Each run produces:
   - `beacon_run.log`  
   - `gp_prior_vs_step.csv`  
   - Optional: `fp_per_run.csv`, `GLOBAL_MIN.info`, or `structures_dft.exact100.xyz`

2. **Analyse results**
   - Use `best_so_far_plots(symlog)_mean_best_success_curve.ipynb` to generate global Panels A–C comparing optimisation performance.
   - Use `GPvalue_length_scale_FP_distance.ipynb` to visualise GP behaviour and FP distances for the median run.

3. **Optional validation**
   - Use `plot_linear_HFref_clipHF_MACE.ipynb` to validate MACE performance against Hartree–Fock for one-dimensional scans.
   - Use `BEACON_ndft30_k_schedule_sweep.ipynb` to assess convergence trends and sensitivity to acquisition settings.

---



