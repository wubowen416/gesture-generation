# gesture-generation

Official implementation for an upcoming workshop paper in ICMI2021.

![A simple sample for wgan on TAKEKUCHI dataset](demo/cl34-dev8.gif)

## To reproduce
1. Clone the repository
2. Download a dataset from https://www.dropbox.com/sh/j419kp4m8hkt9nd/AAC_pIcS1b_WFBqUp5ofBG1Ia?dl=0
3. Download the extracted speech features https://drive.google.com/drive/folders/1BvQYXkQ1aju7KiOIUKsSmzSrj9tZXH2f?usp=sharing
4. Create a directory `./data/takekuchi/source` and put downloaded data into three directories `motion/`, `speech/` and `speeche_features/`, separately.

```
.
data
--takekuchi
   --source
      --motion
      --speech
      --speech_features
```

5. split train, dev, and test, `python datasets/takekuchi/data_processing/prepare_data.py`
6. preprocess dataset `python datasets/takekuchi/data_processing/create_vector.py`
7. train model `python main.py wgan takekuchi hparams/wgan/paper_version.json`
8. Evaluate the model on test set (which was not used during training)
   1. Copy saved model checkpoint path (in `results/log_date/chkpt`) to `Infer: pre_trained` inside `hparams/wgan/paper_version.json`
      ```
      "Infer": {
        "pre_trained": "results/log_20210905_2217/chkpt/generator_232k.pt"
      },
      ```
   2. Execute `python main.py wgan takekuchi hparams/wgan/paper_version.json` to obtain the generated motion and KDE results.

## To visualize
