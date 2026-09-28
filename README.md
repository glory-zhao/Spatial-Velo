# Spatial-Velo

Spatial-Velo infers local, export-associated transcriptional tendencies from subcellular RNA localization in imaging-based spatial transcriptomics. It is designed for platforms such as Xenium, CosMx, and MERFISH that provide transcript coordinates but generally do not provide the spliced/unspliced information required by conventional RNA velocity.

The method uses a phenomenological radial transport model to summarize nuclear transcript organization, estimate a per-cell, per-gene delta signal, and combine that signal with current cytoplasmic expression. Downstream notebooks compute three cell-level kinetic descriptors: Hotspot, Coherence, and Specificity, and demonstrate metric-guided pseudotime analysis.

> Spatial-Velo estimates a local export-associated tendency. It should not be interpreted as a direct biochemical measurement of nuclear export or as a long-term forecast of the same cell's fate.

## Repository contents

| File | Purpose |
| --- | --- |
| `notebooks/step0_A.ipynb` | Optional MERFISH image tiling before nucleus segmentation. |
| `notebooks/step0_B.ipynb` | Optional MERFISH mask stitching and transcript-to-nucleus matching. |
| `notebooks/step1_corrected_output_folder.ipynb` | Recommended Step 1 implementation: radial normalization, model fitting, delta inference, and future-expression estimation. |
| `notebooks/step1_legacy.ipynb` | Legacy Step 1 implementation retained for reproducibility. |
| `notebooks/step2.ipynb` | UMAP and spatial visualization of the inferred velocity signal. |
| `notebooks/step3.ipynb` | Feature-gene and cell-state analyses. |
| `notebooks/step4.ipynb` | Hotspot, Coherence, Specificity, pseudotime, and optimal-transport analyses. |
| `requirements.txt` | Python dependencies. |
| `data/README.md` | Example-data provenance, download, and extraction instructions. |

For new analyses, use `step1_corrected_output_folder.ipynb`. The legacy Step 1 notebook is included only to preserve the earlier implementation.

## Installation

Python 3.11 or 3.12 is recommended.

```bash
git clone https://github.com/glory-zhao/Spatial-Velo.git
cd Spatial-Velo
python -m venv .venv
```

Activate the environment, then install the dependencies:

```bash
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

Step 0 additionally requires [CellProfiler](https://cellprofiler.org/) for nucleus segmentation. It is not needed for the supplied Xenium example because that dataset already contains cell assignments and subcellular compartment annotations.

## Example data

Download `test_data.zip` and `output_data.zip` from the repository's [latest release](https://github.com/glory-zhao/Spatial-Velo/releases/latest).

Extract the input archive so that the repository contains:

```text
data/test_data/
├── xenium_test_tx_file.csv
├── xenium_test_metadata.csv
└── README.txt
```

`output_data.zip` contains reference results from the example workflow and can be extracted separately for comparison. It is distributed as a release asset because it exceeds GitHub's 100 MB limit for ordinary repository files.

## Running the workflow

Start Jupyter from the repository root:

```bash
jupyter lab
```

Run the notebooks in this order:

1. `step1_corrected_output_folder.ipynb`
2. `step2.ipynb`
3. `step3.ipynb`
4. `step4.ipynb`

The notebooks default to `data/test_data`. To use another working directory without editing the notebooks, set the `SPATIAL_VELO_WORKDIR` environment variable. Set `SPATIAL_VELO_NORM_MODE` to `2D` or `3D` to select the normalization mode.

Steps 0A and 0B are only required when raw imaging data must first be segmented and matched to transcripts. Their input and output roots can be set with `SPATIAL_VELO_RAW_DATA_DIR` and `SPATIAL_VELO_OUTPUT_DIR`.

## Input schema

The transcript-level table used by the example contains:

- `cell`: cell identifier
- `gene`: gene identifier
- `global_x`, `global_y`: transcript coordinates
- `CellComp`: subcellular compartment (`Nuclear` or `Cytoplasm`)
- `nucleus_distance`: platform-provided or precomputed nucleus-distance information when available

The metadata table contains:

- `cell`: cell identifier
- `x`, `y`: cell coordinates
- `cell_type`: optional cell-state annotation

Column names can be adjusted in the configuration section of each notebook.

## Reproducibility notes

- Notebook outputs and local execution counts are cleared in the repository copy.
- Local absolute paths have been replaced with portable defaults and environment-variable overrides.
- The updated Step 2 implementation is retained; a duplicated earlier implementation was removed from the release notebook.
- Stochastic analyses may require setting the random seeds in the relevant configuration blocks for bitwise reproducibility.

## Citation

If you use Spatial-Velo, please cite:

Zhao Z, Sun Y, Xia Q. *Subcellular RNA localization encodes transcriptional time in situ*. Manuscript in preparation.

Citation metadata are also provided in `CITATION.cff`.

## Data source

The minimal example is derived from the publicly available 10x Genomics Xenium human lymph-node preview dataset. See `data/README.md` for provenance and redistribution notes.

## License

A reuse license has not yet been selected because the method is associated with a pending patent application. Until the authors replace the current `LICENSE` file, no permission to copy, modify, or redistribute the code is granted beyond rights provided by applicable law. For permission, contact Zhenjun Zhao at zhaozhenjun@shsmu.edu.cn.

