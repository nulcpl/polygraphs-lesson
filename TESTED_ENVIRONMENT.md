# Tested Environment

The released lesson was tested on 18 September 2026 with the following environment. These versions record a known working setup; ordinary users do not need to install every package at exactly these versions.

| Software | Tested version |
| --- | --- |
| Python | 3.12.14 |
| PolyGraphs | 0.0.22a1 (`ptgraph` branch) |
| PolyGraphs commit | `3371ab323ae585bcff25296f0e45ba6cbf3895b4` |
| ptgraph | 0.1.0 |
| ptgraph commit | `0f51a8db6900302dc3cd08f2bf290126800a9063` |
| numpy | 2.5.3 |
| pandas | 3.0.6 |
| networkx | 3.6.1 |
| matplotlib | 3.11.2 |
| seaborn | 0.13.2 |
| torch | 2.14.0 |
| Jupyter | 1.1.1 |
| JupyterLab | 4.6.3 |

The PolyGraphs installation test (`python run.py -f configs/test.yaml`) completed successfully. The generated output was then loaded with `Processor`, and the lesson's graph plotting, belief plotting, and complete `DR_Processor` definition were exercised against it.
