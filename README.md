# Speaker Recognition using Vector Quantization
[Speaker recognition](https://en.wikipedia.org/wiki/Speaker_recognition) is the identification of a person from characteristics of voices (voice biometrics). Speaker recognition systems fall into two categories: **text-dependent** and **text-independent**. If the text must be the same for enrollment and verification this is called text-dependent recognition; text-independent systems are most often used for speaker identification as they require very little if any cooperation by the speaker. <br>
Vector Quantization is a text-independent method. Features are extracted using MFCC, and VQ is impelmented by clustering. <br>
The dataset use for this project is [VoxCeleb](http://www.robots.ox.ac.uk/~vgg/data/voxceleb/), which is a large scale audio-visual dataset of human speech. To make the project scalable, it is implemented using [Spark](https://spark.apache.org) (see [Spark SQL and DataFrame](https://spark.apache.org/sql/), [Spark MLlib]https://spark.apache.org/mllib/) for API and library used in this project).

## Feature extracting
- Mel-frequency cepstrum (MFCC)
- See [python_speech_features](https://python-speech-features.readthedocs.io/en/latest/)

## Vector Quantization
The basic idea for VQ is to cluster the features from a speaker to generate some codewords, which consist a codebook. A unknown utter is compared with all the codebooks, with an objective of finding the minimal distortion measure.

- Some terms and how to implement
    - **Codebook**: each category (speaker) has its own codebook, which is a set of codewords
    - **Codeword**: for each speaker, its feature vectors are clustered, and a codeword is the center of a cluster
    - **Pridict an unknown speaker**: compare with each codebook
        - a testing utter <img src="https://latex.codecogs.com/gif.latex?\inline&space;X=\{x_1,&space;x_2,&space;\ldots,&space;x_T\}" title="X=\{x_1, x_2, \ldots, x_T\}" />, a codebook <img src="https://latex.codecogs.com/gif.latex?\inline&space;C=\{c_1,&space;c_2,&space;\ldots,&space;c_M\}" title="C=\{c_1, c_2, \ldots, c_M\}" />
        - the distance between a code vector <img src="https://latex.codecogs.com/gif.latex?\inline&space;{x_i}" title="{x_i}" /> and a codebook <img src="https://latex.codecogs.com/gif.latex?\inline&space;C" title="C" /> is defined as 
          <img src="https://latex.codecogs.com/gif.latex?\inline&space;d(x_i,&space;C)&space;=&space;\min_{c_j\in&space;C}&space;d(x_i,&space;c_j)" title="d(x_i, C) = \min_{c_j\in C} d(x_i, c_j)" />
        - the average distortion is 
          <img src="https://latex.codecogs.com/gif.latex?\inline&space;D(X,&space;C)&space;=&space;\frac{1}{T}\sum_{i=1}^T&space;d(x_i,&space;C)" title="D(X, C) = \frac{1}{T}\sum_{i=1}^T d(x_i, C)" />
- Clustering methods
  - K-means
  - Gaussian Mixture Model (GMM)
  
## Notes on running environment
[Databricks](https://databricks.com) community edition (free) is used.