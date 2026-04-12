# Five Experiments on Convergence, Thermodynamic Anchoring, and the Geometry of Receiver-Limited Throughput

Grant Lavell Whitmer III

The Windstorm Institute, Fort Ann, NY 12827, USA

Email: grantwhitmer3@gmail.com

ORCID: 0009-0007-3224-755X

---

## Abstract

This study presents five reproducible experiments investigating whether serial decoding systems converge to a finite information parameter. Zero-free-parameter prediction: the M-ary rate-distortion formula predicts ribosome throughput to 0.0004 bits residual, outperforming a naive log_2(M) null model in 2 of 4 testable systems. Basin significance: bio-plausible (M, epsilon) sampling places 90.5% of samples in the 3--6 bit band versus 28.3% for random sampling (p ~ 0). Evolutionary convergence: gradient ascent on cost-constrained utility independently discovers K* ~ 23 for the molecular substrate. Asymptotic convergence: the running mean across 21 systems converges to 4.16 +/- 0.19 bits (95% CI). Thermodynamic anchoring: using four independently measured physical parameters, the Hopfield-Pineros-Tlusty model predicts I_eff = 4.387 bits against the observed 4.390, residual 0.003 bits, anchoring the basin to kT and generating a falsifiable prediction: cooling a ribosome to 280 K should raise per-event information to approximately 4.86 bits.

**Keywords:** convergent evidence; thermodynamic anchor; kinetic proofreading; asymptotic convergence; zero-parameter prediction; Monte Carlo basin

---

## 1. Introduction

In companion papers [1,2], we established that the M-ary rate-distortion function R_M(epsilon) provides a mechanistic floor for serial decoding throughput and that observed systems cluster in a 3--6 bit basin decomposable into floor plus substrate slack plus residual. These papers raise a natural question: does the aggregate behavior converge to a well-defined parameter?

This paper presents five experiments designed to answer that question from five independent angles, forming a convergent evidence chain. Each experiment includes a formal hypothesis, an explicit control group, a quantified result, and a Python implementation for independent replication. The experimental design prioritizes falsifiability: each experiment is constructed so that a negative result would weaken or invalidate the framework.

**Definition.** The Serial Decoding Basin parameter tau is defined as: tau = lim_{n->infinity} (1/n) * sum(I_eff,i), where I_eff,i is the receiver-resolved information per event for the i-th independently characterized serial decoding system. The parameter tau is the centroid of a geometric constraint -- the rate-distortion surface R_M(epsilon) evaluated at parameter ranges observed in biological serial decoders -- not a fundamental constant like c or h-bar.

## 2. Material and Methods

### 2.1. Experiment 1: Zero-Free-Parameter Predictions

For systems where alphabet size M and error rate epsilon are measured independently of I_eff, the formula R_M(epsilon) = log_2(M) - H_b(epsilon) - epsilon * log_2(M - 1) was applied to predict throughput. The null hypothesis is that I_eff scales only with log_2(M), ignoring epsilon. Four systems were tested: ribosome (M = 21, epsilon = 10^-4), phonology (M = 31, epsilon = 0.02), chromatic scale (M = 12, epsilon = 0.05), and neural working memory (M = 7, epsilon = 0.12).

### 2.2. Experiment 2: Monte Carlo Basin Significance

N = 40,000 samples were drawn from each of two distributions. Bio-plausible: M uniform in [4, 64], epsilon log-uniform in [10^-4, 0.1]. Control: M uniform in [2, 300], epsilon log-uniform in [10^-5, 0.5]. Basin membership was recorded as 1 if R_M(epsilon) falls in [3, 6] bits, 0 otherwise. Significance was assessed via binomial test.

### 2.3. Experiment 3: Evolutionary Phase Portrait

Gradient ascent was performed on the utility function U(K) = log_2(K) - gamma * K^alpha with substrate-specific cost parameters: molecular (alpha = 1.50, gamma = 0.0085), neural (alpha = 1.76, gamma = 0.0190), acoustic (alpha = 1.35, gamma = 0.0042), and digital (alpha = 1.20, gamma = 0.0011). These values are estimates, not independently measured constants. Twenty random starts per substrate were used to verify convergence independence. The control was a random fitness landscape U_random(K) = noise.

