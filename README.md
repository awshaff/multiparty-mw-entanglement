# Multiparty Microwave Entanglement Distribution for Quantum Teleportation

Simulation code for my conference paper on how many parties a microwave quantum network can serve before teleportation stops beating the classical limit.

> A. W. Shaffar and H. Shin, "Multiparty Continuous-Variable Microwave Entanglement Distribution for Quantum Teleportation," *2025 Korean Institute of Communications and Information Sciences (KICS) Fall Conference*, pp. 426–427, 2025.

## What this studies

Distributed quantum computing needs entanglement shared among more than two parties. Earlier open-air microwave work focused on two parties. Here I model an **N-party star network**: a central node (Alice) runs N Josephson parametric amplifiers (JPAs) at about 50 mK, each producing a two-mode squeezed thermal state that is sent to one peripheral party over a 5 GHz open-air link.

The model combines:

- **Source noise** that grows with the number of JPAs: `n_cent(N) = n0 + δn (N − 1)`.
- **Channel noise** from air: absorption (µ = 1.44 × 10⁻⁶ m⁻¹) and roughly 1250 thermal photons at ambient temperature.
- **Teleportation fidelity** computed from the covariance-matrix terms of each link. Fidelity above 0.5 means the network beats the classical limit.

All links are assumed to have the same length L for simplicity.

## Main findings (from the paper)

- Fidelity drops by **less than 0.1% per additional party**, even at 400 m.
- With **10 parties at 400 m**, fidelity is about **0.54**, still above the 0.5 classical limit.
- Air thermal noise outweighs the cumulative JPA source noise by roughly **22,700 : 1**, so the network is limited by **distance, not by the number of parties**.
- Sensitivity analysis over a source-noise increment δn of 0.003 to 0.01 keeps the degradation under 0.2% per party in the worst case. Shorter links are more sensitive to source noise.

| Parameter | Value |
|---|---|
| Squeezing r | 1 |
| Baseline source thermal photons n₀ | 0.01 (at ~50 mK) |
| Source noise per extra JPA δn | 0.005 (sensitivity range 0.003–0.01) |
| Air thermal photons N_th | 1250 |
| Atmospheric absorption µ | 1.44 × 10⁻⁶ m⁻¹ |
| Antenna coupling loss η_ant | 0 |
| Link distances | 100 – 400 m |

## Repository contents

| File | What it is |
|---|---|
| `simulation.ipynb` | Main simulation: fidelity versus number of parties and distance |
| `sensitivity_analysis.ipynb` | Sensitivity of the results to the source-noise increment |
| `figure1_fidelity_vs_N.*` | Fidelity versus number of parties N for several distances |
| `figure2_max_N_vs_distance.*` | Maximum number of parties that keeps F > 0.5, versus distance |
| `sensitivity_comparison.*`, `sensitivity_analysis_delta_n.*` | Sensitivity figures |
| `table1_fidelity_vs_N.csv`, `table2_max_N_vs_distance.csv` | Tabulated results |
| `noise_analysis_L200m.dat`, `data/` | Intermediate data |

## Running it

Open the notebooks in Jupyter and run them top to bottom. The required packages are imported at the top of each notebook.

## Scope and limitations

- This is a **theoretical and numerical study**. No hardware experiment was performed.
- Parameters come from published microwave quantum communication experiments and cryogenic noise estimates, not from measurements of my own.
- All links share one length, and source noise is modeled as a linear increase with N.

## Reference

T. Gonzalez-Raya et al., "Open-air microwave entanglement distribution for quantum teleportation," *Phys. Rev. Applied* 18, 044002 (2022).
