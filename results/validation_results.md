# Validation Results

## Experimental Setup

The local validation evaluates image retrieval performance across different camera views.

* Query camera: `c001`
* Gallery cameras: `c002`, `c003`
* Evaluation metrics: Rank-1, Rank-5, Rank-10

## Baseline

The model uses a pretrained ResNet-18 as the image encoder.

Images are resized while preserving their original aspect ratio and padded to `224 × 224`.

The resulting 512-dimensional embeddings are L2-normalized before cosine similarity is computed.

## Batch Hard Triplet Loss

Training uses Batch Hard Triplet Loss with:

* `P = 4` identities per batch
* `K = 4` images per identity
* Batch size: `16`
* Margin: `0.2`
* Training: 5 epochs × 100 batches

The final local validation results were:

| Metric  |  Score |
| ------- | -----: |
| Rank-1  | 50.94% |
| Rank-5  | 73.72% |
| Rank-10 | 81.32% |

## Random Erasing Experiment

Random Erasing was evaluated as an additional augmentation strategy.

| Setting                | Rank-1 | Rank-5 | Rank-10 |
| ---------------------- | -----: | -----: | ------: |
| Without Random Erasing | 50.94% | 73.72% |  81.32% |
| With Random Erasing    | 49.01% | 72.24% |  80.87% |

Random Erasing reduced performance on the local validation set, so it was not used in the final submission pipeline.

## Class-level Analysis

The validation Rank-1 accuracy varied substantially across object categories:

| Class          | Rank-1 |
| -------------- | -----: |
| Traffic signal | 62.43% |
| Rubbish bins   | 46.32% |
| Container      | 37.65% |
| Crosswalk      | 27.04% |

Crosswalk was the most challenging category.

Further analysis showed that smaller crosswalk images were particularly difficult because of severe structural information loss.

## Kaggle Submission

The final inference pipeline extracts embeddings for all query and test images, computes cosine similarity, and retrieves the top-100 test images for each query.

The competition uses 1-based test identifiers, so the PyTorch 0-based indices are converted before generating the submission file.

Final public leaderboard score:

**0.05070 mAP**

## Observations

The experiments suggest that:

1. Image aspect ratio is important for this dataset because many images are highly elongated.
2. Batch Hard Triplet Loss provides a useful baseline for visual re-identification.
3. Random Erasing did not improve local validation performance.
4. Crosswalk images remain the most difficult category.
5. The gap between local validation and the Kaggle leaderboard suggests a significant domain difference between the local camera split and the competition's query camera.
