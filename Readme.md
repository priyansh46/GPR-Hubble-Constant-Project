# Gaussian Process Regression on Cosmic Chronometer Data
### Reconstructing H(z) and Inferring the Hubble Constant H₀

A  project that applies 
Gaussian Process Regression (GPR) — a non-parametric 
Bayesian machine learning method — to reconstruct the 
Hubble parameter H(z) directly from observational data, 
without assuming any cosmological model.

---

##  Background

The **Hubble constant H₀** describes the current expansion 
rate of the Universe. Its value is under active debate — 
a tension exists between:
- **Planck 2018** (CMB): H₀ = 67.4 ± 0.5 km/s/Mpc
- **SH0ES 2022** (Supernovae): H₀ = 73.04 ± 1.04 km/s/Mpc

This ~4σ discrepancy is one of the biggest open problems 
in modern cosmology. This project uses **Cosmic Chronometers 
(CC)** — passive, red-envelope galaxies — as model-independent 
H(z) probes to reconstruct H(z) and infer H₀ using GPR.

---

##  Methodolgy

### 1. Dataset
- 31 Cosmic Chronometer H(z) measurements
- Redshift range: z = 0.07 to 1.965
- Source: Magana et al. 2018 (arXiv:1802.01505)

### 2. Gaussian Process Regression
GPR treats the unknown function H(z) as a **random process** 
defined by:
- A **mean function** (prior belief about H(z))
- A **covariance kernel** (smoothness/correlation structure)

We compare **6 GPR models** in total:

| Mean Function | Kernel | Model |
|---|---|---|
| Zero mean | RBF | Model 1 |
| Zero mean | Matérn (ν=2.5) | Model 2 |
| Zero mean | Rational Quadratic | Model 3 |
| ΛCDM mean | RBF | Model 4 |
| ΛCDM mean | Matérn (ν=2.5) | Model 5 |
| ΛCDM mean | Rational Quadratic | Model 6 |

### 3. Kernel Comparison
Three covariance kernels are tested:
- **RBF (Squared Exponential):** Infinitely smooth
- **Matérn (ν=2.5):** Physically realistic roughness
- **Rational Quadratic:** Scale-mixture of RBFs

### 4. Bayesian Model Comparison
Models are ranked using:
- **Log Marginal Likelihood (LML)** — fit quality
- **AIC** (Akaike Information Criterion)
- **BIC** (Bayesian Information Criterion)

### 5. H₀ Inference
H₀ is extracted by evaluating the GPR reconstruction 
at z → 0, then computing the **Hubble tension** in 
units of σ with respect to both Planck and SH0ES values.

---

##  File

| File | Description |
|------|-------------|
| `Data_Science_Project.ipynb` | Full implementation notebook |

---

##  Libraries Used

| Library | Purpose |
|---|---|
| `numpy` | Numerical computation |
| `matplotlib` | Plotting and visualization |
| `scikit-learn` | Gaussian Process Regressor |
| `scipy` | Root finding for H₀ inference |

---


---

##  Key Results

- ΛCDM mean GPR achieves **higher LML** than zero mean GPR
  → Prior cosmological knowledge improves reconstruction
- All 3 kernels give **consistent results** 
  → Reconstruction is kernel-robust
- Inferred H₀ lies **between Planck and SH0ES** values
  → CC data alone cannot resolve the Hubble tension
- Tension with Planck: ~1σ | Tension with SH0ES: ~2σ

---

## Figures Generated

| Figure | Description |
|---|---|
| Figure 1 | EDA — CC data points + ΛCDM reference + H(z) distribution |
| Figure 2 | GPR reconstruction with Zero mean (3 kernels) |
| Figure 3 | GPR reconstruction with ΛCDM mean (3 kernels) |
| Figure 4 | Side-by-side mean function comparison |

---

