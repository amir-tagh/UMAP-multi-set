# UMAP-multi-set
# UMAP Chemical Space Mapping for Multiple SMILES Sets

This repository provides a Python script to compute and visualize a **shared UMAP embedding** for multiple sets of SMILES molecules. It allows you to compare and visualize **chemical space overlap** across libraries with flexible plotting options.

---

## Features

- Input: multiple `.smi`, `.txt`, or `.csv` files (one SMILES per line by default).
- Fingerprint options:
  - **Morgan fingerprints** (default)
  - **RDKit fingerprints**
  - **AtomPair fingerprints**
- Dimensionality reduction:
  - **Optional PCA** pre-reduction
  - **UMAP** 2D embedding
- Visualization:
  - Multiple sets plotted together in a single embedding
  - Custom **colors**, **markers**, **alphas (transparency)**, and **marker sizes** per set
  - Bold, publication-ready styling (axes, ticks, labels)
- Outputs:
  - **CSV** file with SMILES, set name, and UMAP coordinates
  - **PNG** and/or **SVG** plot images

---

## Installation

Clone this repository and install dependencies:

```bash
git clone https://github.com/yourusername/umap-chemspace-multi.git
cd umap-chemspace-multi
conda create -n chemspace python=3.9 -y
conda activate chemspace
pip install rdkit-pypi umap-learn scikit-learn matplotlib pandas numpy tqdm

Usage
Basic example
python umap_multi_sets.py \
  --in set1.smi set2.smi \
  --labels Set1 Set2 \
  --outdir results \
  --save-png --save-csv

Custom fingerprints + UMAP settings
python umap_multi_sets.py \
  --in libA.smi libB.smi \
  --labels LibraryA LibraryB \
  --fp morgan --fp-bits 2048 --fp-radius 2 \
  --pca 50 \
  --n-neighbors 30 --min-dist 0.1 --metric jaccard \
  --title "UMAP overlap (Morgan, r=2)" \
  --colors red blue \
  --markers o x \
  --markersize 20 60 \
  --alpha 0.5 1.0 \
  --edgecolor none --edgewidth 0 \
  --legend --legend-cols 2 \
  --outdir results --save-svg --save-csv

Options
Input

--in FILES : One or more SMILES input files (≥2).

--labels NAMES : Labels for each input file (must match number of files).

--smiles-col INT : Column index for SMILES (default: 0).

--sep : Column delimiter (default: whitespace).

--infer-delim : Automatically detect delimiter.

--canonicalize : Canonicalize SMILES before featurization.

--max-n INT : Limit number of molecules per set.

Fingerprints

--fp {morgan,rdkit,atompair} : Fingerprint type (default: morgan).

--fp-bits INT : Number of fingerprint bits (default: 2048).

--fp-radius INT : Morgan fingerprint radius (default: 2).

PCA + UMAP

--pca INT : PCA components before UMAP (default: 50, 0 = disable).

--n-neighbors INT : UMAP n_neighbors (default: 30).

--min-dist FLOAT : UMAP min_dist (default: 0.1).

--metric STRING : UMAP distance metric (e.g., euclidean, jaccard).

--random-state INT : Random seed.

--n-epochs INT : Number of UMAP epochs (default: auto).

--learning-rate FLOAT : UMAP learning rate.

--verbose : Print UMAP progress.

Plot styling

--title STRING : Plot title.

--figsize W H : Figure size in inches (default: 8 6).

--colors COLORS : Colors per set (e.g., red blue green or hex codes).

--markers MARKERS : Markers per set (e.g., o x ^).

--alpha FLOATS : Transparency per set (e.g., 0.3 0.7 1.0).

--markersize FLOATS : Marker sizes per set (e.g., 20 40 100).

--edgecolor COLOR : Marker edge color (default: black, use none to disable).

--edgewidth FLOAT : Edge line width (default: 0.4).

--legend : Show legend.

--legend-loc STRING : Legend location (default: best).

--legend-cols INT : Legend column count.

Bold styling

--fontsize INT : Axis label font size (default: 12).

--title-size INT : Title font size (default: 14).

--tick-size INT : Tick font size (default: 11).

--legend-size INT : Legend font size (default: 11).

--axis-linewidth FLOAT : Axis line width (default: 1.8).

--tick-width FLOAT : Tick width (default: 1.8).

Output

--outdir DIR : Output directory (required).

--basename STR : Base filename for outputs (optional).

--save-png : Save PNG image.

--save-svg : Save SVG image.

--dpi INT : DPI for PNG (default: 300).

--save-csv : Save combined CSV file.
