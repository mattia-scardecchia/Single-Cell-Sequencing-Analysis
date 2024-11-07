# Single Cell Sequencing Analysis

The results of this research project have been presented at the **Department of Oncology of Oxford University**, within the *Bioinformatics Hub conference series*, in July 2022. The main goal was building a classifier that, based on the gene expression profile of a cancerous cell, could predict whether the exposition to oxygen of that cell is normal (normoxia) or lower than normal (hypoxia). This information, in fact, is very relevant for the treatment.

This work was supervised by Prof. Francesca Buffa, and was a collaboration with Dario Filatrella, Rocco Giampetruzzi, Rolf Minardi, Alan Picucci and Klejdi Sevdari.

## Project Structure

We explored data coming from two cancerous cell lines (HCC1806, MCF7) that was collected using single-cell RNA sequencing techniques (SmartSeq, DropSeq). The analysis is structured in three main parts: Exploratory Data Analysis, Unsupervised Analysis and Supervised Learning. For a detailed overview of our methods, motivations and findings, refer to `report.ipyb`.

### Exploratory Data Analysis

In this phase, we investigated the statistical properties of our data through a large variety of plots. We used the insights we got to filter our dataset, at the level of both cells and of genes. For cells, we removed those whose expression profile revealed that they were likely dying, had a broken cell membrane, or had been  misrecorded. For genes, we selected those that had enough variability across different cells to be informative for prediction of hypoxia/normoxia.

Cell Filtering             |  Gene Filtering
:-------------------------:|:-------------------------:
![Each circle represents a cell from HCC sequenced with SmartSeq, with an indication of the sparsity of its expression profile (x axis), its total volume (y axis) and the fraction of mithocondrial genes (circle radius)](https://github.com/MattiaSC01/Single-Cell-Sequencing-Analysis/blob/main/figures_readme/volume_vs_sparsity_vs_mitochondria.png)  |  ![Each dot here represents a gene, with an indication of mean and variance of its expression across HCC cells in the SmartSeq sequencing](https://github.com/MattiaSC01/Single-Cell-Sequencing-Analysis/blob/main/figures_readme/mean_variance.png)

### Unsupervised Analysis

In this phase, we used various dimensionality reduction and clustering techniques to gain more insight into the structure of our data, as well as to obtain a parsimonious representation of the gene expression profiles to make supervised learning more efficient. Here, for instance, you can see a visualization of the gene expression profiles of cells, where genes and cells have been ordered based on the results of agglomerative clustering run independently for both.

![gene_expression ordering based on agglomerative clustering](https://github.com/MattiaSC01/Single-Cell-Sequencing-Analysis/blob/main/figures_readme/gene_expression_using_clustering_ordering.png)

### Supervised Learning

In the final phase, we trained and evaluated classifiers using a variety of machine learning techniques, from simple random forests to deep residual neural networks. We leveraged the filtering and the unsupervised analysis to reduce noise and engineer good features for our models. Using a K-fold cross-validation scheme, we selected the best performing models and built an ensemble that was able to correctly predict hypoxia/normoxia with 95-97% accuracy on a held-out test set (with roughly balanced classes), depending on the cell line and sequencing technique.
