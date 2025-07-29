# DCAR：Dual Prompt Learning for Adapting Vision-Language Models to Downstream Image-Text Retrieval
Recently, prompt learning has demonstrated remarkable success in adapting pre-trained Vision-Language Models (VLMs) to various downstream tasks such as image classification. However, its application to the downstream Image-Text Retrieval (ITR) task is more challenging. We find that the challenge lies in discriminating both **fine-grained attributes** and **similar subcategories** of the downstream data. To address this challenge, we propose **D**ual prompt Learning with Joint **C**ategory-**A**ttribute **R**eweighting (**DCAR**), a novel dual-prompt learning framework to achieve precise image-text matching. The framework dynamically adjusts prompt vectors from both semantic and visual dimensions to improve the performance of CLIP on the downstream ITR task. Based on the prompt paradigm, DCAR jointly optimizes attribute and class features to enhance fine-grained representation learning. Specifically, (1) at the attribute level, it dynamically updates the weights of attribute descriptions based on text-image mutual information correlation; (2) at the category level, it introduces negative samples from multiple perspectives with category-matching weighting to learn subcategory distinctions. To validate our method, we construct the Fine-class Described Retrieval Dataset (FDRD), which serves as a challenging benchmark for ITR in downstream data domains. It covers over *1,500* downstream fine categories and *230,000* image-caption pairs with detailed attribute annotations. Extensive experiments on FDRD demonstrate that DCAR achieves state-of-the-art performance over existing baselines.

