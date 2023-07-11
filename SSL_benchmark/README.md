# Benchmark for speech self-supervised representations

To run a downstream evaluation for a given SSL model on huggingface you will need to  :
* Change the SSL related values in the run\_benchmark.sh file, specifying the HF hub, the encoder dimension (size of every frame vector), and the number of layers.
* Choose a set of tasks among the ones listed  and for every task a downstream architecture among the existing ones.
* Change the variable defined in run\_benchmark.sh with two lists of equal sized where to every task  in "ConsideredTasks" corresponds in the same index in "Downstreams" the downstream architecture.
* If you want to run two downstream decoders on the same task, just put it twice in the first list with different corresponding decoders below.

If you want to run only on experiment, let us take the example of LibriSpeech using the huggingface model link : mygroup/mySSLModel, that outputs frame vectors of dimension 768 and has 13 internal layers, than you should run : 

```
python LibriSpeech/LSTM/train.py LibriSpeech/LSTM/hparams/ssl.yaml --ssl_hub mygroup/mySSLModel --encoder_dim 768 --num_layers_ssl 13 --output_folder my-output-folder --data_folder mypath/to/LibriSpeech 
``` 
##Tasks and downstream heads

| Task                                     | First Probing Head    | Second Probing Head | Dataset Download                                         |
|------------------------------------------|-----------------------|---------------------|----------------------------------------------------------|
| LibriSpeech ASR                          | BiLSTM                | Conformer           | https://www.openslr.org/12                               |
| Buckeye ASR                              | BiLSTM                | ContextNet          | https://buckeyecorpus.osu.edu/                           |
| CommonVoice Low-Resource  ASR            | BiLSTM                | Linear              | https://commonvoice.mozilla.org/fr                       |
| VoxCeleb1 Automatic Speaker Verification | X-Vectors             | ECAPA-TDNN          | https://www.robots.ox.ac.uk/~vgg/data/voxceleb/vox1.html |
| IEMOCAP Emotion Recognition              | Time-Pooling + Linear | ECAPA-TDNN          | https://sail.usc.edu/iemocap/                            |
| SLURP Intent Classification              | Time-Pooling + Linear | BiLSTM + Linear     | https://zenodo.org/record/4274930                        |

# **Citing**
If you use this benchmark, please cite :

```bibtex
@article{zaiem2023speech,
  title={Speech Self-Supervised Representation Benchmarking: Are We Doing it Right?},
  author={Zaiem, Salah and Kemiche, Youcef and Parcollet, Titouan and Essid, Slim and Ravanelli, Mirco},
  journal={arXiv preprint arXiv:2306.00452},
  year={2023}
}
```
Please, cite SpeechBrain if you use it for your research or business.

```bibtex
@misc{speechbrain,
  title={{SpeechBrain}: A General-Purpose Speech Toolkit},
  author={Mirco Ravanelli and Titouan Parcollet and Peter Plantinga and Aku Rouhe and Samuele Cornell and Loren Lugosch and Cem Subakan and Nauman Dawalatabad and Abdelwahab Heba and Jianyuan Zhong and Ju-Chieh Chou and Sung-Lin Yeh and Szu-Wei Fu and Chien-Feng Liao and Elena Rastorgueva and François Grondin and William Aris and Hwidong Na and Yan Gao and Renato De Mori and Yoshua Bengio},
  year={2021},
  eprint={2106.04624},
  archivePrefix={arXiv},
  primaryClass={eess.AS},
  note={arXiv:2106.04624}
}
```

