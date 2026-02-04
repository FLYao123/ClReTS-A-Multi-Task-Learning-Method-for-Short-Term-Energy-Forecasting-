×××××××× A Multi-Task Learning Method for Short-Term Energy Forecasting with Interpretable Trend–Deviation Decomposition ××××××××


📖 Introduction

This repository contains the official implementation of the manuscript (submitted): "A Multi-Task Learning Method for Short-Term Energy Forecasting with Interpretable Trend–Deviation Decomposition".

We propose ClReTS (also called CaReTS), a novel multi-task learning framework for short-term energy time series forecasting. The framework jointly models classification and regression tasks through a dual-stream architecture:

1) Classification branch: captures step-wise future trends;

2) Regression branch: estimates deviations from the latest target observation.

This design disentangles macro-level trends and micro-level deviations, resulting in more interpretable predictions. To achieve effective joint learning, we introduce a multi-task loss with uncertainty-aware weighting, balancing the contributions of different tasks adaptively. Four model variants (ClReTS1–4) are developed under this framework, supporting mainstream temporal modeling encoders: CNNs, LSTMs, and Transformers. Experiments on multiple real-world datasets demonstrate that ClReTS outperforms SOTA algorithms in forecasting accuracy and trend classification.

📊 Datasets

Publicly available datasets used in this work can be accessed here: 👉  [FLYao123] https://github.com/FLYao123/District-microgrid-dataset & https://github.com/FLYao123/A_Self-organizing_Interval_Type-2_Fuzzy_Neural_Network

To ensure reproducibility, the preprocessed data is also provided in the Data-Prepro folder.

💻 Code Structure

This repository provides: ClReTS1–4 (our proposed models, also called CaReTS1–4 ) and Baseline1–3 (newly designed baselines). Each model has its own file. 📢 Please update your own paths in the scripts before running.

Code outputs include: 1) N-fold cross-validation results; 2) Performance on train/validation/test sets.

Evaluation metrics: MSE, RMSE, trend accuracy, and average runtime per fold.

⚙️ Usage

1. Encoder Setup

The encoder can be implemented as LSTM, CNN, or Transformer. To switch between them, e.g., modify:

    Class RegressionDualBranchModel(nn.Module):
        def __init__(self, input_dim=1, hidden_dim=64, num_layers=2, output_len=6, model_type='LSTM'):# Change to "CNN" or "TRANSFORMER"
        ...

2. Dataset Setup

The dataset can be set to unmet power or electricity price. For example, to switch to the electricity price dataset, modify:

    def load_data_new:
        ...
        X_data_train = pd.read_csv('/content/drive/MyDrive/CaReTS/unmets_HWM_train.csv') # Change to "prs_HWM_train.csv"
        X_data_test = pd.read_csv('/content/drive/MyDrive/CaReTS/unmets_HWM_test.csv')# Change to "prs_HWM_train.csv"
        ...


3. Input/Output Setup

By default, the forecasting mode is 15-input-6-output. To change input-output ratio: adjust settings when loading the training and test sets in load_data_new method. If you modify the output length, please remember to also update the output_len parameter in RegressionDualBranchModel(nn.Module), for example::
    
    Class RegressionDualBranchModel(nn.Module):
        def __init__(self, input_dim=1, hidden_dim=64, num_layers=2, output_len=6, model_type='LSTM'):# Change '6' to '4' or '8'
        ...
During training, the model automatically detects the input length, so no further modification is required.

🔗 References & Acknowledgements

We thank the following contributors for making their codes available:

1) SOTA baselines (8 models: Autoformer, FEDformer, Non-stationary, TimesNet, Dlinear, Nlinear, TimeXer, TimeMixer) 👉 [wuhaixu2016]  https://github.com/thuml/Time-Series-Library


2) SOTA baselines (2 models: SOIT2FNN-MO, D-CNN-LSTM) 👉 [FLYao123] https://github.com/FLYao123/A_Self-organizing_Interval_Type-2_Fuzzy_Neural_Network

3) We also express our sincere appreciation to the authors of these 10 algorithms. 🙏

Note: In earlier versions of our work, the method was referred to as CaReTS. In this repository, ClReTS and CaReTS are used interchangeably and refer to the same approach.
