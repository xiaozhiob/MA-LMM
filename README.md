# (2024CVPR) MA-LMM: Memory-Augmented Large Multimodal Model for Long-Term Video Understanding
### [Project Page](https://boheumd.github.io/MA-LMM/) | [Paper](https://arxiv.org/abs/)
The official repository of our paper "**MA-LMM: Memory-Augmented Large Multimodal Model for Long-Term Video Understanding**".

<p align="center">
<img src="figs/teaser.png" alt="teaser" width="60%">
</p>


## Model Overview
<p align="center">
<img src="figs/architecture.png" alt="model" width="80%">
</p>

## Requirements

You can install the conda environment by running:
```bash
git clone https://github.com/boheumd/MA-LMM.git
cd MA-LMM
pip install -e .
```

## Dataset
For the long-term video understanding task, we conduct experiments including ([LVU](https://github.com/chaoyuaw/lvu)) and two standard video summarization datasets ([Breakfast](https://serre-lab.clps.brown.edu/resource/breakfast-actions-dataset/), [COIN](https://coin-dataset.github.io/)).
For the video question answering task, we conduct experiments including [MSRVTT](https://github.com/xudejing/video-question-answering), [MSVD](https://github.com/xudejing/video-question-answering), and [ActivityNet](https://github.com/MILVLG/activitynet-qa).
For the video captioning task, we also conduct experiments on [Youcook2](http://youcook2.eecs.umich.edu/) dataset.

You can download videos for each dataset through the script provided here (lavis/datasets/download_scripts).
Then extract video frames of each video with fps=10.
   ```
    ├── data
        └── activitynet
            ├── annotation
            ├── frames
            ├── videos
        └── breakfast
            ├── annotation
            ├── frames
            ├── videos
        └── coin
            ├── annotation
            ├── frames
            ├── videos
        └── lvu
            ├── annotation
            ├── frames
            ├── videos
        └── msrvtt
            ├── annotation
            ├── frames
            ├── videos
        └── msvd
            ├── annotation
            ├── frames
            ├── videos
        └── youcook2
            ├── annotation
            ├── frames
            ├── videos
   ```



## Running

### Download Pre-trained LLM
We use Vicuna-v1.1 as our pre-trained LLM weights, you can download from this [link](https://github.com/lm-sys/FastChat/blob/main/docs/vicuna_weights_version.md) as arrange in this format.
   ```
   ├── llm
        ├── vicuna-7b
        ├── vicuna-13b
   ```
### Training
We train the model on 4 A100 GPUs. To train the model on different dataset, please execute the following command:
```bash
bash run_scripts/${dataset}/train.sh
```

#### LVU dataset
```bash
    # Please choose the task from the list
    # ['director', 'genre', 'relationship', 'scene', 'way_speaking', 'writer', 'year']
    datasets.lvu_cls.task ${task}
```

### Testing
First, download the [saved_model.tar](https://drive.google.com/file/d/1mq6fg69Ofm32-1HjEunoFtPg8ymAIcOp/view?usp=sharing) and unzip it. 
Then for the test script of each dataset, pass the checkpoint path to run.resume_ckpt_path to run the evaluation.
```bash
bash run_scripts/${dataset}/test.sh
```

### Hyper-parameters
One important hyper-parameters memory_bank_length, please change that in the training script on different datasets.
```bash
    # pre-defined length of the memory bank
    model.memory_bank_length ${value}
    # value=0 means without using the memory bank
```


## Citation
If you find our code or our paper useful for your research, please **[★star]** this repo and **[cite]** the following paper:

```latex
@inproceedings{he2024malmm,
  title = {MA-LMM: Memory-Augmented Large Multimodal Model for Long-Term Video Understanding},
  author    = {He, Bo and Li, Hengduo and Jang, Young Kyun and Jia, Menglin and Cao, Xuefei and Shah, Ashish and Shrivastava, Abhinav and Ser-Nam, Lim},
  booktitle = {Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition (CVPR)},
  year = {2024}
}
```


## Acknowledgement
We referenced the repo below for the code
- [LAVIS](https://github.com/salesforce/LAVIS)