### 2.4. Experiment 4: Asymptotic Convergence

The running mean tau_n and 95% bootstrap confidence interval were computed using 21 systems from the cross-substrate survey [2], entered in order of measurement precision (Tier 1 first). The control was random I_eff values sampled uniformly from [0, 8] bits.

### 2.5. Experiment 5: Thermodynamic Anchor to kT

Ribosome throughput was predicted from four independently measured physical parameters via the Hopfield-Pineros-Tlusty kinetic proofreading model [3,4]:

I_eff = eta * n_c * Delta_G / (R * T * ln(2))                               (1)

**Table 1.** Physical parameters for thermodynamic prediction.

| Parameter | Symbol | Value | Source |
|-----------|--------|-------|--------|
| Proofreading efficiency | eta | 0.223 | Pineros and Tlusty (2020), TUR measurement |
| Discrimination contacts | n_c | 3 | tRNA biology, X-ray crystallography |
| Free energy per contact | Delta_G | 2.8 kcal/mol | Isothermal calorimetry |
| Temperature | T | 310 K | Physiological standard |

All four parameters are measured independently of I_eff. The falsification criterion is that varying T or Delta_G should produce physically predictable changes in I_eff if the thermodynamic relationship is genuine.

## 3. Results

### 3.1. Experiment 1: Zero-Free-Parameter Predictions

**Table 2.** Rate-distortion predictions versus null model.

| System | Tier | M | epsilon | R_M(epsilon) | Observed | Residual (model) | log_2(M) | Residual (null) | Winner |
|--------|------|---|---------|-------------|----------|-----------------|----------|-----------------|--------|
| Ribosome | MI | 21 | 10^-4 | 4.390 | 4.390 | +0.000 | 4.392 | +0.002 | R_M |
| Phonology | MI | 31 | 0.02 | 4.715 | 4.200 | +0.515 | 4.954 | +0.754 | R_M |
| Chromatic | SS | 12 | 0.05 | 3.126 | 3.580 | -0.454 | 3.585 | -0.005 | Null |
| Neural WM | SS | 7 | 0.12 | 1.968 | 3.120 | -1.152 | 2.807 | -0.313 | Null |

R_M(epsilon) outperforms the null in 2 of 4 testable systems. The informative tests are phonology (R_M wins by 0.24 bits) and neural working memory (null wins by 0.84 bits). The neural working memory failure likely reflects that Miller's 7 +/- 2 items involve parallel chunk comparison rather than pure serial discrimination -- a scope violation of the framework.

### 3.2. Experiment 2: Monte Carlo Basin Significance

Bio-plausible sampling: 90.5% in [3, 6] bits (mean I_eff = 4.49). Random control: 28.3% (mean I_eff = 3.12). Binomial test: p < 10^-300. The 3--6 bit basin is a real attractor of the bio-plausible parameter region. However, this demonstrates geometric consequence of biological parameter ranges, not necessarily that biology "chose" these parameters because of the basin.

### 3.3. Experiment 3: Evolutionary Phase Portrait

**Table 3.** Evolutionary simulation results across substrates.

| Substrate | K* (theory) | K* (sim, 20 runs) | I* (bits) | Observed I_eff | Delta_I |
|-----------|-------------|-------------------|-----------|----------------|---------|
| Molecular | 23.4 | 23.4 +/- 0.01 | 3.59 | 4.39 | -0.80 |
| Acoustic | 60.5 | 60.5 +/- 0.01 | 4.85 | 4.95 | -0.10 |
| Neural | 8.5 | 8.5 +/- 0.00 | 2.27 | 3.12 | -0.85 |
| Digital | 340.5 | 340.5 +/- 0.02 | 7.21 | 4.46 | +2.75 |

The molecular fixed point K* ~ 23 is within 2 of the ribosome's M = 21. The acoustic substrate shows near-zero prediction error (Delta_I = -0.10). The co-evolutionary result from the companion paper [2] is the strongest: K = 19.76 and epsilon = 6.62 x 10^-3, independently rediscovering the ribosome's neighborhood.

### 3.4. Experiment 4: Asymptotic Convergence

**Table 4.** Running mean convergence.

