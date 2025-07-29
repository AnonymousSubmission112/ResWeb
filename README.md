This is the artifact for the paper "ResWeb: Resource-Rich Web Code Generation via Evolutionary Sampling." This artifact supplies the ResWeb toolkit and supplementary materials for the paper. 


This repository contains:

1. **Code implementation of ResWeb generation pipeline**, i.e., the Python script and instructions to run ResWeb to preprocess websites, and generate UI code from screenshots with resource lists. 
2.  **ResWeb Dataset**. Our experiment data (both original and generated) is available in `/dataset_collection/all_data`. 
3. **Image Quality Assessment dataset**. The human annotated image pairs for image quality assessment is available at `/experiment/RQ1/annotation.csv`. 
4. **A user-friendly tool based on ResWeb**.


Quick links: [Demo video](#Demo-video) | [ResWeb Examples](#Examples) | [Code usage](#Code-usage) | [Tool usage](#ResWeb-tool) 


# Abstract

Webpages often contain numerous internal and external resources, such as links, images, and downloadable content, which are essential for their functionality. Current approaches to "design-to-code" typically focus on self-contained webpages that do not include real links or images, overlooking the complexities of dynamic, resource-driven websites. This paper introduces the first comprehensive framework for generating, evaluating, and improving resource-rich webpages (ResWeb) from UI designs. Our contributions include: (1) the design of a data structure, the resource list, to track the correspondence between visual design elements and their associated resources (links, images, etc.) and a novel image-text interleaved HCI method for user input collection; (2) the creation of the first ResWeb dataset, comprising 10.2K websites with resource lists, screenshots, and ground truth code; (3) the introduction of new evaluation metrics tailored to ResWeb generation, measuring the correctness of generated resources and their alignment with visual design; and (4) a novel evolutionary-inspired sampling approach to enhance the quality of generated ResWeb by 2% - 25% on various metrics. Additionally, we present an easy-to-use framework and a release of code and data to encourage future research in this area. This work lays the foundation for advancing web development tools that can support resource-rich, real-world web applications.



# Demo video

This video demonstrates how the ResWeb tool enables code-free development from UI designs to resource-aware, navigable websites. 

https://github.com/user-attachments/assets/8b759d7d-21d5-49a3-96c6-b07d30384e98


# Examples

Comparison of self-contained website and multi-page resource-aware web (ResWeb). ResWeb supports multi-page navigation, real-image loading and backend routing.

![image-20241219171847068](assets/comparison1.png)

Adding resource lists can improve the visual similarity of a generated webpage across different MLLMs and metrics since resource lists enable MLLMs to include the exact images displayed on the webpage, thus enhancing the overall similarity. Without resource lists, MLLMs can only use placeholder images in the generated web code.

![image-20241219171953522](assets/comparison2.png)


# Code usage

## 0. Setup

```shell
pip install -r requirements.txt
```



## 1. Save & Process Website

```shell
# please create an unsplash API key and input to dataset_collection/img_gen_key.txt
python dataset_collection/collect_data.py
```

## 2. ResWeb Experiment

```shell
# store your respective API keys in keys/gptkey.txt, keys/geminikey.txt, keys/claudekey.txt
python experiment/experiments.py
```

## 3. Calculate Metrics

```shell
python experiment/RQ2/metrics.py
```



# ResWeb tool

1. Start the server

```shell
cd experiment/RQ4/tool
python app.py
```

2. Visit http://127.0.0.1:5000 via local browser

3. Usage:

   1. Upload an design image.
   2. draw bounding box on the image to indicate the element, specify corresponding resources on the right.

   ![image-20241219181219420](assets/tool.png)