![Figure 1](https://github.com/wyf202322/DCAR/blob/main/figure/fig1.svg)

Figure 1: Comparison between our dataset and existing datasets. The text inside the rounded rectangles represents the image captions. Our FDRD includes both detailed attribute descriptions and fine-grained category information.

## Proposed Method
The overview of our method is shown in Fig.2. Specifically, the framework introduces dual prompts to optimize both visual and textual representations, and ensures robust cross-modal alignment with two key aspects: **(1)Dynamic Token Re-Weighting:** We dynamically re-weight tokens based on their mutual information with text-image correlation, enhancing attribute awareness. **(2) Category Aware Augmentation:** We employ negative samples augmentation with emphasis on the fine-grained discriminative among subcategories of the same meta-category. 
These components improve retrieval accuracy by aligning descriptions with visual semantics. 

![Figure 2](https://github.com/wyf202322/DCAR/blob/main/figure/fig2.png)

Figure 2: Overview of DCAR approach.

## Fine-class Described Retrieval Dataset
![Figure 3](https://github.com/wyf202322/DCAR/blob/main/figure/fig3.jpg)

Figure 3: The pipeline for constructing the Fine-class Described Retrieval Dataset (FDRD).

The JSON files containing image captions for the FDRD dataset can be found in the [FDRD](https://github.com/wyf202322/DCAR/blob/main/FDRD)

## Installation
For installation and other package requirements, please follow the instructions detailed in [INSTALL.md](https://github.com/wyf202322/DCAR/blob/main/INSTALL.md).

Please follow the instructions at [DATASETS.md](https://github.com/wyf202322/DCAR/blob/main/DATASETS.md) to prepare all datasets.

## Main Result

We use [CLIP-ViT-B/32](https://huggingface.co/models?library=open_clip) as the pre-trained model.

- `Baseline`: To validate the effectiveness of DCAR, we use the following baselines:

  (1) [CLIP](https://github.com/openai/CLIP), (2) [CoOp](https://github.com/KaiyangZhou/CoOp), (3) [CLIP-Adapter](https://github.com/gaopengcuhk/CLIP-Adapter), (4) [MaPle](https://github.com/muzairkhattak/multimodal-prompt-learning), (5) [FILIP](https://arxiv.org/abs/2111.07783), (6) [Alip](https://github.com/deepglint/ALIP), (7) [FineCLIP](https://github.com/Timsty1/FineCLIP).
- `Evaluation Metrics`: Recall@K. The *K* list of Rank-*K*. *(str) default: [1, 5,10].*
- `AVG`: Average performance across the downstream fine-grained domains.

| Dataset      | R@K  | Image-to-Text |       |         |       |       |       |          |       | Text-to-Image |       |         |       |       |       |          |       |
| ------------ | ---- | ------------- | ----- | ------- | ----- | ----- | ----- | -------- | ----- | ------------- | ----- | ------- | ----- | ----- | ----- | -------- | ----- |
|              |      | CLIP|CoOp| CLIP-Adapter | MaPle | FILIP | Alip  | FineCLIP | DCAR(Ours)  |CLIP | CoOp| CLIP-Adapter | MaPle | FILIP | Alip  | FineCLIP | DCAR(Ours) |
| Caltech101   | 1    | 38.99         | 45.13 | 39.41   | 46.26 | 41.02 | 43.51 | 46.46    | 48.13 | 32.17         | 29.70 | 30.22   | 29.69 | 33.23 | 35.86 | 37.20    | 36.78 |
|              | 5    | 69.49         | 76.12 | 70.93   | 77.09 | 70.43 | 74.23 | 77.75    | 80.14 | 64.54         | 60.81 | 60.44   | 60.97 | 65.21 | 68.94 | 71.43    | 70.16 |
|              | 10   | 82.68         | 87.03 | 83.34   | 87.31 | 84.17 | 83.97 | 85.24    | 89.00 | 78.66         | 75.86 | 75.42   | 76.55 | 78.84 | 80.15 | 82.24    | 82.31 |
| OxfordPets   | 1    | 40.77         | 49.88 | 43.43   | 49.40 | 41.97 | 47.11 | 48.45    | 52.88 | 30.69         | 31.59 | 29.19   | 30.50 | 31.28 | 36.63 | 35.93    | 39.82 |
|              | 5    | 70.13         | 78.81 | 72.83   | 78.36 | 72.73 | 75.60 | 75.88    | 81.80 | 55.52         | 59.61 | 54.21   | 57.94 | 57.38 | 61.01 | 66.78    | 69.56 |
|              | 10   | 81.60         | 87.80 | 83.36   | 87.63 | 83.79 | 83.68 | 85.17    | 90.93 | 68.38         | 72.14 | 67.08   | 71.16 | 69.77 | 76.81 | 80.43    | 81.08 |
| StanfordCars | 1    | 25.88         | 34.33 | 32.41   | 43.50 | 24.97 | 28.12 | 40.78    | 45.52 | 18.60         | 21.63 | 18.65   | 26.78 | 16.14 | 21.04 | 27.20    | 32.90 |
|              | 5    | 52.22         | 65.62 | 63.26   | 76.44 | 51.63 | 58.95 | 67.46    | 79.05 | 43.22         | 46.81 | 43.24   | 54.96 | 41.29 | 47.82 | 59.18    | 64.06 |
|              | 10   | 65.96         | 78.10 | 75.87   | 86.17 | 63.25 | 71.48 | 80.31    | 88.41 | 56.78         | 59.62 | 55.79   | 67.45 | 53.31 | 61.81 | 67.82    | 76.21 |
| Flowers102   | 1    | 16.08         | 24.33 | 18.00   | 24.38 | 18.96 | 20.34 | 20.75    | 26.04 | 12.87         | 12.11 | 10.32   | 12.38 | 13.75 | 13.56 | 16.16    | 18.56 |
|              | 5    | 41.21         | 57.63 | 47.68   | 60.30 | 51.31 | 51.44 | 54.18    | 62.47 | 39.59         | 36.19 | 33.94   | 37.92 | 40.55 | 40.20 | 42.97    | 43.65 |
|              | 10   | 57.00         | 75.16 | 64.98   | 76.51 | 66.10 | 68.81 | 72.85    | 78.83 | 58.14         | 52.11 | 49.17   | 55.66 | 58.62 | 59.51 | 60.59    | 61.30 |
| Food101      | 1    | 13.83         | 18.77 | 13.99   | 19.50 | 13.52 | 15.24 | 19.06    | 21.80 | 6.98          | 8.50  | 6.20    | 8.00  | 7.82  | 8.50  | 10.28    | 13.03 |
|              | 5    | 29.59         | 39.53 | 31.06   | 40.44 | 30.41 | 36.66 | 41.20    | 44.20 | 17.99         | 20.72 | 16.63   | 20.18 | 17.70 | 19.45 | 22.45    | 26.98 |
|              | 10   | 38.71         | 50.39 | 41.35   | 51.65 | 41.33 | 45.60 | 50.29    | 53.08 | 25.78         | 29.18 | 23.83   | 28.59 | 26.25 | 29.31 | 34.07    | 37.33 |
| FGVCAircraft | 1    | 19.41         | 23.80 | 21.98   | 26.12 | 23.87 | 20.36 | 22.33    | 28.94 | 18.93         | 12.84 | 12.48   | 14.12 | 19.13 | 18.72 | 20.96    | 20.47 |
|              | 5    | 41.91         | 51.66 | 46.94   | 54.03 | 47.13 | 43.29 | 53.64    | 56.43 | 42.12         | 30.36 | 30.54   | 31.56 | 43.54 | 41.52 | 43.31    | 44.04 |
|              | 10   | 52.45         | 64.07 | 57.59   | 66.75 | 58.58 | 55.46 | 64.43    | 68.32 | 52.50         | 40.56 | 40.02   | 42.33 | 53.65 | 51.72 | 55.31    | 55.60 |
| SUN397       | 1    | 34.94         | 43.05 | 37.09   | 45.60 | 43.88 | 42.14 | 42.53    | 47.34 | 23.48         | 19.03 | 19.97   | 18.62 | 30.22 | 29.97 | 29.28    | 34.30 |
|              | 5    | 62.06         | 72.65 | 65.05   | 74.36 | 69.82 | 69.64 | 69.07    | 75.29 | 49.03         | 42.55 | 44.43   | 41.26 | 59.12 | 58.51 | 54.49    | 61.11 |
|              | 10   | 73.68         | 83.11 | 79.84   | 84.76 | 78.54 | 77.69 | 79.72    | 88.91 | 62.55         | 55.94 | 57.86   | 54.00 | 69.34 | 67.23 | 63.83    | 72.78 |
|DTD          | 1    | 37.94         | 45.93 | 40.19   | 44.39 | 44.78 | 40.94 | 43.91    | 47.10 | 29.49         | 18.32 | 18.55   | 20.39 | 29.69 | 29.17 | 29.20    | 30.73 |
|              | 5    | 72.10         | 76.78 | 71.81   | 76.25 | 74.91 | 73.92 | 70.24    | 78.60 | 58.75         | 41.96 | 41.66   | 46.99 | 58.82 | 56.76 | 57.19    | 58.22 |
|              | 10   | 82.62         | 87.89 | 83.16   | 86.35 | 85.36 | 83.58 | 84.84    | 89.17 | 71.16         | 54.14 | 53.66   | 60.64 | 71.36 | 70.41 | 70.33    | 69.98 |
| UCF101       | 1    | 15.49         | 18.53 | 16.26   | 19.60 | 16.89 | 17.82 | 18.87    | 21.12 | 12.34         | 10.65 | 10.49   | 11.62 | 13.01 | 13.73 | 15.49    | 18.62 |
|              | 5    | 47.34         | 54.91 | 49.83   | 56.36 | 49.10 | 50.67 | 52.29    | 57.28 | 38.30         | 34.02 | 34.97   | 36.46 | 38.15 | 40.73 | 45.11    | 48.72 |
|              | 10   | 63.83         | 72.85 | 67.33   | 73.26 | 69.15 | 69.22 | 70.67    | 73.38 | 54.69         | 49.33 | 50.12   | 52.99 | 57.20 | 59.32 | 63.86    | 66.40 |
| AVG          | 1    | 27.04         | 33.75 | 29.20   | 35.42 | 29.98 | 30.62 | 33.68    | 37.65 | 20.62         | 18.26 | 17.34   | 19.12 | 21.59 | 23.02 | 24.63    | 27.25 |
|              | 5    | 54.01         | 63.75 | 57.71   | 65.96 | 57.50 | 59.38 | 62.41    | 68.36 | 45.45         | 41.45 | 40.01   | 43.14 | 46.86 | 48.33 | 51.43    | 54.06 |
|              | 10   | 66.50         | 76.27 | 70.76   | 77.82 | 70.03 | 71.05 | 74.84    | 80.00 | 58.74         | 54.32 | 52.55   | 56.60 | 59.82 | 61.81 | 64.28    | 67.00 |


***More code will be released soon...***

## Acknowledgements
This repo benefits from [CLIP](https://github.com/openai/CLIP), [CoOp](https://github.com/KaiyangZhou/CoOp), [CLIP-Adapter](https://github.com/gaopengcuhk/CLIP-Adapter), [MaPle](https://github.com/muzairkhattak/multimodal-prompt-learning) and [InternLM-XComposer2.5](https://github.com/InternLM/InternLM-XComposer). We thank the authors for releasing their code. If you find our code and papers useful in your research, please consider citing these works as well.
