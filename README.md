# DCAR：Dual Prompt Learning for Adapting Vision-Language Models to Downstream Image-Text Retrieval
Recently, prompt learning has demonstrated remarkable success in adapting pre-trained Vision-Language Models (VLMs) to various downstream tasks such as image classification. However, its application to the downstream Image-Text Retrieval (ITR) task is more challenging. We find that the challenge lies in discriminating both **fine-grained attributes** and **similar subcategories** of the downstream data. To address this challenge, we propose **D**ual prompt Learning with Joint **C**ategory-**A**ttribute **R**eweighting (**DCAR**), a novel dual-prompt learning framework to achieve precise image-text matching. The framework dynamically adjusts prompt vectors from both semantic and visual dimensions to improve the performance of CLIP on the downstream ITR task. Based on the prompt paradigm, DCAR jointly optimizes attribute and class features to enhance fine-grained representation learning. Specifically, (1) at the attribute level, it dynamically updates the weights of attribute descriptions based on text-image mutual information correlation; (2) at the category level, it introduces negative samples from multiple perspectives with category-matching weighting to learn subcategory distinctions. To validate our method, we construct the Fine-class Described Retrieval Dataset (FDRD), which serves as a challenging benchmark for ITR in downstream data domains. It covers over *1,500* downstream fine categories and *230,000* image-caption pairs with detailed attribute annotations. Extensive experiments on FDRD demonstrate that DCAR achieves state-of-the-art performance over existing baselines.

![Figure 1](https://github.com/wyf202322/DCAR/blob/main/figure/fig1.png)

Figure 1: Comparison between our dataset and existing datasets. The text inside the rounded rectangles represents the image captions. Our FDRD includes both detailed attribute descriptions and fine-grained category information.

## Proposed method
The overview of our method is shown in Fig.2. Specifically, the framework introduces dual prompts to optimize both visual and textual representations, and ensures robust cross-modal alignment with two key aspects: **(1)Dynamic Token Re-Weighting:** We dynamically re-weight tokens based on their mutual information with text-image correlation, enhancing attribute awareness. **(2) Category Aware Augmentation:** We employ negative samples augmentation with emphasis on the fine-grained discriminative among subcategories of the same meta-category. 
These components improve retrieval accuracy by aligning descriptions with visual semantics. 

![Figure 2](https://github.com/wyf202322/DCAR/blob/main/figure/fig2.png)

Figure 2: Overview of DCAR approach.

## Fine-class Described Retrieval Dataset
![Figure 3](https://github.com/wyf202322/DCAR/blob/main/figure/fig3.png)

The JSON files containing image captions for the FDRD dataset can be found in the [FDRD](https://github.com/wyf202322/DCAR/blob/main/FDRD)

***More code will be released soon...***

## Acknowledgements
This repo benefits from [CLIP](https://github.com/openai/CLIP), [CoOp](https://github.com/KaiyangZhou/CoOp), [CLIP-Adapter](https://github.com/gaopengcuhk/CLIP-Adapter), [MaPle](https://github.com/muzairkhattak/multimodal-prompt-learning) and [InternLM-XComposer2.5](https://github.com/InternLM/InternLM-XComposer). We thank the authors for releasing their code. If you find our code and papers useful in your research, please consider citing these works as well.
