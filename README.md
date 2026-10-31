# CSCI461 Assignment 1 - IMDB Review Analysis

Analysis of 50,000 IMDB reviews for sentiment classification and K-Means clustering.

## Project files

```text
data/IMDB Dataset.csv              source data
notebook/analysis.ipynb            complete analysis notebook
output/figures/                    saved charts and confusion matrices
output/files/                      cleaned data, metrics, and cluster summary
screenshots/                       Docker and JupyterLab evidence
Dockerfile                         JupyterLab image definition
requirements.txt                   additional Python packages
```

## Run locally

Build the image from the project root:

```powershell
docker build -t bd-a1 .
```

Run JupyterLab with the notebook and outputs stored on the host:

```powershell
docker run -p 8888:8888 --name bd-a1 -v "${PWD}\notebook:/home/jovyan/work/notebook" -v "${PWD}\output:/home/jovyan/work/output" bd-a1
```

Open the JupyterLab URL printed in the terminal, then run `notebook/analysis.ipynb` from top to bottom.

`bd-a1` is the image built from the Dockerfile. The running container is an instance of that image. In `-p 8888:8888`, the first port is on the host and the second is inside the container. The two bind mounts keep notebook edits and `output/` files after the container stops or is removed.

## Docker commands used for evidence

```powershell
docker images
docker ps
docker ps -a
docker logs bd-a1
docker inspect bd-a1
```

## Docker Hub

Published image: `lark201/bd-a1:latest`

```powershell
docker tag bd-a1 lark201/bd-a1:latest
docker push lark201/bd-a1:latest
docker pull lark201/bd-a1:latest
docker run -p 8888:8888 --name bd-a1 -v "${PWD}\notebook:/home/jovyan/work/notebook" -v "${PWD}\output:/home/jovyan/work/output" lark201/bd-a1:latest
```

## Saved results

| Result | Location |
|---|---|
| Cleaned review data | `output/files/cleaned_data.csv` |
| Supervised-model metrics | `output/files/logisticReg_metrics.txt`, `output/files/linearSVC_metrics.txt` |
| K-Means sizes, label comparison, silhouette score, and cluster notes | `output/files/cluster_summary.txt` |
| Correlation heatmap | `output/figures/correlation_heatmap.png` |
| Word-frequency comparison | `output/figures/word_frequency_comparison.png` |
| Sentiment-group comparison | `output/figures/group_comparison.png` |
| Logistic Regression and LinearSVC confusion matrices | `output/figures/logisticReg_confusion_matrix.png`, `output/figures/linearSVC_confusion_matrix.png` |

## Assignment checklist

| Requirement | Done in |
|---|---|
| Docker image, packages, working directory, dataset, and notebook copy | `Dockerfile`, `requirements.txt` |
| Dataset inspection, cleaning, `loc`/`iloc`, transformations, sampling, and correlation | `notebook/analysis.ipynb` under **Data Analysis and Preprocessing** |
| Cleaning, token counts, word frequencies, group comparison, and five observations | `notebook/analysis.ipynb` under **Text Analysis** |
| TF-IDF, Logistic Regression, LinearSVC, metrics, and confusion matrices | `notebook/analysis.ipynb` under **Supervised Text Classification**; metric and figure paths above |
| K-Means, selection of `k`, silhouette score, cluster sizes, top terms, and label comparison | `notebook/analysis.ipynb` under **K-Means Clustering**; `output/files/cluster_summary.txt` |
| Docker build, image, container, JupyterLab, push, pull, and Docker Hub evidence | `screenshots/` |
