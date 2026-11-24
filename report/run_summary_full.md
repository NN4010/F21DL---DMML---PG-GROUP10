# Run summary: full run

Full Colab run (T4 GPU, seed 42) of `notebooks/DMML_Group10.ipynb`. All numbers below are copied from that run.

## Data after cleaning

| Dataset | Records | Train / test | Classes |
| --- | --- | --- | --- |
| D1 Maternal Health Risk | 451 | 360 / 91 | low 233, mid 106, high 112 |
| D2 Cardiotocography | 2,112 | 1,689 / 423 | normal 1,646, suspect 292, pathologic 174 |
| D3 FETAL_PLANES_DB | 12,400 images | 7,129 train (6,217 + 912 validation) / 5,271 test | 6 planes |

## Selected model per dataset

| Dataset | Selected model | Selection score | Test accuracy | Test macro-F1 |
| --- | --- | --- | --- | --- |
| D1 | Random Forest (tuned) | CV macro-F1 0.669 | 0.703 | 0.614 |
| D2 | Random Forest (tuned) | CV macro-F1 0.892 | 0.950 | 0.910 |
| D3 | EfficientNetB0 (2-phase fine-tune) | Val macro-F1 0.886 | 0.888 | 0.876 |

## Clustering agreement with the clinical labels (ARI)

| Dataset | K-Means | GMM (EM) | Ward | DBSCAN |
| --- | --- | --- | --- | --- |
| D1 | 0.045 | 0.041 | 0.045 | 0.013 |
| D2 | 0.039 | 0.088 | 0.187 | 0.111 |

## Files

`results/figures/`

- fig_D1_clustering_summary.png
- fig_D1_clusters_pca.png
- fig_D1_confusion_matrices.png
- fig_D1_decision_tree.png
- fig_D1_k_selection.png
- fig_D1_critical_class.png
- fig_D1_shap.png
- fig_D2_clustering_summary.png
- fig_D2_clusters_pca.png
- fig_D2_confusion_matrices.png
- fig_D2_decision_tree.png
- fig_D2_k_selection.png
- fig_D2_critical_class.png
- fig_D2_shap.png
- fig_class_distributions.png
- fig_cnn_training_curves.png
- fig_correlations.png
- fig_d1_boxplots.png
- fig_d2_violins.png
- fig_efficientnet_confusion.png
- fig_efficientnet_per_plane.png
- fig_efficientnet_training_curves.png
- fig_feature_relevance.png
- fig_gradcam.png
- fig_mlp_search.png
- fig_mlp_training_curves.png
- fig_model_comparison.png
- fig_skewness_before_after.png
- fig_ultrasound_samples.png
- fig_validation_curves.png

`results/tables/`

- all_results.csv
- best_model_per_family.csv
- best_parameters.json
- clustering_D1.csv
- clustering_D2.csv
- d1_feature_rank.csv
- d2_feature_rank.csv
- d3_plane_recall_vs_size.csv
- imbalance_experiment.csv
- metrics_detailed.csv
- selected_model_class_metrics.csv

`report/`

- run_summary_full.md
- run_log_full.txt (printed output of every cell)