| n | tau_n | 95% CI | CI width |
|---|-------|--------|----------|
| 5 | 4.140 | [3.676, 4.608] | 0.932 |
| 10 | 4.191 | [3.878, 4.568] | 0.690 |
| 15 | 4.157 | [3.908, 4.408] | 0.500 |
| 21 | 4.157 | [3.970, 4.350] | 0.380 |

tau_21 = 4.157 bits. The CI width shrinks from 0.93 at n = 5 to 0.38 at n = 21, consistent with sqrt(n) convergence. Tier 1 only (n = 7): tau_7 = 4.24 bits, 95% CI [4.00, 4.48].

### 3.5. Experiment 5: Thermodynamic Anchor

I_pred = 0.223 * 3 * 2.8 / (1.987 x 10^-3 * 310 * ln(2)) = **4.387 bits**

**Table 5.** Thermodynamic prediction summary.

| Quantity | Value |
|----------|-------|
| I_max (no proofreading, eta = 1) | 19.67 bits |
| I_pred (eta = 0.223) | 4.387 bits |
| I_obs (rate-distortion) | 4.390 bits |
| Residual | 0.003 bits |

**Table 6.** Sensitivity of thermodynamic prediction to eta.

| eta | I_pred | Residual from observed |
|-----|--------|----------------------|
| 0.200 | 3.935 | -0.455 |
| 0.210 | 4.131 | -0.259 |
| 0.220 | 4.328 | -0.062 |
| 0.223 | 4.387 | -0.003 |
| 0.230 | 4.525 | +0.135 |
| 0.250 | 4.919 | +0.529 |

The prediction is sensitive to eta: a +/- 5% shift in eta produces a +/- 0.5 bit shift in I_pred. The residual of 0.003 bits depends on eta being correct to approximately 1%.

**Falsifiable wet-lab prediction:** At T = 280 K, I_eff = 4.857 bits (+0.47 from 310 K). At T = 340 K, I_eff = 3.996 bits (-0.39 from 310 K). Temperature coefficient: dI_eff/dT ~ -0.014 bits/K. This is testable by measuring ribosomal translation fidelity at controlled temperatures.

## 4. Discussion

### 4.1. The Convergent Evidence Chain

Each experiment alone is suggestive. Together, they constitute a coherent case:

**Table 7.** Summary of convergent evidence.

| Experiment | Question | Key Result | Falsified? |
|-----------|----------|-----------|-----------|
| Zero-parameter | Does R_M predict? | Ribosome residual = 0.0004 | No |
| Monte Carlo | Is the basin real? | 90.5% vs 28.3%, p ~ 0 | No |
| Evolution | Does optimization find M ~ 21? | K* = 23.4 | No |
| Convergence | Does tau_n converge? | tau_21 = 4.16, CI shrinking | No |
| Thermodynamic | Is tau anchored to kT? | Residual = 0.003 | No (pending eta revision) |

### 4.2. What the Chain Does Not Prove

The evidence does not prove that tau is a universal constant (between-domain variation is real; Kruskal-Wallis p = 0.016), that biology "chose" the basin versus merely inhabiting it, that eta = 0.223 is correct to the precision needed, or that n = 21 systems is sufficient for reliable convergence. The tau parameter is best interpreted as the centroid of a geometric constraint rather than a fundamental physical constant.

### 4.3. Ribosomal Efficiency in Context

The ribosome operates within 2.7% of its theoretical thermodynamic minimum (phi_useful = 1.027). For comparison, the best human-engineered heat engines achieve 40--60% of Carnot efficiency, and the best solar cells reach 47% of the Shockley-Queisser limit. Evolution is a better optimizer than human engineering -- at least for the serial decoding problem. This efficiency has implications for synthetic biology: any attempt to expand the genetic code beyond 21 amino acids must contend with the ribosome's near-optimal thermodynamic operating point [5].

### 4.4. Toward a Formal Asymptotic Framework

The function R_M(epsilon) is continuous and bounded on the compact bio-plausible domain D = {(M, epsilon) : M in [4, 64], epsilon in [10^-4, 0.1]}. By the strong law of large numbers, for any probability measure mu on D, tau = E_{(M,epsilon)~mu}[R_M(epsilon)] exists and is finite. The empirical estimate tau_21 = 4.16 is a sample mean converging to this expectation.

