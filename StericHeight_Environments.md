# ECCO Version 4 Python Tutorial — Environments to run Steric Height Calculation


**Yuanyuan Song · MIT**

---

## 1. Get the tutorial

On your personal computer:

```bash
git clone https://github.com/ECCO-GROUP/ECCO-v4-Python-Tutorial.git
cd ECCO-v4-Python-Tutorial/Intro_to_PO_Tutorials/
```

Two relevant notebooks live in this folder:

- `Steric_height.ipynb` — Part 3a: computing steric height anomaly
- `Steric_SSH_OBP.ipynb` — Part 3b: computing steric height from SSH and OBP

---

## 2. Python requirements

**Python ≥ 3.11.** Recommended: create a `conda` environment containing the packages below (versions pinned to the ones used in this tutorial).

| Package | Version |
| --- | --- |
| **numpy** | 2.4.5 |
| **ecco_v4_py** | 1.8.1 |
| **ecco_access** | 0.2.1 |
| xarray | 2026.4.0 |
| matplotlib | 3.10.9 |
| cartopy | 0.25.0 |
| pyproj | 3.7.2 |
| shapely | 2.1.2 |
| pykdtree | 1.4.3 |
| pyresample | 1.35.0 |
| xgcm | 0.9.0 |
| xmitgcm | 0.5.2 |
| zarr | 3.2.1 |
| s3fs | 2026.4.0 |
| aiohttp | 3.13.5 |
| botocore | 1.43.0 |
| dask | 2026.3.0 |
| distributed | 2026.3.0 |
| netCDF4 | 1.7.4 |
| pandas | 3.0.3 |
| jupyterlab | 4.5.7 |
| notebook | 7.5.6 |
| cmocean | 4.0.3 |
| tqdm | 4.67.3 |
| requests | 2.34.2 |


---

## 3. MacBook example — install miniforge and create the env

Install miniforge via Homebrew, initialize conda for zsh, and reload the shell:

```bash
brew install --cask miniforge
/opt/homebrew/bin/conda init zsh
source ~/.zshrc
```

Create the `ecco` environment with the scientific stack from conda-forge:

```bash
conda create -n ecco -c conda-forge -y \
    python=3.12 \
    numpy xarray matplotlib cartopy dask netcdf4 \
    jupyterlab notebook \
    pyresample cmocean xgcm xmitgcm \
    pyproj shapely tqdm pandas requests
```

---

## 4. Install the ECCO-specific packages

Activate the environment:

```bash
conda activate ECCOenv
```

**Install `ecco_v4_py` from a local clone** (recommended by the official guide):

```bash
git clone https://github.com/ECCO-GROUP/ECCOv4-py.git
pip install -e $yourpath/ECCOv4-py
```

The `-e` (editable) install lets `git pull` updates flow into the env without reinstalling.

**Pin `ecco_access` to 0.2.1:**

```bash
pip install "ecco_access==0.2.1"
```

> Why pin? PyPI's latest `ecco_access` 0.3.1 builds malformed PODAAC URLs (queries ~9 500 wrong granules and 404s). The copy bundled in the tutorial repo is too old to accept the notebook's `prompt_request_payer` argument. Version **0.2.1** is the sweet spot.

---

## 5. Patch `misc/jmd95.py` for NumPy 2.0

NumPy 2.0 removed `np.asfarray`. Replace its 6 call sites in `misc/jmd95.py` (lines 105–107 and lines 160–162):

```diff
- s = np.asfarray(s)
- t = np.asfarray(theta)
- p = np.asfarray(p)
+ s = np.asarray(s, dtype=float)
+ t = np.asarray(theta, dtype=float)
+ p = np.asarray(p, dtype=float)
```

`np.asarray(x, dtype=float)` is the documented NumPy-2-compatible replacement and behaves identically.

---

## 6. Launch the notebook

```bash
cd $yourpath/ECCO-v4-Python-Tutorial/Intro_to_PO_Tutorials
jupyter lab Steric_height.ipynb
```

---

## 7. Data

Two options for getting the required ECCO V4r4 granules:

**Option 1 — Direct download from Zenodo:**
Pull the data bundle from <https://zenodo.org/records/20278138> and adjust the download path inside the notebook to point at your local copy.

**Option 2 — Let the notebook fetch from PO.DAAC:**
The first few cells download data from `urs.earthdata.nasa.gov`. Prerequisites:

- `~/.netrc` containing your Earthdata credentials (`chmod 0600 ~/.netrc`)
- An empty `~/.urs_cookies` file
