# Stellar Classification with KNIME

A visual machine learning workflow for classifying **galaxies, quasars, and stars** using the Sloan Digital Sky Survey DR17 dataset. The project compares seven classifier configurations and investigates how redshift, feature selection, and normalization affect performance.

[KNIME workflow](KNIME_project3.knwf) · [Project report](Machine_learning%20team%2048_%203rd%20feb.pdf)

## Dataset

The included `star_classification.csv` contains **100,000 observations** with 17 input attributes and the categorical target `class`:

- `GALAXY`
- `QSO` — quasar
- `STAR`

Inputs include photometric magnitudes, celestial coordinates, redshift, observation parameters, and identifiers.

Dataset reference: [Stellar Classification Dataset — SDSS17](https://www.kaggle.com/fedesoriano/stellar-classification-dataset-sdss17).

## Methodology

- Remove identifier-like variables and inspect feature relationships using Spearman correlations.
- Explore photometric feature engineering and reduce highly correlated predictors.
- Use a stratified **60% training / 30% validation / 10% test** partition with seed **71**.
- Compare tree-based models, Naive Bayes, and multilayer perceptrons.
- Evaluate accuracy, Cohen's kappa, confusion matrices, and ROC curves.
- Repeat selected experiments without redshift to assess feature dependence.

## Reported results

The project report's model-comparison table lists:

| Model | Accuracy | Cohen's kappa |
| --- | ---: | ---: |
| Bagging + PCA | **97.82%** | **0.9613** |
| Decision Tree | 97.69% | 0.9588 |
| Random Forest | 97.23% | 0.9505 |
| Gradient Boosting | 96.69% | 0.9411 |
| MLP with MinMax normalization | 95.56% | 0.9211 |
| MLP with Z-score normalization | 93.08% | 0.8765 |
| Naive Bayes | 75.00% | 0.5958 |

The report labels these as test-set results and presents validation confusion matrices separately. In its redshift-removal experiment, Bagging + PCA accuracy falls to approximately **87%**, highlighting the model's dependence on the available inputs.

## Open the workflow

1. Clone or download this repository.
2. Open **KNIME Analytics Platform** and import `KNIME_project3.knwf` using the workflow-import option.
3. Install any node extensions requested by KNIME. Configure a compatible Python environment if the Python Script node requires it.
4. Update the CSV Reader to point to the included `star_classification.csv`.
5. Execute the preprocessing and partitioning nodes, then the learner, predictor, and scorer branches.
6. Compare the node outputs with the accompanying report.

The repository does not specify a fully pinned KNIME and extension environment. Use the imported node settings as the reference when resolving compatibility differences.

## Scope and next steps

These results describe one dataset and its recorded experiments. Performance without redshift is a separate setting and should not be compared as though the same features were available.

Future improvements include documenting exact extension versions, checking sentinel values such as `-9999` in photometric fields, and validating on independent observations.

## Contributors

**Tony Dawra · Ilaria Mato · Raffaele Romano**  
University of Milano-Bicocca · Machine Learning · February 2026
