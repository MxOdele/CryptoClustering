# CryptoClustering

<div align='center'>
    <img src='https://images.pexels.com/photos/844124/pexels-photo-844124.jpeg' height='350' title='Coin representations of three cryptocurrencies (BitCoin, Etherium, and Ripple) next to a micro-sd card for scale (image courtesy of Pexels)' alt='Three coins stamped with the logos of the cryptocurrencies they represent - one gold coin with circutry lines and the "B" of BitCoin, one silver coin with the word "etherium" and a golden pyramid above a golden chevron, and one gold coin with a map of the word and the logo and lettering for "ripple" - all laying beside a micro-sd card.' />

*Crypto Clustering*[^1]

**Module 11 Challenge**

## READ ME
</div>

## Table of Contents

* [Overview](#Overview)
* [Execution](#Execution)

---

## Overview

### *The Assignment*

The Module 11 Challenge centered around applying our understanding of the **K-means algorithm** and **Principal Component Analysis (PCA)** to classify cryptocurrencies according to their price fluctuations across various timeframes.

We were provided the `Crypto_Clustering_starter_code.ipynb` Jupyter Notebook with starter code, and the `crypto_market_data.csv` file, to accomplish our assignment.

### *Written in*

Jupyter Notebook using Python v3.10.13, Pandas, scikit-learn, and hvPlot

### *Accessing the notebook*

To access the crypto clustering notebook, simply download the `.ipynb` file `Crypto_Clustering.ipynb` and the `Resources` folder in this repository into a local directory, then load the `Crypto_Clustering.ipynb` file into Jupyter Notebook through your terminal.

---

## Execution

### *How to use*

Simply `Run All Cells` to execute the code in every cell of the notebook in sequence. Alternatively, each cell may be `Run` on its own, though it is still recommended to run them in order.

### *Breaking down the code*

Below is a more in-depth explanation of the various cells coded within the `Crypto_Clustering.ipynb` notbook.

| Cell (in sequence) | Notes[^2] |
| ---: | :--- |
| 1[^3] | Importing required libraries and dependencies |
| 2[^3] | Reading the provided `.cvs` in as `market_data_df` while setting the index to the `coin_id` column <br> Displaying a sample of the data |
| 3[^3] | Generating a summary of the statistics for `market_data_df` |
| 4 | Declaring the columns from `market_data_df` that will be scaled <br> Declaring `market_data_scaled` and applying the `StandardScalar()` module to normalize the data from the declared columns of `market_data_df` |
| 5 | Declaring `scaled_market_df` as a DataFrame (DF) with the scaled data <br> Adding the `coin_id` column from `market_data_df` to `scaled_market_df` <br> Setting `coin_id` column as index for `scaled_market_df` <br> Displaying a sample of the data |
| 6[^4] | Declaring `k` as a range from 1 to 11 <br> Creating the empty list `inertia` <br> Creating a `for` loop to fit `scaled_market_df` to the `KMeans()` model with `n_clusters=i`, then appending the returned `.inertia_` to the `inertia` list <br> Creating the dictionary `elbow_data` with the data from the `for` loop <br> Creating the DF `df_elbow` from the dictionary `elbow_data` <br> Displaying the data |
| 7 | Plotting `df_elbow` |
| 8[^4] | Initializing the `KMeans()` model as `model` with `n_clusters=4` (as decided by the Elbow Data from `Cell 6`) |
| 9 | Fitting `model` to `scaled_market_df` |
| 10 | Declaring `market_clusters` as the predicted clusters from `scaled_market_df` <br> Displaying the predicted array |
| 11 | Creating a copy of `scaled_market_df` as `scaled_market_predictions` |
| 12 | Adding `MarketCluster` column to `scaled_market_predictions` with `market_clusters` <br> Displaying a sample of the data |
| 13 | Creating a scatter plot of `scaled_market_predictions` using `price_change_percentage_24h` as the x-axis, `price_change_percentage_7d` as the y-axis, and `MarketCluster` as c <br> *Note:* `colormap='rainbow'` *used per instructions, but this might be my new favorite* `colormap=` *option!* |
| 14 | Intializing the `PCA()` model as `pca` with `n_components=3` (as decided by the instructions) |
| 15 | Fitting `pca` to `scaled_market_df` as `market_pca_data` <br> Displaying a sample of the data |
| 16 | Retrieving the explained variance of `pca` |
| 17[^5] | Calculating the total explained variance of the three principal components of `pca` using `sum()` <br> *Note: I did this because I trust the* `sum()` *function more than my dyslexia* |
| 18 | Declaring `market_pca_df` as a DF of `market_pca_data` <br> Adding `coin_id` column to `market_pca_df` with index of `market_data_df` <br> Setting `coin_id` as index for `market_pca_df` <br> Displauing a sample of the data |
| 19[^4] | Declaring `k_pca`[^6] as a range from 1 to 11 <br> Creating the empty list `inertia_pca`[^6] <br> Creating a `for` loop to fit `market_pca_data` to the `KMeans()` model with `n_clusters=i`, then appending the returned `.inertia_` to the `inertia_pca` list <br> Creating the dictionary `pca_elbow_data`[^6] with the data from the `for` loop <br> Creating the DF `df_pca_elbow`[^6] from the dictionary `pca_elbow_data` <br> Displaying the data |
| 20 | Plotting `df_pca_elbow` |
| 21[^4] | Initializing the `KMeans()` model as `pca_model`[^6] with `n_clusters=4` (as decided by the PCA Elbow Data from `Cell 20`) |
| 22 | Fitting `pca_model` to `market_pca_df` |
| 23 | Declaring `pca_clusters` as the predicted clusters from `market_pca_df` <br> Displaying the predicted array |
| 24 | Creating a copy of `market_pca_df` as `market_pca_predicitons_df` <br> Adding `crypto_cluster` column to `market_pca_predicitons_df` with `pca_clusters` <br> Displaying a sample of the data |
| 25[^7] | Creating a scatter plot of `market_pca_predicitons_df` using `hvplot.scatter`, `PCA1` as the x-axis, `PCA2` as the y-axis, and `crypto_cluster` as c <br> *Note: Still using* `colormap='rainbow` *for ease of reading and also because challenge completed coming into June* |
| 26[^7] | Creating a scatter plot of `market_pca_predicitons_df` using `plot.scatter`, `PCA1` as the x-axis, `PCA2` as the y-axis, and `crypto_cluster` as c <br> *Note: Still using* `colormap='rainbow` *for ease of reading and also because challenge completed coming into June* |
| 27 | Declaring `pca_component_weights` as a DF with `pca.components_.T` as values and columns of `market_data_df` as index <br> Displaying the data |
| 28[^5] | Using `describe()` to identify strongest positive and negative influences on each component from `pca` <br> *Note: I did this because I trust the* `describe()` *function more than my dyslexia* |

[^1]: Image courtesy of the free source image site, <a href='https://www.pexels.com/photo/ripple-etehereum-and-bitcoin-and-micro-sdhc-card-844124/' title='Link to Pexels listing for image'>Pexels</a>

[^2]: Markdown cells not annotated

[^3]: Denotes cells with completed code provided, no student coding contained

[^4]: `random_state=1` used wherever applicable to standardize the output

[^5]: Cell added to find values without risk of dyslexic error (as notated in cells of notebook and [Breaking down the code](#Breaking-down-the-code) table)

[^6]: `_pca`, `_pca_`, or `pca_` added to objects to differentiate from previous instances with similar names

[^7]: Conflicting instructions made it unclear as whether to use `plot.scatter` or `hvplot.scatter`, so both methods were used