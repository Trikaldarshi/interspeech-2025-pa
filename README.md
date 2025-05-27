# Interspeech-2025: 
# Step 1 Data Download/ Prepare
 ## Install transformers library:
```pip install transformers ```
### Download CV-Ar data from huggingface and store into 
 - dev
   - transcripts
   - wav
 - train
   - transcripts
   - wav
 ```
python download_hugg_data.py --path "mostafaashahin/common_voice_Arabic_12.0_Augmented_SWS_lam_phoneme" --split "train" --output_dir "./sws_data/CV-Ar"
python download_hugg_data.py --path "mostafaashahin/common_voice_Arabic_12.0_Augmented_SWS_lam_phoneme" --split "dev" --output_dir "./sws_data/CV-Ar"

```
### Download Arabic TTS data described in the paper from huggingface and store into 
 - dev
   - transcripts
   - wav
 - train
   - transcripts
   - wav
```
python download_hugg_data_tts.py --path "mostafaashahin/SWS_TTS_v0.2" --split "train" --output_dir "./data/TTS" --dev_name "Amer"
```
## Install s3prl toolkit
```
conda create -n s3prl python=3.8 \
conda activate s3prl \
git clone https://github.com/s3prl/s3prl.git \
cd s3prl \
pip install -e ".[all]"
```
In this work, the downstream task located in the [s3prl/s3prl/downstream/ctc](https://github.com/s3prl/s3prl/tree/main/s3prl/downstream/ctc) is used to train a ctc based phoneme recognition system.

# Step 2 Data setup for [s3prl/s3prl/downstream/ctc](https://github.com/s3prl/s3prl/tree/main/s3prl/downstream/ctc)

a.) 
Navigate to [s3prl/s3prl/preprocess](https://github.com/s3prl/s3prl/tree/main/s3prl/preprocess) and move  ``` generate_len_for_bucket_sdaia.py ``` there and run:

``` python generate_len_for_bucket_sdaia.py -i path_to_downloaded_data/sws_data/CV-Ar -o ../data/CV-Ar/```

This will generate sorted files inside ```s3prl/s3prl/data/CV-Ar/len_for_bucket/train.csv``` and ```s3prl/s3prl/data/CV-Ar/len_for_bucket/dev.csv```

b.) 
Navigate to [s3prl/s3prl](https://github.com/s3prl/s3prl/tree/main/s3prl/) and move  ``` csv_to_tsv_with_transcripts.py ``` there and run:

```
python csv_to_tsv_with_transcripts.py --csv_path data/CV-Ar/train.csv --transcript_root "./sws_data/CV-Ar/" --output_path "./sws_data/CV-Ar/train/train.tsv
python csv_to_tsv_with_transcripts.py --csv_path data/CV-Ar/dev.csv --transcript_root "./sws_data/CV-Ar/" --output_path "./sws_data/CV-Ar/dev/dev.tsv
```


