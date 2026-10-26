# big_5_Computer_Vision
Computer Vision project to classify the big 5 animals (leopard, buffalo, lion, elephant, rhino) using ResNet50.

<img width="993" height="320" alt="image" src="https://github.com/user-attachments/assets/db7fda91-39df-465f-b29b-ab934d02bcba" />

## Summary
• All three strategies land at 97.7% to 98.3% test accuracy on a 299-image test set (feature extraction 97.99%, partial fine-tune 97.66%, full fine-tune 98.33%).
• The differences are 1 to 2 images, and the 95% Wilson intervals overlap almost completely (about 95.5% to 99.1%). On this evidence, the three methods cannot be ranked with confidence.
• Cost differs sharply. Full fine-tuning trains about 1,900 times more parameters than the frozen-backbone head (23.49M vs 12,294) and takes about 1.9 times the wall time of Experiment A for its stage (313.7 s vs 167.9 s).
• Fine-tuning fixed some errors and added one. Leopard recall rose from 92.6% to 96.3% for full fine-tuning, but one rhino was newly misclassified as zebra.
• Four class-level error patterns persist across all three models (buffalo to elephant, buffalo to rhino, zebra to rhino, leopard to zebra). Reviewing the images suggests most come from multi-animal scenes, a small subject, and probable label noise, not from missing model capacity.
• Main validity risk: lion and leopard come only from the Kaggle source, and the other four classes only from Ultralytics, so species and image source are confounded. 

## Limitations and threats to validity
• Species-source confound. Lion and leopard appear only in the Kaggle data; buffalo, elephant, rhino and zebra only in Ultralytics. Lion's perfect scores in C may partly reflect source cues (framing, resolution, tone). Mixed evidence: leopard errors in A and B went to elephant and zebra as well as lion, so the model is not purely keying on source, but the notebook has no test that separates the two.
• Possible leakage. Images were pooled and re-split. If either dataset contains near-duplicate frames or augmented copies, they may span train and test and inflate scores. Not checked.
• Model selection on the test set. The 'best' model was chosen by test macro-F1, which gives an optimistic estimate for C. Validation metrics should drive that choice.
• Small test set, single seed, single split. 299 images, 27 for leopard, no repeated runs. Differences of 1 to 2 images should not be reported as improvements.
• Label noise from detection-to-classification conversion. Majority-class-by-box-count labeling is lossy for multi-animal images.
• No per-image logging. Error overlaps across models is inferred from confusion-matrix cells only.

<img width="1010" height="372" alt="image" src="https://github.com/user-attachments/assets/faffab2e-26db-4cc0-8e51-23ed8e9917bb" />

More specifics on findings can be found in the report.
