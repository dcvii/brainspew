---
title: "Federated Learning for Soil Moisture Prediction: Benchmarking Lightweight CNNs and Robustness in Distributed Agricultural IoT Networks"
source: https://www.mdpi.com/2504-4990/7/4/132
author:
published:
created: 2026-01-24
description:
tags:
  - clippings
  - ML
---
---

## 1\. Introduction

Global climate modeling, flood forecasting, drought monitoring, and agricultural yield are all influenced mainly by soil moisture \[[1](https://www.mdpi.com/2504-4990/7/4/#B1-make-07-00132)\]. Accurate estimation of soil moisture supports climate initiatives, improves irrigation management, and reduces water losses \[[1](https://www.mdpi.com/2504-4990/7/4/#B1-make-07-00132)\]. However, although in situ sensors provide high precision, they remain expensive to deploy at scale and offer limited spatial coverage \[[2](https://www.mdpi.com/2504-4990/7/4/#B2-make-07-00132)\]. Therefore, recent advances in machine learning (ML) and remote sensing have enabled data-driven soil moisture forecasting by combining diverse data sources, such as satellite imagery, weather station measurements, and environmental records \[[2](https://www.mdpi.com/2504-4990/7/4/#B2-make-07-00132)\].

At both field and regional scales, integrating soil, crop, and weather data has improved prediction accuracy. For example, combining soil and weather variables improved local soil moisture prediction in the Red River Valley \[[3](https://www.mdpi.com/2504-4990/7/4/#B3-make-07-00132)\]. Similarly, the multimodal MIS-ME framework, which merged weather and imagery data, achieved a mean absolute percentage error (MAPE) of approximately 10.14%, outperforming unimodal baselines \[[4](https://www.mdpi.com/2504-4990/7/4/#B4-make-07-00132)\]. In Egypt, an IoT-based irrigation system was implemented that combined soil moisture sensors and weather forecasts to improve water management \[[5](https://www.mdpi.com/2504-4990/7/4/#B5-make-07-00132)\].

A wide range of ML and deep learning architectures have been applied to soil moisture prediction, including multimodal fusion models that integrate heterogeneous variables \[[2](https://www.mdpi.com/2504-4990/7/4/#B2-make-07-00132),[3](https://www.mdpi.com/2504-4990/7/4/#B3-make-07-00132),[4](https://www.mdpi.com/2504-4990/7/4/#B4-make-07-00132),[6](https://www.mdpi.com/2504-4990/7/4/#B6-make-07-00132),[7](https://www.mdpi.com/2504-4990/7/4/#B7-make-07-00132)\], long short-term memory (LSTM) networks that capture temporal dynamics \[[6](https://www.mdpi.com/2504-4990/7/4/#B6-make-07-00132)\], and convolutional neural networks (CNNs) that extract spatial features from environmental data \[[8](https://www.mdpi.com/2504-4990/7/4/#B8-make-07-00132)\]. Earlier ML-based IoT systems have been developed to monitor soil and environmental parameters, integrating sensor networks with predictive algorithms for crop and fertilizer recommendations \[[9](https://www.mdpi.com/2504-4990/7/4/#B9-make-07-00132)\]. More recently, transformer-based models have shown competitive results for soil and weather time-series forecasting \[[10](https://www.mdpi.com/2504-4990/7/4/#B10-make-07-00132)\]. Physics-informed deep learning methods \[[2](https://www.mdpi.com/2504-4990/7/4/#B2-make-07-00132)\] and knowledge-guided frameworks that couple Sentinel-1 SAR with physical backscatter models \[[11](https://www.mdpi.com/2504-4990/7/4/#B11-make-07-00132)\] also improved generalization under noisy data. Other studies employed active learning \[[12](https://www.mdpi.com/2504-4990/7/4/#B12-make-07-00132)\] to optimize sensor placement and multiscale deep learning \[[13](https://www.mdpi.com/2504-4990/7/4/#B13-make-07-00132)\] to combine satellite and in situ data, achieving regional correlations of $R≈0.90$.

Despite these advancements, most existing models rely on centralized data collection, which is often impractical for distributed agricultural networks due to privacy, ownership, and bandwidth constraints \[[6](https://www.mdpi.com/2504-4990/7/4/#B6-make-07-00132),[8](https://www.mdpi.com/2504-4990/7/4/#B8-make-07-00132),[9](https://www.mdpi.com/2504-4990/7/4/#B9-make-07-00132),[10](https://www.mdpi.com/2504-4990/7/4/#B10-make-07-00132),[14](https://www.mdpi.com/2504-4990/7/4/#B14-make-07-00132),[15](https://www.mdpi.com/2504-4990/7/4/#B15-make-07-00132)\]. Centralized frameworks, such as MIS-ME \[[4](https://www.mdpi.com/2504-4990/7/4/#B4-make-07-00132)\] and multiscale deep learning models \[[13](https://www.mdpi.com/2504-4990/7/4/#B13-make-07-00132)\], achieved strong predictive performance (MAPE = 10.14%, RMSE = 0.034 m <sup>3</sup> /m <sup>3</sup>), yet they required data aggregation on a central server. Similarly, physics-informed and knowledge-guided models \[[2](https://www.mdpi.com/2504-4990/7/4/#B2-make-07-00132),[11](https://www.mdpi.com/2504-4990/7/4/#B11-make-07-00132)\] have improved robustness under certain physical or sensing constraints; however, they were still developed and validated in centralized settings. None of these studies systematically evaluated performance under federated or heterogeneous (non-IID) conditions.

Federated learning (FL) offers a decentralized alternative that enables model training across multiple clients without exchanging raw data. Early studies in agriculture showed FL’s potential for communication-efficient optimization \[[16](https://www.mdpi.com/2504-4990/7/4/#B16-make-07-00132),[17](https://www.mdpi.com/2504-4990/7/4/#B17-make-07-00132)\], IoT-based environmental monitoring \[[18](https://www.mdpi.com/2504-4990/7/4/#B18-make-07-00132)\], and crop yield prediction \[[19](https://www.mdpi.com/2504-4990/7/4/#B19-make-07-00132)\]. However, its application to soil moisture prediction is underexplored.  Previous research has primarily focused on algorithmic enhancements rather than evaluating the application of federated sensor networks for soil moisture prediction \[[7](https://www.mdpi.com/2504-4990/7/4/#B7-make-07-00132)\]. [Figure 1](https://www.mdpi.com/2504-4990/7/4/#fig_body_display_make-07-00132-f001) shows the conceptual framework of federated learning applied to soil moisture prediction. In this setup, multi-source environmental data such as satellite imagery, meteorological records, and in situ sensor measurements are processed locally at each weather station. Only model updates (not raw data) are exchanged using federated averaging, enabling privacy-preserving model training. While such a framework could support broader applications, such as irrigation scheduling, drought monitoring, and flood risk assessment, this study focuses explicitly on soil moisture prediction using distributed weather-station data.

![Make 07 00132 g001](https://www.mdpi.com/make/make-07-00132/article_deploy/html/images/make-07-00132-g001-550.jpg "Make 07 00132 g001")

**Figure 1.** Conceptual framework of federated learning for soil moisture prediction.

This work represents a systematic benchmark of FL for soil moisture prediction in a large-scale IoT environment. It includes robustness evaluation under non-IID and adversarial conditions, a lightweight CNN architecture with approximately 0.8 k parameters optimized for resource-constrained edge devices \[[20](https://www.mdpi.com/2504-4990/7/4/#B20-make-07-00132)\], and a large-scale, reproducible benchmark built on the WHIN sensor network. Experimental results show an efficiency–robustness trade-off, where the lightweight CNN achieved performance comparable to heavier models (approximately 9.4 k parameters) while reducing computational and communication costs. Therefore, the results show that lightweight FL models can achieve high predictive accuracy while remaining practical for real-world IoT deployment.

The rest of this paper is organized as follows: [Section 2](https://www.mdpi.com/2504-4990/7/4/#sec2-make-07-00132) describes the dataset specifications and preprocessing steps. [Section 3](https://www.mdpi.com/2504-4990/7/4/#sec3-make-07-00132) introduces the baseline federated learning models. [Section 4](https://www.mdpi.com/2504-4990/7/4/#sec4-make-07-00132) discusses ablation studies and model selection. [Section 5](https://www.mdpi.com/2504-4990/7/4/#sec5-make-07-00132) compares the performance of centralized and federated models. [Section 6](https://www.mdpi.com/2504-4990/7/4/#sec6-make-07-00132) evaluates robustness under non-IID conditions. [Section 7](https://www.mdpi.com/2504-4990/7/4/#sec7-make-07-00132) presents the final discussion, and [Section 8](https://www.mdpi.com/2504-4990/7/4/#sec8-make-07-00132) concludes the paper, outlining future work.

## 2\. Dataset Specifications and Preprocessing

The dataset used in this study is provided by the Wabash Heartland Innovation Network (WHIN), a digital agriculture Living Laboratory spanning 10 counties in north-central Indiana \[[21](https://www.mdpi.com/2504-4990/7/4/#B21-make-07-00132)\]. WHIN’s sensor network gathers structured, real-time data from over 160 weather stations across its deployment area, making it one of the most densely deployed agricultural weather networks in the US \[[21](https://www.mdpi.com/2504-4990/7/4/#B21-make-07-00132)\]. Geographically, the WHIN network covers approximately 39° to 42° N latitude and −87°to −86° W longitude. The WHIN dataset is freely available to researchers, students, and educators under open-access licensing terms \[[21](https://www.mdpi.com/2504-4990/7/4/#B21-make-07-00132)\]. This dataset comprises measurements from 144 weather stations for May 2020, and is available in both CSV and JSON formats. It can also be accessed programmatically through the WHIN API for automated data retrieval and analysis.

Each weather station records 24 environmental variables every 15 min \[[21](https://www.mdpi.com/2504-4990/7/4/#B21-make-07-00132)\], including air temperature, humidity, barometric pressure, rainfall, solar radiation, wind direction and speed, and soil temperature and moisture at four depths (1–4 inches). In this study, soil moisture at a depth of 4 inches (soil\_moist\_4) is selected as the target variable because it reflects conditions in the root zone that are significant and difficult to measure accurately \[[22](https://www.mdpi.com/2504-4990/7/4/#B22-make-07-00132)\]. Soil moisture (soil\_moist\_4) is measured in centibars (cbar), which represent soil water tension. Higher cbar values indicate drier soil, while lower values correspond to wetter conditions. The observed range of 0–200 cbar is consistent with the calibration of WHIN’s field sensors for typical agricultural soils.

To identify the most relevant input features for (soil\_moist\_4), all variables from each station are aggregated, non-numeric identifiers are removed, and the other soil moisture depth levels are excluded. Feature importance is then estimated locally at each station using a Random Forest surrogate model with permutation importance, a technique known for its robustness to nonlinear relationships and reduced risk of overfitting. The averaged importance scores across all stations are summarized in [Table 1](https://www.mdpi.com/2504-4990/7/4/#table_body_display_make-07-00132-t001). A higher importance value indicates a greater influence of that feature on soil moisture prediction, and the importance scores for all features sum to 1.

**Table 1.** Feature importance across 144 WHIN stations.

![](https://pub.mdpi-res.com/img/table.png)

To prepare the data for model training, each local dataset is divided chronologically into 70% training, 10% validation, and 20% test subsets, ensuring that future timestamps are never used during training. To standardize feature ranges across clients, Min–Max normalization is applied separately for each station, while missing values are imputed using the median. For reproducibility, the same data splits are used across all experiments.

## 3\. Baseline Federated Learning Models

This study evaluates the predictive capability of FL for soil moisture estimation using three baseline models of increasing architectural complexity: Linear Regression (LR), Multilayer Perceptron (MLP), and a lightweight convolutional neural network (CNN). This enables a fair comparison between a traditional regression approach, a simple neural network, and a deep convolutional model under identical FL settings.

The LR model serves as a simple non-deep learning baseline. The MLP architecture comprises two hidden layers with 64 and 32 neurons, respectively, each using ReLU activations, which provides a good trade-off between performance and computational efficiency. The lightweight CNN is designed for low-resource environments and includes a single one-dimensional convolutional layer (kernel size = 1) with ReLU activations, followed by adaptive average pooling and a fully connected regression output. A dropout rate of 0.2 helps prevent overfitting. Depending on the number of hidden channels (8–64), the CNN has between 0.7 k and 3.2 k parameters, making it suitable for deployment on edge devices \[[20](https://www.mdpi.com/2504-4990/7/4/#B20-make-07-00132)\].

Federated training follows the FedAvg algorithm, where a central server aggregates model updates from multiple clients to build a shared global model. To efficiently configure FedAvg, a sensitivity analysis is performed by varying the number of local epochs (2–5) and the client sampling ratio (20–40%). The analysis shows that the mean MAE fluctuation remains below 2%, confirming stable convergence across configurations. Based on these findings, the setup uses 40 clients (approximately 28% of the 144 total) per round and three local epochs to balance predictive accuracy and communication efficiency. Each client trains locally using the Adam optimizer (learning rate = 0.001, batch size = 32), and client updates are weighted according to their sample counts. For reproducibility, deterministic random seeds (seed = 42 + client\_ID) are applied to each client.

After establishing a stable training configuration, the models are statistically compared to determine whether their performance differences are meaningful or due to random variation. The paired Wilcoxon signed-rank test compares MAE values across the 144 weather stations. The test produces the signed-rank statistic (W) and standardized Z-value, which indicates how far the observed difference deviates from the null hypothesis in standard deviation units. The effect size ($r=Z/N$), where $N=144$, quantifies the magnitude of improvement beyond random noise. According to \[[23](https://www.mdpi.com/2504-4990/7/4/#B23-make-07-00132),[24](https://www.mdpi.com/2504-4990/7/4/#B24-make-07-00132)\], r values of 0.1, 0.3, and 0.5 correspond to small, medium, and large effects, respectively; therefore, the values between 0.62 and 0.74 observed in [Table 2](https://www.mdpi.com/2504-4990/7/4/#table_body_display_make-07-00132-t002) represent practically meaningful improvements.

**Table 2.** Wilcoxon signed-rank test results comparing model performance across 144 stations.

![](https://pub.mdpi-res.com/img/table.png)

Furthermore, to ensure that the results are not dependent on a single training run, each experiment is repeated five times with different random seeds. Random number generators are initialized deterministically to ensure reproducibility. Results are reported as mean ± standard deviation (SD), where smaller SD values indicate more consistent performance. Additionally, 95% confidence intervals ($CI95=1.96×σ/n$, with $n=5$) are computed; narrower intervals indicate greater reliability and stability of the model’s performance.

As shown in [Table 3](https://www.mdpi.com/2504-4990/7/4/#table_body_display_make-07-00132-t003), both federated CNN variants outperform the MLP and LR baselines in soil moisture prediction. The lightweight CNN achieves an MAE of 8.07 ± 0.26 cbar, outperforming the MLP (9.68 ± 0.38 cbar) and LR (12.03 ± 0.41 cbar) models. The heavy CNN achieves the best accuracy (7.59 ± 0.28 cbar), but at a higher computational cost. The narrow confidence intervals across CNN variants confirm stable, reproducible performance, indicating that FedAvg aggregation maintains predictive accuracy and robustness under decentralized WHIN network conditions.

**Table 3.** Federated model performance over five independent runs.

![](https://pub.mdpi-res.com/img/table.png)

## 4\. Ablation Studies and Model Selection

Building on the baseline FL experiments, which demonstrate that both lightweight and heavy CNN models outperform LR and MLP in soil moisture prediction, we are now investigating how input features and architectural design influence predictive performance. The baseline results indicate that even minor modifications in architecture or feature representation can significantly impact performance. This observation underscores the need for a systematic ablation analysis to identify optimal configurations for effective FL deployment.

### 4.1. Feature Ablation

The effect of feature selection on model performance is evaluated using Random Forest permutation importance: features are ranked, and models are trained with 1–17 features in order of importance. All MAE and RMSE values are reported in centibars (cbar) for consistency.

As shown in [Table 4](https://www.mdpi.com/2504-4990/7/4/#table_body_display_make-07-00132-t004) and [Figure 2](https://www.mdpi.com/2504-4990/7/4/#fig_body_display_make-07-00132-f002), predictive accuracy improves as more features are included, particularly between 10 and 15 features. Beyond 15 features, performance gains plateau, suggesting diminishing returns and indicating that 14–15 features capture the most informative data for soil moisture prediction. RMSE values remain stable across feature counts, indicating that the model consistently captures the data’s underlying patterns.

![Make 07 00132 g002](https://www.mdpi.com/make/make-07-00132/article_deploy/html/images/make-07-00132-g002-550.jpg "Make 07 00132 g002")

**Figure 2.** Feature ablation of federated CNN models.

**Table 4.** Federated CNN performance with a varying number of features (MAE and RMSE in cbar).

![](https://pub.mdpi-res.com/img/table.png)

### 4.2. Architecture Ablation

Once a nearly optimal feature subset has been identified, the impact of CNN architectural choices, including the number of convolutional layers (1 to 3) and the number of hidden channels (8 to 64), on predictive performance is assessed. All models are trained under identical FL settings to isolate the effect of the architecture.

The results in [Table 5](https://www.mdpi.com/2504-4990/7/4/#table_body_display_make-07-00132-t005) and [Figure 3](https://www.mdpi.com/2504-4990/7/4/#fig_body_display_make-07-00132-f003) show that increasing hidden channels generally improves performance, while adding a third convolutional layer provides moderate gains over two-layer models. Therefore, deeper and wider architectures capture more complex relationships without overfitting, consistent with the improvements observed in the baseline heavy CNN. Together, depth and width adjustments enable the model to explore the distributed data fully.

![Make 07 00132 g003](https://www.mdpi.com/make/make-07-00132/article_deploy/html/images/make-07-00132-g003-550.jpg "Make 07 00132 g003")

**Figure 3.** Effect of convolutional depth and width on federated CNN performance.

**Table 5.** Federated CNN performance with varying hidden channels and convolutional layers (MAE and RMSE in cbar).

![](https://pub.mdpi-res.com/img/table.png)

### 4.3. Combined Ablation Study

Finally, a combined ablation is performed to identify the configuration that optimizes both feature selection and architecture collectively. Models are trained with 2–3 convolutional layers, 16–64 hidden channels, and 10–15 input features (the ranges previously identified as most effective). Efficient training under federated averaging is ensured through early stopping based on validation MAE.

[Figure 4](https://www.mdpi.com/2504-4990/7/4/#fig_body_display_make-07-00132-f004) shows that deeper networks and larger feature sets generally achieve lower MAE. [Table 6](https://www.mdpi.com/2504-4990/7/4/#table_body_display_make-07-00132-t006) confirms that the heavy CNN (64 channels, three layers, 15 features) achieves the lowest MAE (7.86 cbar), while a lightweight CNN (16 channels, three layers, 14 features) reaches nearly the same performance (7.87 cbar) with fewer parameters.

![Make 07 00132 g004](https://www.mdpi.com/make/make-07-00132/article_deploy/html/images/make-07-00132-g004-550.jpg "Make 07 00132 g004")

**Figure 4.** Three-dimensional surface: features × channels vs. test MAE: (**a**) conv. layers = 3; (**b**) conv. layers = 2.

**Table 6.** Model performance with a varying number of features, hidden channels, and convolutional layers (MAE in cbar).

![](https://pub.mdpi-res.com/img/table.png)

## 5\. Centralized vs. Federated Performance

Building on the ablation studies, which identified near-optimal feature sets and CNN architectures, we next compare the performance of federated and centralized training configurations. Both the lightweight and heavy CNN models are evaluated under identical preprocessing and training settings, allowing for a fair assessment of how distributed learning affects predictive accuracy.

[Table 7](https://www.mdpi.com/2504-4990/7/4/#table_body_display_make-07-00132-t007) and [Figure 5](https://www.mdpi.com/2504-4990/7/4/#fig_body_display_make-07-00132-f005) summarize the results, showing that centralized training achieves slightly lower MAE and RMSE values, as it benefits from direct access to the full dataset during optimization. However, federated learning achieves a slight increase of ∼0.5 cbar in MAE, showing that the FedAvg aggregation maintains strong predictive performance even under distributed, heterogeneous data conditions.

![Make 07 00132 g005](https://www.mdpi.com/make/make-07-00132/article_deploy/html/images/make-07-00132-g005-550.jpg "Make 07 00132 g005")

**Figure 5.** Centralized vs. federated performance of lightweight and heavy CNNs.

**Table 7.** Performance comparison of lightweight and heavy CNNs under centralized and federated settings (MAE and RMSE in cbar; mean ± standard deviation and 95% CI across five runs).

![](https://pub.mdpi-res.com/img/table.png)

Notably, the lightweight CNN achieves competitive accuracy compared to the heavy CNN while requiring nearly ten times fewer parameters (0.8 k vs. 9.4 k). This reduction in model size makes it highly suitable for edge deployment, where resource constraints and communication efficiency are critical. The heavy CNN provides marginal gains in accuracy but at a higher computational cost, showing the trade-off between model complexity and practical deployment considerations.

Given these findings, the lightweight CNN is selected for subsequent robustness experiments and stress tests under non-IID data distributions, ensuring that the model is both accurate and deployable in real-world WHIN network environments.

## 6\. Robustness Evaluation Under Non-IID Conditions

Building on the baseline and ablation studies, the efficiency of the selected lightweight CNN is evaluated in heterogeneous and adverse deployment scenarios. While previous experiments identified an optimal configuration (14 input features, 16 hidden channels, three convolutional layers, ∼0.8 k parameters) that achieves near-optimal accuracy (MAE = 7.87 cbar), it is still critical to verify whether this architecture maintains performance under non-IID data distributions and robustness perturbations, which are common in real-world IoT deployments.

Therefore, we designed a robustness evaluation pipeline, shown in [Figure 6](https://www.mdpi.com/2504-4990/7/4/#fig_body_display_make-07-00132-f006), that simulates two types of non-IID scenarios (Dirichlet distribution skew and feature shift) at multiple severity levels. Three classes of robustness perturbations are introduced: label noise, input noise, and Byzantine failures, applied at varying intensities. Specifically, the perturbations are simulated as follows:

![Make 07 00132 g006](https://www.mdpi.com/make/make-07-00132/article_deploy/html/images/make-07-00132-g006-550.jpg "Make 07 00132 g006")

**Figure 6.** Proposed robustness evaluation framework.

- Label noise: 10–30% of local samples have randomly flipped soil moisture labels.
- Input noise: Gaussian noise $N(0,σ2)$ with $σ∈$ 0.01, 0.05, and 0.1 is added to normalized features.
- Byzantine attacks: A subset of clients (5–20%) replaced local model updates with random gradients scaled to match the $ℓ2$ norm of valid updates.

To systematically model heterogeneous client distributions, Dirichlet sampling with concentration parameter $α$ is applied. Low $α$ (0.1) creates highly unbalanced local datasets, while higher $α$ (1.0) approximates near-IID conditions. Across all configurations, the model maintains stable MAE and RMSE under moderate non-IID and up to 20% label corruption, with only minor degradation. Performance decreases at intermediate heterogeneity ($α=0.5$) are attributed to moderate client drift, where label imbalance and feature skew slow down local convergence before FedAvg aggregation stabilizes the global model.

[Table 8](https://www.mdpi.com/2504-4990/7/4/#table_body_display_make-07-00132-t008), [Table 9](https://www.mdpi.com/2504-4990/7/4/#table_body_display_make-07-00132-t009) and [Table 10](https://www.mdpi.com/2504-4990/7/4/#table_body_display_make-07-00132-t010) report detailed results across varying non-IID and robustness settings, while [Figure 7](https://www.mdpi.com/2504-4990/7/4/#fig_body_display_make-07-00132-f007) summarizes the aggregated MAE and RMSE trends.

![Make 07 00132 g007](https://www.mdpi.com/make/make-07-00132/article_deploy/html/images/make-07-00132-g007-550.jpg "Make 07 00132 g007")

**Figure 7.** Federated Learning robustness landscape: (**left**) MAE; (**reght**) RMSE.

**Table 8.** Federated learning experiment results for various non-IID and robustness configurations: Dirichlet severity 0.1 (MAE and RMSE in cbar).

![](https://pub.mdpi-res.com/img/table.png)

**Table 9.** Federated learning experiment results for various non-IID and robustness configurations: Dirichlet severity 0.5 and 1.0 (MAE and RMSE in cbar).

![](https://pub.mdpi-res.com/img/table.png)

**Table 10.** Federated learning experiment results for various non-IID and robustness configurations: feature-shift experiments (MAE and RMSE in cbar).

![](https://pub.mdpi-res.com/img/table.png)

Under mild non-IID and low-noise conditions ($α=1.0$, $σ=0.01$), the lightweight CNN achieves an average MAE of 8.27 cbar. As the severity of non-IID skew or Byzantine participation increases, both MAE and RMSE rise predictably, but no catastrophic failures occur. This indicates that the lightweight architecture maintains convergence stability and robustness, even when facing challenging conditions.

## 7\. Discussion

[Table 11](https://www.mdpi.com/2504-4990/7/4/#table_body_display_make-07-00132-t011) provides a comparative overview of soil moisture prediction studies using machine learning. Most previous works relied on centralized setups and often used satellite or field-scale datasets, while none employed the WHIN sensor network. This study establishes the first quantitative federated baselines on WHIN, contributing to distributed soil moisture modeling.

Compared with previous centralized models \[[2](https://www.mdpi.com/2504-4990/7/4/#B2-make-07-00132),[10](https://www.mdpi.com/2504-4990/7/4/#B10-make-07-00132),[13](https://www.mdpi.com/2504-4990/7/4/#B13-make-07-00132)\], which achieved low RMSE values using complex architectures such as transformers or physics-informed deep learning, the proposed lightweight CNN offers a substantially smaller model footprint (0.8 k parameters) with comparable predictive capability. Despite its simplicity, it achieves near-centralized accuracy (MAE = 7.80 for FL vs. 7.25 centralized) and demonstrates efficiency–accuracy balance, as illustrated in [Figure 8](https://www.mdpi.com/2504-4990/7/4/#fig_body_display_make-07-00132-f008). This supports the feasibility of deploying compact models on edge and IoT devices without sacrificing performance.

![Make 07 00132 g008](https://www.mdpi.com/make/make-07-00132/article_deploy/html/images/make-07-00132-g008-550.jpg "Make 07 00132 g008")

**Figure 8.** Efficiency vs. accuracy trade-off between lightweight and heavy CNNs.

While multimodal or knowledge-guided approaches \[[4](https://www.mdpi.com/2504-4990/7/4/#B4-make-07-00132),[11](https://www.mdpi.com/2504-4990/7/4/#B11-make-07-00132)\] enhance interpretability and performance under specific conditions, they remain limited to centralized frameworks that require unified access to data. In contrast, the proposed federated setup ensures data privacy and scalability across distributed stations, aligning with the real-world constraints of agricultural sensing. Moreover, previous IoT-based systems \[[5](https://www.mdpi.com/2504-4990/7/4/#B5-make-07-00132)\] lacked quantitative evaluation metrics, whereas the present study provides concrete benchmarks based on real sensor data.

An additional strength of this work lies in its robustness evaluation. Previous studies ignored the effects of non-IID distributions, sensor noise, or Byzantine failure conditions that frequently occur in field-deployed networks. The proposed FL framework maintained stable performance under these perturbations, showing minimal degradation across robustness tests. This confirms that the model generalizes well to heterogeneous and imperfect sensing environments.

Overall, the results indicate that lightweight CNNs, when integrated into a federated learning framework, can deliver competitive performance in soil moisture prediction while ensuring data privacy and computational efficiency.

## 8\. Conclusions and Future Work

This work presented the first FL benchmark for soil moisture prediction using the WHIN dataset (144 weather stations). Lightweight (0.8 k) and heavy (9.4 k) CNNs were evaluated under centralized and federated setups, including robustness to noise, non-IID data, and Byzantine failures. Lightweight CNNs nearly performed as well as large CNN models, while being over 10 times smaller, offering strong trade-offs in efficiency and communication. FL achieved near-centralized performance while preserving data privacy and remaining robust under adverse conditions, proving its suitability for distributed agricultural sensing. Notably, all baselines were evaluated under reproducible settings, providing a reliable benchmark for future research. Future work will explore communication-efficient FL (such as compression, partial participation), enhanced robustness (such as differential privacy, resilient aggregation), and deployment on live WHIN infrastructure. Extending to multi-season, multi-region data will further validate generalizability. This work demonstrates that FL with compact models is both effective and practical for scalable, privacy-aware agricultural monitoring.