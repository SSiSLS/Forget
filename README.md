# Forget

- A pdf version of the lecture on **Estimating the Circulation and Climate of the Ocean (ECCO)** is available @ https://doi.org/10.13140/RG.2.2.28126.60489/1
- Below is the information on tutorials and suggested exercises

## Notebooks we will go over and try out together

- explore standard ECCO diagnostics interactively via Pluto/Julia using [Climatology.jl](https://juliaocean.github.io/Climatology.jl/dev/examples/ECCO_standard_plots.html)
- adjoint reconstruction in python or julia notebook (notebook & data provided)
- reference ECCO recipes to analyze sea level from gridded output in Python :
  - https://ecco-v4-python-tutorial.readthedocs.io/Steric_height.html
  - https://ecco-v4-python-tutorial.readthedocs.io/Steric_SSH_OBP.html
  - https://ecco-v4-python-tutorial.readthedocs.io/ECCO_v4_Volume_budget_closure.html

## Input data 

- For the tutorial on ECCO reconstruction, all that is need is @ https://zenodo.org/records/20301468
- For the tutorial on steric sea level and bottom pressure in ECCO, the files needed are @ https://zenodo.org/records/20278138
  - Alternatively, a better idea in the long run for all NASA data needs is to get an account on earthdata.nasa.gov as explained @ https://ecco-v4-python-tutorial.readthedocs.io/ECCO_access_intro.html to enable you to use `ecco_access`
- For the tutorial on steric sea level and bottom pressure in ECCO, see `StericHeight_Environments.md`

## More that you can try on your own

- calculate global steric sea level in python or julia based on [Greatbatch 1994](https://agupubs.onlinelibrary.wiley.com/doi/10.1029/94JC00847)
- [rerunning ECCO4r4](https://zenodo.org/records/10038354) on your favorite computer (96 cores is great, 16 cores is enough but 6x slower)
- explore level 4 sea level anomaly data sets using [Climatology.jl](https://juliaocean.github.io/Climatology.jl/dev/examples/SatelliteAltimetry.html)
- diagnoze near surface seawater pathways using Oscar data product (2D) using [Drifters.jl](https://juliaclimate.github.io/Drifters.jl/dev/examples/Oscar_model.html)
- simulate seawater pathways using ECCO flow fields (3D or 2D) using [Drifters.jl](https://juliaclimate.github.io/Drifters.jl/dev/examples/global_ocean_circulation.html)
- differentiable programming (adjoint modeling) example on air-sea fluxes using [ECCO.jl](https://gaelforget.github.io/ECCO.jl/dev/examples/)
- build and run MITgcm interactively from Julia using [MITgcm.jl](https://gaelforget.github.io/MITgcm.jl/dev/)

## Acknowledgments

- Thanks to Drs Yuanyuan Song, Yueyang Lu for setting up and leading the tutorials. 
- Thanks to Dr Ian Fenty for contributing slides used in the lecture, Dr Ou Wang for contributing to the tutorials session.
- Thanks to the ECCO community and to NASA for their support and contributions.

Gaël Forget
