# PolyGraphs: Running Simulations and Analysing Synthetic Data

This two-part lesson introduces [PolyGraphs](https://github.com/alexandroskoliousis/polygraphs), a Python package for studying how beliefs develop within communities.

PolyGraphs represents a community as a network of agents who gather evidence, communicate with one another, and update their beliefs. By changing the structure of the network, the reliability of its members, and other features of the model, we can study how these factors affect whether a community reaches the truth, falls into error, or fails to reach agreement.

The lesson covers both sides of this process: running simulations and analysing the data they produce.

**Authors:** Brian Ball, David Freeborn, Federica Imbriale, Amil Mohanan and Nicolas Kuri Perez Villaman, Computational Philosophy Lab, Northeastern University London.

[![Lesson DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.22727305.svg)](https://doi.org/10.5281/zenodo.22727305)
[![Dataset DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.22726906.svg)](https://doi.org/10.5281/zenodo.22726906)

## The lesson

**[Part 1: Running Simulations](part-1-running-simulations.md)** introduces the basic ideas behind PolyGraphs and shows you how to install the software and run your own simulations. It covers network structure, configuration files, and importing graph datasets.

**[Part 2: Analysing Synthetic Data](part-2-analyzing-data.md)** turns to the results. You will load PolyGraphs output into pandas, visualise networks and changing beliefs, and work through a case study on misinformation and disinformation. The final sections show how to extend PolyGraphs' `Processor` class for your own analyses.

The `images/` directory contains the figures used in both parts.

## Dataset

Part 2 uses a dataset of PolyGraphs simulations produced for the misinformation case study. The simulations are entirely synthetic and contain no personal data.

The compressed dataset is about 2 GB and is hosted separately on Zenodo:

https://doi.org/10.5281/zenodo.22726906

Download `cleaned_data_v3_pt.tar.gz`.

To check that the dataset downloaded correctly, open a terminal, or PowerShell on Windows, navigate to the folder containing `cleaned_data_v3_pt.tar.gz`, and run the appropriate command below. It will print an MD5 checksum. This should exactly match:

`3e90cf71fd52146eb4e542c0e132b7ba`

If it does not match, the download may be incomplete or corrupted and you should download the file again.

The downloaded file should also be `1,994,345,823 bytes`.

On Linux:

```bash
md5sum cleaned_data_v3_pt.tar.gz
```

On macOS:

```bash
md5 cleaned_data_v3_pt.tar.gz
```

On Windows:

```powershell
certutil -hashfile cleaned_data_v3_pt.tar.gz MD5
```

From the same directory, unpack the archive with:

```bash
tar -xzf cleaned_data_v3_pt.tar.gz
```

This creates the extracted `cleaned_data_v3_pt` directory. Roughly 35 GB of free disk space is required.

Part 2 explains where to place the resulting files and how to load them.

Dataset authors: Brian Ball, David Freeborn, Federica Imbriale and Amil Mohanan.

## Software

The lesson uses the `ptgraph` branch of PolyGraphs with Python 3.12 or later and Jupyter. The analysis also uses:

* numpy
* pandas
* matplotlib
* networkx
* seaborn

Part 1 covers installation from scratch, including an option for running PolyGraphs in Google Colab.

See the [tested environment](TESTED_ENVIRONMENT.md) for the PolyGraphs revision and software versions used to test the released lesson.

## Archive and citation

The lesson and dataset have separate permanent records on [Zenodo](https://zenodo.org/).

| Material                      | Location                                 | DOI                                     |
| ----------------------------- | ---------------------------------------- | --------------------------------------- |
| Lesson text, figures and code | GitHub, with releases archived on Zenodo | https://doi.org/10.5281/zenodo.22727305 |
| Dataset used in Part 2        | Zenodo                                   | https://doi.org/10.5281/zenodo.22726906 |

The lesson DOI is a *concept DOI*: it resolves to the latest archived release. Individual releases also receive version-specific DOIs. Use the concept DOI when citing the lesson as a whole, and a version-specific DOI when the exact version matters.

GitHub can generate a formatted citation from the metadata in [CITATION.cff](CITATION.cff). Please cite the dataset separately if you use it.

For background on PolyGraphs and the research behind the lesson, see:

* Ball, B., Koliousis, A., Mohanan, A., & Peacey, M. (2024). “Computational philosophy: reflections on the PolyGraphs project.” *Humanities and Social Sciences Communications*, 11(1), 1–9.
* Ball, B., Koliousis, A., Mohanan, A., & Peacey, M. (2024). “Misinformation and higher-order evidence.” *Humanities and Social Sciences Communications*, 11(1), 1–12.

## Licence

* Lesson text and figures: Creative Commons Attribution 4.0 International (CC BY 4.0)
* Code snippets: MIT License
* Dataset: CC BY 4.0

See [LICENSE](LICENSE) for details.

## Maintaining the repository

Instructions for publishing releases and archiving them on Zenodo are in [RELEASING.md](RELEASING.md).
