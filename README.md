# ChromaFeatures_CoverID

Set of functions and methods to compute various chroma and audio similarity measures particularly for the task of cover song identification.

It also includes the python implementation of cover song similarity measures as mentioned in the following papers.

* Serra, J., Serra, X., & Andrzejak, R. G. (2009). Cross recurrence quantification for cover song identification. New Journal of Physics.

* Chen, N., Li, W., & Xiao, H. (2017). Fusing similarity functions for cover song identification. Multimedia Tools and Applications.


## Dependencies

[TO DO SOON] : Add docker file with all the dependencies

All dependencies except Essentia can be installed via pip

```bash
$ pip install -r requirements.txt
```

For installing essentia check the documentation or you can easily set it up using the official 
(Essentia docker image)[https://github.com/MTG/essentia-docker].



## Usage examples

* For feature extraction using [chroma_features.py]

```python
from chroma_features import ChromaFeatures

audio_path = "./test_audio.wav"

#Initiate the chroma class
chroma = ChromaFeatures(audio_file=audio_path, mono=True, sample_rate=44100)

# Now you can compute various chroma features and ther plots using the various methods of object chroma
chroma.chroma_stft()
chroma.chroma_cqt()

#You can specify custom params
chroma.chroma_hpcp(hopSize=2048, numBins=24)
chroma.chroma_cens(hopSize=1024)

```

* Computing cover song similarity measures (qmax and dmax)

```python
from chroma_features import ChromaFeatures
import similarity_measures as similarity

chroma1 = ChromaFeatures('<path_to_query_audio_file>')
chroma2 = ChromaFeatures('<path_to_reference_audio_file>')
hpcp1 = chroma1.chroma_hpcp()
hpcp2 = chroma2.chroma_hpcp()

#similarity matrix
sims = similarity.RecurrentPlots()
cross_recurrent_plot = sims.cross_recurrent_plot(hpcp1, hpcp2)
#plot
sims.plot_crp(cross_recurrent_plot, cmap='hot')

#cover song similarity distance
qmax = sims.qmax_measure(cross_recurrent_plot)
dmax = sims.dmax_measure(cross_recurrent_plot)

```

For more detailed examples have a look on the ipython [notebook](examples.ipynb)



## Contribution

