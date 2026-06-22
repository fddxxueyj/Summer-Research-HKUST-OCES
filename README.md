# Summer-Research-HKUST-OCES

## 1. Offline learning

### 1.1 Hyperparamters
The model is constructed based on the library `NeuralOperator`. The key hyperparamter when training on this dataset is truncated mode, which equals to 48. The dimension of the input 2D data is 64*64, so this truncated mode allows the model to learn the high-wavenumber information in the subgrid terms. The spectra of the trained Fourier layers also prove this point, where the weight of the high wavenumbers is the largest in the first Fourier layer. 

![alt text](https://raw.githubusercontent.com/fddxxueyj/Summer-Research-HKUST-OCES/main/results/spectral_weights.png)

## 1.2 Offline testing

