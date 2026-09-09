# Urban Elements Re-Identification 2026

Implementation and experiments for the Kaggle Urban Elements Re-ID Challenge 2026.

## Overview

This project explores image retrieval and re-identification of urban elements
using deep visual embeddings and metric learning.

## Dataset

- 14,947 images
- 1,453 identities
- 11,175 training images
- 928 query images
- 2,844 gallery/test images

## Approach

- ResNet-18 image encoder
- ImageNet-pretrained weights
- Aspect-ratio-preserving image preprocessing
- Batch Hard Triplet Loss
- Cosine similarity
- Top-100 image retrieval

## Validation

| Metric | Score |
|---|---:|
| Rank-1 | 50.94% |
| Rank-5 | 73.72% |
| Rank-10 | 81.32% |

## Project Status

Completed baseline implementation and submission pipeline.