### 4.5. Priority Measurements

Every new Tier 1 confusion-matrix measurement narrows the confidence interval on tau. The highest-priority targets include: olfactory receptor confusion matrices (new Tier 1 domain), sign language phonological feature mutual information (new Tier 1 domain), insect pheromone channel capacity (cross-phylum test), synthetic cells with expanded genetic codes (direct test of the M prediction), and quantum biological systems such as photosynthetic exciton transfer (Holevo bound comparison).

### 4.6. Limitations

1. The ribosome prediction at low epsilon is near-tautological (R_M approaches log_2(M) as epsilon approaches 0).
2. The cost parameters (alpha, gamma) in Experiment 3 are estimates, not independently measured constants.
3. The thermodynamic anchor (Experiment 5) depends on eta = 0.223 being correct to approximately 1%.
4. With only 21 systems (7 at Tier 1), the confidence interval on tau remains wide (0.38 bits).
5. The temperature prediction (Experiment 5) has not yet been tested in a wet-lab setting.

---

## Ethics Statement

This work did not require ethical approval.

## Data Accessibility

All data, Python implementations for all five experiments, analysis scripts, and raw results are publicly available at https://github.com/Windstorm-Labs/serial-decoding-basin (DOI: 10.5281/zenodo.19323423).

## Declaration of AI Use

Claude (Anthropic) was used as an AI research tool for mathematical derivations, data analysis, and manuscript drafting assistance. All results were verified independently by the author.

## Authors' Contributions

G.L.W.: Conceptualization, Methodology, Software, Validation, Formal Analysis, Investigation, Resources, Data Curation, Writing -- Original Draft, Writing -- Review and Editing, Visualization, Supervision, Project Administration.

## Conflict of Interest Declaration

The author declares no competing interests.

## Funding

This research received no external funding. All work was self-funded by the author.

## Acknowledgements

This paper was developed through adversarial review by six frontier AI models. Mathematical derivations, experimental design, and data analysis were performed with the assistance of Claude (Anthropic), an AI research tool. The tau formalization was catalyzed by Claude's review and experimental suite.

## References

[1] Whitmer GL III. The Receiver-Limited Floor: Rate-Distortion Bounds on Serial Decoding Throughput. Zenodo. 2026. DOI: 10.5281/zenodo.19322973

[2] Whitmer GL III. The Throughput Basin: Cross-Substrate Convergence and Decomposition of Serial Decoding Throughput. Zenodo. 2026. DOI: 10.5281/zenodo.19323194

[3] Hopfield JJ. Kinetic proofreading: a new mechanism for reducing errors in biosynthetic processes requiring high specificity. Proc Natl Acad Sci USA. 1974;71:4135-4139. DOI: 10.1073/pnas.71.10.4135

[4] Pineros WD, Tlusty T. Kinetic proofreading and the limits of thermodynamic discrimination. Phys Rev Lett. 2020;125:228101. DOI: 10.1103/PhysRevLett.125.228101

[5] Zaher HS, Green R. Quality control by the ribosome following peptide bond formation. Nature. 2009;457:161-166. DOI: 10.1038/nature07582

[6] Shannon CE. A mathematical theory of communication. Bell Syst Tech J. 1948;27:379-423. DOI: 10.1002/j.1538-7305.1948.tb01338.x

[7] Miller GA. The magical number seven, plus or minus two: some limits on our capacity for processing information. Psychol Rev. 1956;63:81-97. DOI: 10.1037/h0043158

[8] Tlusty T. Rate-distortion scenario for the emergence and evolution of noisy molecular codes. Phys Rev Lett. 2008;100:048101. DOI: 10.1103/PhysRevLett.100.048101

[9] Whitmer GL III. The Fons Constraint: Information-Theoretic Convergence on Encoding Depth in Self-Replicating Systems. Zenodo. 2026. DOI: 10.5281/zenodo.19274048

[10] Whitmer GL III. Serial Decoding Basin: Experiment Code and Data. GitHub. 2026. Available from: https://github.com/Windstorm-Labs/serial-decoding-basin
