# Introducing PolyGraphs: Running Philosophical Simulations and Analyzing Synthetic Data

A two-part lesson on using the [PolyGraphs](https://github.com/alexandroskoliousis/polygraphs) Python package to run philosophical simulations and analyze the synthetic data they generate, so as to better understand social processes of knowledge production.

**Authors:** Brian Ball, David Freeborn, Federica Imbriale, Amil Mohanan and Nicolas Kuri Perez Villaman (Computational Philosophy Lab, Northeastern University London).

[![Lesson DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.ZENODO-LESSON-DOI.svg)](https://doi.org/10.5281/zenodo.ZENODO-LESSON-DOI)
[![Dataset DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.ZENODO-DATASET-DOI.svg)](https://doi.org/10.5281/zenodo.ZENODO-DATASET-DOI)

## Contents

- [Part 1: Running Simulations](part-1-running-simulations.md) introduces key concepts of network theory and social epistemology, and shows how to install PolyGraphs, run simulations, edit configuration files, and import your own graph datasets.
- [Part 2: Analyzing Synthetic Data](part-2-analyzing-data.md) shows how to load PolyGraphs output into a pandas dataframe, visualize graphs and the evolution of opinion over time, and extend the built-in `Processor` class to analyze a case study on mis- and disinformation.
- `images/` holds the figures used in both parts.

## How this lesson and its data are archived

This lesson lives in two places, each with its own permanent DOI on [Zenodo](https://zenodo.org):

| What | Where | DOI |
|---|---|---|
| Lesson text, figures and code snippets (this repository) | GitHub, archived automatically on Zenodo at each release | https://doi.org/10.5281/zenodo.ZENODO-LESSON-DOI |
| Dataset `cleaned_data_v3_pt.tar.gz` used in Part 2 (about 2 GB) | Zenodo only. It is too large for GitHub | https://doi.org/10.5281/zenodo.ZENODO-DATASET-DOI |

The lesson DOI above is a *concept* DOI: it always resolves to the latest released version of this repository, and each GitHub release also receives its own version-specific DOI on Zenodo. Cite the concept DOI unless you need to refer to a particular version.

## Getting the dataset

Part 2 of the lesson analyzes a cleaned dataset of PolyGraphs simulation output. To obtain it:

1. Open the dataset record: https://doi.org/10.5281/zenodo.ZENODO-DATASET-DOI
2. Download `cleaned_data_v3_pt.tar.gz` (about 2 GB compressed; allow roughly 35 GB of free disk space for the unpacked data).
3. Check the download is intact by comparing its MD5 checksum with the one shown beside the file on the Zenodo record:

   ```
   md5sum cleaned_data_v3_pt.tar.gz        # Linux
   md5 cleaned_data_v3_pt.tar.gz           # macOS
   certutil -hashfile cleaned_data_v3_pt.tar.gz MD5   # Windows
   ```

4. Unpack it. Part 2 explains where to put it and how to point the analysis code at it:

   ```
   tar -xzf cleaned_data_v3_pt.tar.gz
   ```

The data are entirely synthetic and contain no personal information. Dataset authors: Brian Ball, David Freeborn, Federica Imbriale and Amil Mohanan.

## Software requirements

The lesson uses the `ptgraph` branch of PolyGraphs together with Python 3, Jupyter, numpy, pandas, matplotlib, networkx and seaborn. Installation is covered step by step in Part 1, including instructions for running in Google Colab.

## Citing this lesson

Please cite this repository using the metadata in [CITATION.cff](CITATION.cff) (GitHub shows a ready-made citation under "Cite this repository"). Cite the dataset separately using its own DOI. Background reading on the PolyGraphs project:

- Ball, B., Koliousis, A., Mohanan, A., & Peacey, M. (2024). Computational philosophy: reflections on the PolyGraphs project. *Humanities and Social Sciences Communications*, 11(1), 1–9.
- Ball, B., Koliousis, A., Mohanan, A., & Peacey, M. (2024). Misinformation and higher-order evidence. *Humanities and Social Sciences Communications*, 11(1), 1–12.

## License

- Lesson text and figures: Creative Commons Attribution 4.0 International (CC BY 4.0)
- Code snippets: MIT License
- Dataset: CC BY 4.0 (stated on the Zenodo record)

See [LICENSE](LICENSE) for details.

## For maintainers

The steps for depositing the dataset, enabling the Zenodo archive of this repository, and filling in the DOIs are in [RELEASING.md](RELEASING.md).
