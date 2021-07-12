# VT-SSum

VT-SSum is a benchmark dataset with spoken language for video transcript segmentation and summarization


## Statistics of VT-SSum
#### Statistics on Train/Val/Test sets of VT-SSum
| Source                        | train    | dev   | test |
|-------------------------------|----------|-------|------|
| Vedio                         | 7,692    | 962   | 962  |


#### Data statistics of VT-SSum in video-level
| Dataset                        | Avg.slides    | Avg.sents   | Avg.words |
|--------------------------------|---------------|-------------|-----------|
| VT-SSum                        | 33.3          | 293.1       | 4,208.1    |

#### Data statistics of VT-SSum in page-level compared with CNN/DM
| Dataset                        | Samples    | Avg.sents   | Avg.words |
|--------------------------------|------------|-------------|-----------|
| VT-SSum                        | 125,004    | 12.7        | 185.9     |
| CNN/DM                         | 311,971    | 38.6        | 690.9     |

## Baselines

### Summarization

Evaluation results on the test data of VT-SSum with models fine-tuned on different datasets

| Models                        | Top3_Precision | Top3_Recall    | Top3_F1        | Top5_Precision | Top5_Recall    |Top5_F1         | 
|-------------------------------|----------------|----------------|----------------|----------------|----------------|----------------|
| CNN/DM                        | 31.49          | 58.41          | 40.92          | 27.10          | 74.46          | 39.74          |
| VT-SSum                       | 37.86          | 69.04          | 48.90          | 29.79          | 80.79          | 43.53          |
| CNN/DM→VT-SSum                | 38.10          | 69.48          | 49.22          | 29.88          | 81.02          | 43.66          |

Evaluation results on the test data of AMI with models fine-tuned on different datasets

| Models                        | Top3_Precision | Top3_Recall    | Top3_F1        | Top5_Precision | Top5_Recall    |Top5_F1         | 
|-------------------------------|----------------|----------------|----------------|----------------|----------------|----------------|
| CNN/DM                        | 45.30          | 59.03          | 51.26          | 39.03          | 72.61          | 50.77          |
| VT-SSum                       | 51.80          | 67.96          | 58.79          | 42.72          | 79.26          | 55.51          |
| CNN/DM→VT-SSum                | 52.66          | 68.72          | 59.62          | 42.99          | 79.78          | 55.87          |


### Segmentation

Evaluation result of the segmentation on the test data of VT-SSum

| Models                        | Accuracy    |
|-------------------------------|-------------|
| LSTM                          | 90.33       |
| UniLMv2<sub>base</sub>        | 92.14       |
| UniLMv2<sub>large</sub>       | 93.00       |


##  Format of the dataset

Each file(*.json) consists of 6 fields:

- `id`: The id of video.
- `title`: The title of the current video.
- `info`: Some information of current video, such as time of published/recorded. 
- `url`: The link to the current video.
- `segmentation`: The segmentation part of the VT-SSum. This field consists of a list:
  ```
    [
        [sent_0 in seg_0, sent_1 in seg_0, ..., sent_n in seg_0],
         ..., 
        [sent_0 in seg_k, sent_1 in seg_0, ..., sent_m in seg_k]
    ]
  ```
  where `k` is the number of segments in the current video, and `n`/`m` is the number of sentences in the segment.
- `summarization`: The summarization part of the VT-SSum. This field consists of a dict:
  ```
    {
        "clip_0":
            {
                "is_summarization_sample": true/false,
                "summarization_data": [
                    {
                        "sent": "sent_0",
                        "label": 0/1,
                    },
                    ...
                    {
                        "sent": "sent_n",
                        "label": 0/1,
                    },
                ]
            }
        ...,
        "clip_k":
            {
                ...
            }
    }
  ```
  where `is_summarization_sample` indicates that the current segment can find the corresponding summary and be used in the training/evaluation of the summarization task. 
  
## Paper
VT-SSum: A Benchmark Dataset for Video Transcript Segmentation and Summarization **[in review]**


