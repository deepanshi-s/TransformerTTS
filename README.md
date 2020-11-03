## MultiSpeech Implementation

This repo is based on the following papers:
- MultiSpeech: Multi-Speaker Text to Speech with Transformer (https://arxiv.org/pdf/2006.04664.pdf)

The multispeech paper talks about four changes to the transformer model.
-Layer Normalization
-Speaker module
-Bottleneck in decoder prenet
-Diagnol Constraint

I have integrated the first three changes in the transformer git repo. Speaker modules for encoder and decoder have been added in model/layers.py. The phoneme input has been normalized in the SelfAttentionBlocks class of the model/layers.py. The decoder prenet has been changed accordingly in the class defination of DecoderPrenet in model/layers.py. Necessary changes to load and pass the speaker embeddings (x-vectors here) to encoder have been made to the code. 

## 📖 Contents
- [Installation](#installation)
- [Dataset](#dataset)
- [Training](#training)

## Installation

Make sure you have:

* Python >= 3.6

Install espeak as phonemizer backend (for macOS use brew):
```
sudo apt-get install espeak
```

Then install the rest with pip:
```
pip install -r requirements.txt
```


## Dataset
You can directly use [Libritts](https://research.google/tools/datasets/libri-tts/) to create the training dataset.


* **EDIT PATHS**: in `data_config.yaml` edit the paths to point at your dataset and log folders

#### Custom dataset
Prepare a dataset in the following format:
```
|- dataset_folder/
|   |- metadata.csv
|   |- wavs/
|       |- file1.wav
|       |- ...
```
where `metadata.csv` has the following format:
``` wav_file_name|transcription ```

## Training
Change the ```--config``` argument based on the configuration of your choice.
### Create training dataset
```bash
python create_dataset.py --config config/melgan
```
This will add the `mels` and `resampled_wavs` folders to your `train_data_dir`.
### Training
```bash
python train_autoregressive.py --config config/melgan
```

#### Training & Model configuration
- Training and model settings can be configured in `<model>_config.yaml`

#### Resume or restart training
- To resume training simply use the same configuration files
- To restart training, delete the weights and/or the logs from the logs folder with the training flag `--reset_dir` (both) or `--reset_logs`, `--reset_weights`



This Github repo is forked from https://github.com/as-ideas/TransformerTTS.git
Please see the License file for details 
