# Example data

The example input and reference output are published as GitHub Release assets rather than committed to Git history.

## Files

- `test_data.zip` — minimal Xenium example input. The compressed archive is approximately 28.8 MB and contains approximately 124 MB of uncompressed data.
- `output_data.zip` — reference workflow output. The compressed archive is approximately 114.6 MB and contains approximately 830 MB of uncompressed data.

Download both files from:

<https://github.com/glory-zhao/Spatial-Velo/releases/latest>

Extract `test_data.zip` into `data/test_data/` before running the notebooks.

## SHA-256 checksums

```text
24134dc26b3cb474603d7696093aeca50c59c75a5e9b602055e2a967d7e92395  test_data.zip
e101473fff25ec64136b354ff9c8b96dcf7cf5c5ec703d8a0088b5de74535437  output_data.zip
```

## Provenance

The example is derived from the 10x Genomics preview dataset **FFPE Human Lymph Node with 5K Pan Tissue and Pathways Panel**:

<https://www.10xgenomics.com/datasets/preview-data-xenium-prime-gene-expression>

The example contains selected B-cell populations and is intended only to demonstrate the Spatial-Velo workflow. Users are responsible for complying with the source dataset's terms of use and for citing the original data provider.

## Input files

`xenium_test_tx_file.csv` contains transcript-level coordinates, cell assignments, gene identities, and nuclear/cytoplasmic annotations. `xenium_test_metadata.csv` contains cell coordinates and cell-type annotations.

Neither archive should contain credentials, patient names, email addresses, or other direct identifiers. Before replacing these release assets, repeat the repository's privacy and secret checks.
