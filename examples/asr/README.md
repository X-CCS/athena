# Examples for ASR Tasks

Currently supported ASR tasks are HKUST and AISHELL. An example script for Librispeech will be released shortly. To perform the full procedure of ASR experiments, simply run:
```bash
source env.sh
bash examples/asr/$task_name/run.sh
```

## A complete run contains following stages:

1) Data preparation: Before you run `examples/asr/$task_name/run.sh`, you should download the coorsponding dataset and store it in `/nfs/project/datasets/opensource_data/$task_name`. The script `examples/asr/$task_name/local/prepare_data.py` would generate the desired csv file decripting the dataset

2) Data normalization: With the generated csv file, we should compute the cmvn file firstly like this `python athena/cmvn_main.py examples/asr/$task_name/configs/mpc.json examples/asr/$task_name/data/all.csv`

3) Unsupervised pretraining: You can perform the unsupervised pretraining using the json file `examples/asr/$task_name/mpc.json` or just skip this

4) Acoustic model training: You can train a transformer model using json file `examples/asr/$task_name/configs/transformer.json` or train a mtl_transformer_ctc model using json file `examples/asr/$task_name/configs/mtl_transformer.json`

5) Language model training: You can train a rnnlm model using the transcripts with the json file `examples/asr/$task_name/rnnlm.json`, of course, you should firstly prepare the csv file for it

6) Decoding: Currently, we provide a simple but not so effective way for decoding mtl_transformer_ctc model. To use it, run `python athena/decode_main.py examples/asr/$task_name/configs/mtl_transformer.json`

## Results for ASR Tasks

| Error Rate (CER for Mandarin, WER for English)  |  without MPC/%     |     with MPC/%   |
| :-------------: | :----------: | :-----------: |
|  HKUST          | 23.30        | 22.98         |
| AISEHLL         | 5.97         | 5.77          |
| Librispeech     |              |               |
| switchboard_fisher |           |               |

