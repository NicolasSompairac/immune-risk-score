# immune-risk-score

Python Jupyter notebook to calculate an Immune Risk score on bulk RNA-seq samples using
immune cell-types geneset with single-sample Gene Set Enrichment (ssGSEA) and
penalised Cox modelling.

## Overview

This repository contains a workflow in a Jupyter notebook allowing to calculate
an immune risk score on bulk RNA-seq data by running a penalised Cox model on
single-sample Gene Set Enrichment (ssGSEA) enrichment score obtained from
immune cell-type markers extracted from a healthy bone marrow single-cell
dataset.
By default, the script uses a Lasso penalisation for the Cox modelling and
generates 3 immune risk groups using the median absolute deviation (MAD) of the
risk score.

## Workflow of the notebook

1.	Load the bulk RNA-seq data in logTPM and the corresponding survival table.
2.	Calculate the ssGSEA enrichment scores using the example immune cell-type
	markers obtained from the healthy bone marrow "bmcite" dataset from Seurat.
3.	Perform a penalised Cox modelling (default Lasso penalisation) with a 
	K-fold cross-validation (default 10-fold) for the alpha parameter optimisation.
4.	Generation of the immune risk score from the Cox modelling coefficients and
	identification of 3 immune risk groups (low, medium, high) using the median
	absolute deviation (MAD) of the risk score.

## Outputs

The paths are relative to the project directory with names based on the default
parameters.

-	`output/CoxLasso_modelling_10_kfold_norm_CV/`: outputs of the penalised Cox
	modelling (alpha optimisation curve, pointplot of Cox coefficients vs alpha,
	forestplot figure of cell-type coefficients, summary stats of each fold run,
	best fit Cox coefficients).
-	`output/CoxLasso_modelling_10_kfold_norm_CV/Risk_score/`: figure of the
	distribution of the risk score with the MAD separation.
-	`output/CoxLasso_modelling_10_kfold_norm_CV/Survival_curves/`: Kaplan-Meier
	curves of the 3 immune risk groups based on MAD.
-	`output/CoxLasso_modelling_10_kfold_norm_CV/Tables/`: Table of assigned risk
	scores and groups for each sample.
-	`output/ssGSEA/`: ssGSEA scores of each RNA-seq samples.

## Requirements

- Python version 3.8 or later
- Python packages: `sksurv`, `sklearn`, `pandas`, `numpy`, `matplotlib`,
`seaborn`, `gseapy`, `scipy`.

## Example data

The dataset available in the `example_data/` folder contains 132 AML bulk
RNA-seq samples and has been downloaded from the [UCSC Xena Browser](https://xenabrowser.net/datapages/?cohort=GDC%20TCGA%20Acute%20Myeloid%20Leukemia%20(LAML)).

## Citations
- S. Pölsterl, "scikit-survival: A Library for Time-to-Event Analysis Built on
Top of scikit-learn", Journal of Machine Learning Research, vol. 21, no. 212,
pp. 1–6, 2020.
- Pedregosa et al., "Scikit-learn: Machine Learning in Python", JMLR 12,
pp. 2825-2830, 2011.
- McKinney, "Data structures for statistical computing in python", Proceedings
of the 9th Python in Science Conference, Volume 445, 2010.
- Harris, C.R., Millman, K.J., van der Walt, S.J. et al. "Array programming with
NumPy". Nature 585, 357–362 (2020). DOI: 10.1038/s41586-020-2649-2. 
- J. D. Hunter, "Matplotlib: A 2D Graphics Environment", Computing in Science &
Engineering, vol. 9, no. 3, pp. 90-95, 2007.
- Waskom, M. L., (2021). "seaborn: statistical data visualization". Journal of
Open Source Software, 6(60), 3021, https://doi.org/10.21105/joss.03021.
- Zhuoqing Fang, Xinyuan Liu, Gary Peltz, "GSEApy: a comprehensive package for
performing gene set enrichment analysis in Python",
Bioinformatics, 2022;, btac757, https://doi.org/10.1093/bioinformatics/btac757.
- Virtanen, P., Gommers, R., Oliphant, T.E. et al., "SciPy 1.0: fundamental
algorithms for scientific computing in Python". Nat Methods 17, 261–272 (2020).
https://doi.org/10.1038/s41592-019-0686-2.
- Hao, Yuhan et al. "Integrated analysis of multimodal single-cell data."",
Cell vol. 184,13 (2021): 3573-3587.e29. doi:10.1016/j.cell.2021.04.048.

## Author

Nicolas Sompairac, King's College London
