# Interspeech-2025: 
# Step 1 Data Download/ Prepare
 ## Install transformers library:
```pip install transformers ```
### Download data from huggingface and store into 
 - dev
   - transcripts
   - wav
 - train
   - transcripts
   - wav
 ```
python download_hugg_data.py --path "mostafaashahin/common_voice_Arabic_12.0_Augmented_SWS_lam_phoneme" --split "train" --output_dir "./data"
python download_hugg_data.py --path "mostafaashahin/common_voice_Arabic_12.0_Augmented_SWS_lam_phoneme" --split "dev" --output_dir "./data"

```
## Install s3prl toolkit
```
conda create -n s3prl python=3.8 \
conda activate s3prl \
git clone https://github.com/s3prl/s3prl.git \
cd s3prl \
pip install -e ".[all]"
```
