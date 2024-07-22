<p align="center">
  <h2 align="center">UMATO</h2>
	<h3 align="center">Uniform Manifold Approximation with Two-phase Optimization</h3>
</p>

---



Uniform Manifold Approximation with Two-phase Optimization (UMATO) is a dimensionality reduction technique, which can preserve the global as well as the local structure of high-dimensional data. Most existing dimensionality reduction algorithms focus on either of the two aspects, however, such insufficiency can lead to overlooking or misinterpreting important global patterns in the data. Moreover, the existing algorithms suffer from instability. 
To address these issues, UMATO proposes a two-phase optimization: global optimization and local optimization. First, we obtain the global structure by selecting and optimizing the hub points.
Next, we initialize and optimize other points using the nearest neighbor graph. Our experiments with one synthetic and three real world datasets show that UMATO can outperform the baseline algorithms, such as PCA, [t-SNE](https://lvdmaaten.github.io/tsne/), [Isomap](https://scikit-learn.org/stable/modules/generated/sklearn.manifold.Isomap.html), [UMAP](https://github.com/lmcinnes/umap), [LAMP](https://github.com/lgnonato/LAMP) and [PacMAP](https://github.com/YingfanWang/PaCMAP), in terms of accuracy, stability, and scalability.

## System Requirements
- Python 3.9 or greater
- scikit-learn
- numpy
- scipy
- numba
- pandas (to read csv files)

## Installation 

UMATO is available via pip.

```sh
pip install umato
```

```python
import umato
from sklearn.datasets import load_iris

X, y = load_iris(return_X_y=True)
emb = umato.UMATO(hub_num=50).fit_transform(X)
```

For detailed information on the algorithm and parameter usage, check the API listed under Wiki.

## Findings

#### Figure 1: Accuracy Rankings in Dimensionality Reduction
![Figure 1](path/to/figure1.png)  
**Description:** This figure illustrates the average scores of nine DR techniques in the accuracy analysis. Techniques ranked in the top four are highlighted in blue, with darker shades indicating higher accuracy. Techniques ranked in the bottom four are highlighted in red, with darker shades indicating lower performance. UMATO outperforms other techniques significantly in terms of global metrics, with a slight sacrifice in local metrics. Both the original data and projections are standardized to minimize the impact of scaling.
<style>
    table.dr-table {
        font-size: 0.8em; /* Adjusts the font size to be smaller */
        width: 100%; /* Ensures the table uses the full width available */
        border-collapse: collapse; /* Improves the appearance of borders */
    }
    table.dr-table th, table.dr-table td {
        border: 1px solid #ccc; /* Adds borders to cells for better readability */
        padding: 5px; /* Adds padding inside cells */
        text-align: center; /* Centers the text in cells */
    }
    table.dr-table caption {
        margin: 10px 0; /* Adds space around the caption */
    }
</style>
<table class="dr-table">
    <caption>The average scores that nine DR techniques obtain in the accuracy analysis. For each quality metric, DR techniques ranked in the first-fourth place are highlighted in blue, where we assign higher opacity to the better techniques. Similarly, techniques ranked in the sixth-ninth place are highlighted in red, where worse techniques have higher opacity. UMATO substantially outperforms baselines in terms of global metrics with a slight sacrifice in local metric scores. Note that we standardize both the original data and projections to minimize the impact of scaling.</caption>
    <thead>
        <tr>
            <th></th>
            <th colspan="10">Local</th>
            <th colspan="5">Global</th>
        </tr>
        <tr>
            <th></th>
            <th>Trust. k=10</th>
            <th>Trust. k=50</th>
            <th>Conti. k=10</th>
            <th>Conti. k=50</th>
            <th>MRRE_F k=10</th>
            <th>MRRE_F k=50</th>
            <th>MRRE_M k=10</th>
            <th>MRRE_M k=50</th>
            <th>Stead.</th>
            <th>Coherv.</th>
            <th>KL Div. σ=1</th>
            <th>KL Div. σ=.1</th>
            <th>DTM σ=1</th>
            <th>DTM σ=.1</th>
            <th>Stress</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>UMAP</td>
            <td style="background-color: #a3c1f7">0.9067</td>
            <td style="background-color: #bed7fa">0.8658</td>
            <td style="background-color: #8db3f5">0.9420</td>
            <td style="background-color: #ffcccc">0.8773</td>
            <td style="background-color: #a3c1f7">0.9113</td>
            <td style="background-color: #a3c1f7">0.8922</td>
            <td style="background-color: #8db3f5">0.9524</td>
            <td style="background-color: #8db3f5">0.9227</td>
            <td style="background-color: #a3c1f7">0.8538</td>
            <td style="background-color: #809ff4">0.6445</td>
            <td style="background-color: #ffe6e6">0.0042</td>
            <td style="background-color: #ffcccc">0.2383</td>
            <td style="background-color: #ffcccc">0.0662</td>
            <td style="background-color: #ffcccc">0.4056</td>
            <td style="background-color: #ffcccc">2.7369</td>
        </tr>
        <!-- Add additional rows here for other DR techniques, formatting them similarly -->
        <tr>
            <td><b>UMATO</b></td>
            <td>0.8502</td>
            <td style="background-color: #ffcccc">0.8299</td>
            <td style="background-color: #a3c1f7">0.9133</td>
            <td style="background-color: #bed7fa">0.8845</td>
            <td>0.8536</td>
            <td>0.8407</td>
            <td>0.9195</td>
            <td style="background-color: #bed7fa">0.9021</td>
            <td style="background-color: #ffcccc">0.7248</td>
            <td style="background-color: #a3c1f7">0.6222</td>
            <td style="background-color: #809ff4">0.0017</td>
            <td style="background-color: #8db3f5">0.1388</td>
            <td style="background-color: #809ff4">0.0362</td>
            <td style="background-color: #809ff4">0.3050</td>
            <td style="background-color: #a3c1f7">0.7949</td>
        </tr>
    </tbody>
</table>


#### Figure 2: Local and Global Metric Rankings
![Figure 2](path/to/figure2.png)  
**Description:** This figure ranks DR techniques by their performance on local and global quality metrics. UMATO shows the highest accuracy for global metrics and ranks fourth for local metrics. Error bars represent the 95% confidence interval. Detailed statistics are available in Table 2.

#### Figure 3: Scalability with Large Datasets
![Figure 3](path/to/figure3.png)  
**Description:** Results of the scalability analysis with large datasets. The size and dimensionality of each dataset are indicated on the left side of the dataset’s name. The runtime of each DR technique is presented in mm:ss format. UMATO outperforms almost all competitors except PCA, with an average speedup of ×14.3 over UMAP.

#### Figure 4: Projection Subset Analysis
![Figure 4](path/to/figure4.png)  
**Description:** Subset of the projections generated in our accuracy analysis. Colors represent the class label of each dataset, showing that UMATO excels in preserving global structure while maintaining competitive performance in depicting local structure.

#### Figure 5: Scalability with Small Datasets
![Figure 5](path/to/figure5.png)  
**Description:** The scalability analysis results with small datasets. LAMP has been removed due to its long computation time, making the runtime of other techniques appear similar. UMATO takes about three seconds on average to generate projections, outperforming all other nonlinear DR techniques. Error bars represent 95% confidence intervals.

## Citation

UMATO can be cited as follows:

```bibtex
@inproceedings{jeon2022vis,
  title={Uniform Manifold Approximation with Two-phase Optimization},
  author={Jeon, Hyeon and Ko, Hyung-Kwon and Lee, Soohyun and Jo, Jaemin and Seo, Jinwook},
  booktitle={2022 IEEE Visualization and Visual Analytics (VIS)},
  pages={80--84},
  year={2022},
  organization={IEEE}
}
```

Jeon, H., Ko, H. K., Lee, S., Jo, J., & Seo, J. (2022, October). Uniform Manifold Approximation with Two-phase Optimization. In 2022 IEEE Visualization and Visual Analytics (VIS) (pp. 80-84). IEEE.


<table>
    <caption>The average scores that nine DR techniques obtain in the accuracy analysis. For each quality metric, DR techniques ranked in the first-fourth place are highlighted in blue, where we assign higher opacity to the better techniques. Similarly, techniques ranked in the sixth-ninth place are highlighted in red, where worse techniques have higher opacity. UMATO substantially outperforms baselines in terms of global metrics with a slight sacrifice in local metric scores. Note that we standardize both the original data and projections to minimize the impact of scaling.</caption>
    <thead>
        <tr>
            <th></th>
            <th colspan="10">Local</th>
            <th colspan="5">Global</th>
        </tr>
        <tr>
            <th></th>
            <th>Trust. k=10</th>
            <th>Trust. k=50</th>
            <th>Conti. k=10</th>
            <th>Conti. k=50</th>
            <th>MRRE_F k=10</th>
            <th>MRRE_F k=50</th>
            <th>MRRE_M k=10</th>
            <th>MRRE_M k=50</th>
            <th>Stead.</th>
            <th>Coherv.</th>
            <th>KL Div. σ=1</th>
            <th>KL Div. σ=.1</th>
            <th>DTM σ=1</th>
            <th>DTM σ=.1</th>
            <th>Stress</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>UMAP</td>
            <td style="background-color: #a3c1f7">0.9067</td>
            <td style="background-color: #bed7fa">0.8658</td>
            <td style="background-color: #8db3f5">0.9420</td>
            <td style="background-color: #ffcccc">0.8773</td>
            <td style="background-color: #a3c1f7">0.9113</td>
            <td style="background-color: #a3c1f7">0.8922</td>
            <td style="background-color: #8db3f5">0.9524</td>
            <td style="background-color: #8db3f5">0.9227</td>
            <td style="background-color: #a3c1f7">0.8538</td>
            <td style="background-color: #809ff4">0.6445</td>
            <td style="background-color: #ffe6e6">0.0042</td>
            <td style="background-color: #ffcccc">0.2383</td>
            <td style="background-color: #ffcccc">0.0662</td>
            <td style="background-color: #ffcccc">0.4056</td>
            <td style="background-color: #ffcccc">2.7369</td>
        </tr>
        <!-- Add additional rows here for other DR techniques, formatting them similarly -->
        <tr>
            <td><b>UMATO</b></td>
            <td>0.8502</td>
            <td style="background-color: #ffcccc">0.8299</td>
            <td style="background-color: #a3c1f7">0.9133</td>
            <td style="background-color: #bed7fa">0.8845</td>
            <td>0.8536</td>
            <td>0.8407</td>
            <td>0.9195</td>
            <td style="background-color: #bed7fa">0.9021</td>
            <td style="background-color: #ffcccc">0.7248</td>
            <td style="background-color: #a3c1f7">0.6222</td>
            <td style="background-color: #809ff4">0.0017</td>
            <td style="background-color: #8db3f5">0.1388</td>
            <td style="background-color: #809ff4">0.0362</td>
            <td style="background-color: #809ff4">0.3050</td>
            <td style="background-color: #a3c1f7">0.7949</td>
        </tr>
    </tbody>
</table>
