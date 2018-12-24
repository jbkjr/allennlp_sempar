# AllenNLP for semantic parsing

This repository contains the data, configuration files, and scripts needed to reproduce the following results on the ATIS, GEO, and JOBS semantic parsing datasets, using the AllenNLP framework:

| Model | ATIS | GEO | JOBS |
| --- | --- | --- | --- |
| S2S + attention | 75.2 | 62.5 | 58.6 |
| S2S + attention + ELMo | 79.0 | 71.1 | 74.3 |

Make sure you have [AllenNLP](https://github.com/allenai/allennlp) installed first!

## Training models

To train a model:

```bash
make train
# ... follow the prompts to specify the path to your model config (e.g. experiments/atis/seq2seq.json) and serialization directory.
```

## Prediction and Evaluation

After training, to generate predictions:

```bash
allennlp predict --output-file [FILENAME] --predictor simple_seq2seq [SERIALIZED_MODEL] [INPUT_JSONL]
```

For example, to generate predictions on ATIS for a model that has been serialized to /tmp/models/atis/seq2seq/run_001:

```bash
allennlp predict --output-file predictions/atis/seq2seq.jsonl --predictor simple_seq2seq /tmp/models/atis/seq2seq/run_001/model.tar.gz data/atis/atis_test.jsonl
```

I have already included the predictions in the "predictions" folder for those who simply want to verify the results. Once the predictions have been generated, the accuracy of the model can be calculated against the gold outputs on the test set by following the code in results.ipynb.
