# Speaker Recognition using Vector Quantization

## Feature extracting
- MFCC

## Vector Quantization
- Some terms and how to implement
    - **Codebook**: each category (speaker) has its own codebook, which is a set of codewords
    - **Codeword**: for each speaker, its feature vectors are clustered, and a codeword is the center of a cluster
    - **Pridict an unknown speaker**: compare with each codebook
        - a testing utter <img src="https://latex.codecogs.com/gif.latex?X={x_1, x_2, \ldots, x_T}"/>, a codebook <img src="https://latex.codecogs.com/gif.latex?C={c_1, c_2, \ldots, c_M}" />
        - the distance between a code vector x and a codebook is defined as 
          <img src="https://latex.codecogs.com/gif.latex?d(x_i, C) = \min_{c_j} d(x_i, c_j)"/>
        - the average distortion of X and C is
          <img src="https://latex.codecogs.com/gif.latex?D(X, C) = \frac{1}{T}\sum_{i=1}^T d(x_i, C)"/>
- Clustering methods
  - **K-means**
  - Gaussian Mixture Model (GMM)