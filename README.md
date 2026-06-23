# FNO-in-eddy-parameterization

## 1. Offline learning

### 1.1 Hyperparamters

The model is implemented using the `NeuralOperator` library. A key hyperparameter for this dataset is the truncation mode, which is set to 48. Given that the input data have a spatial resolution of $64 \times 64$, this relatively large truncation mode enables the model to capture high-wavenumber information associated with the subgrid-scale terms. This setting is further supported by the spectra of the trained Fourier layers. In particular, the first Fourier layer assigns the largest weights to the high-wavenumber modes.

![alt text](https://raw.githubusercontent.com/fddxxueyj/Summer-Research-HKUST-OCES/main/results/spectral_weights.png)

## 1.2 Training Stretagy

The first 295 runs in `train.nc` are used for training, while the remaining 5 runs are reserved for testing. To ensure that the flow has fully developed into a eddy state, only the model outputs obtained after about three years (snapshot 20) of integration are included in the dataset. Experiments indicate that including samples from the spin-up phase (snapshots 1–19) significantly degrades the training process. In this case, the model predictions are underestimated, with amplitudes on the order of $10^{-2}-10^{-3}$ relative to the ground truth. This behavior differs markedly from that observed for CNNs, which seem to be less sensitive to the presence of transient-state data. The approach adopted here is similar to Victor Mangeleer's work, where `'Sampling begins after the system has achieved a quasi-steady state solution, which takes 4 years for eddy-driven flows and 6 years for jet-driven flows.'` 

## 1.3 Offline Testing

Two metrics are chosen, pearson correlation and the coefficient of determination $R^2$. The examples demonstrate that the offline results look fine, better than the results reproted in Victor Mangeleer's work, where the $R^2$ for FNO predictions is always lower than 0.5. The results also look slightly better than the CNNs if they are trained on the same datasets. 

![alt text](https://raw.githubusercontent.com/fddxxueyj/Summer-Research-HKUST-OCES/main/results/20260621v1_layer0_plot.png)

## 1.4 Online Testing

We first conducted online tests using only three different initial conditions in the testset, with each simulation integrated for 10 years. 

![alt text](https://raw.githubusercontent.com/fddxxueyj/Summer-Research-HKUST-OCES/main/results/comparison_layer0.gif)

The results indicate that all three runs remained numerically stable throughout the entire integration period. The evolution of the correlation coefficient with respect to the reference numerical simulation closely resembles the behavior reported in Feier's paper. For long-term statistical properties, the PDF of the PVs obtained from the FNO simulations is in good agreement with that of the numerical model. This result appears to be superior to that reported for CNN-based approaches although the size of the ensemble is still small. This may imply that FNO can better preserves PV conservation. 

![alt text](https://raw.githubusercontent.com/fddxxueyj/Summer-Research-HKUST-OCES/main/results/pdf.png)

