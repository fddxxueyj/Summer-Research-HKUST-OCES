# FNO-in-eddy-parameterization

## 1. Offline learning

### 1.1 Hyperparamters

The model is constructed based on the library `NeuralOperator`. The key hyperparamter when training on this dataset is truncated mode, which equals to 48. The dimension of the input 2D data is 64*64, so this truncated mode allows the model to learn the high-wavenumber information in the subgrid terms. The spectra of the trained Fourier layers also prove this point, where the weight of the high wavenumbers is the largest in the first Fourier layer. 

![alt text](https://raw.githubusercontent.com/fddxxueyj/Summer-Research-HKUST-OCES/main/results/spectral_weights.png)

## 1.2 Training Stretagy

The first 295 runs are chosen as the training dataset and the last 5 runs are the testing dataset. We only use the numerical results after 3-years iteration in order to ensure the flow fully develops into eddy state. The experiments have shown that if the data in the developing state are contained in the training set, the FNO cannot be trained, which is quit different from training CNN. The approach is similar to Victor Mangeleer's work, where `'Sampling begins after the system has achieved a quasi-steady state solution, which takes 4 years for eddy-driven flows and 6 years for jet-driven flows.'` 

## 1.3 Offline Testing

Two metrics are chosen, pearson correlation and the coefficient of determination $R^2$. The examples demonstrate that the offline results look fine, better than the results reproted in Victor Mangeleer's work, where $R^2$ is always lower than 0.5. The results also look slightly better than the CNNs if they are trained on the same datasets. 

![alt text](https://raw.githubusercontent.com/fddxxueyj/Summer-Research-HKUST-OCES/main/results/20260621v1_layer0_plot.png)

## 1.4 Online Testing

We first conducted online tests using only three different initial conditions in the testset, with each simulation integrated for 10 years. 

![alt text](https://raw.githubusercontent.com/fddxxueyj/Summer-Research-HKUST-OCES/main/results/comparison_layer0.gif)

The results indicate that all three runs remained numerically stable throughout the entire integration period. The evolution of the correlation coefficient with respect to the reference numerical simulation closely resembles the behavior reported in Feier's paper. For long-term statistical properties, the PDF of the PVs obtained from the FNO simulations is in good agreement with that of the numerical model. This result appears to be superior to that reported for CNN-based approaches although the size of the ensemble is still small. This may imply that FNO can better preserves PV conservation. 

![alt text](https://raw.githubusercontent.com/fddxxueyj/Summer-Research-HKUST-OCES/main/results/pdf.png)

