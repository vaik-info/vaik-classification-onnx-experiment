# vaik-classification-onnx-experiment

Create json file by classification model. Calc ACC.


## Install

```shell
pip install -r requirements.txt
```

## Usage

### Create json file

```shell
python inference.py --input_saved_model_path '~/.vaik-classification-pth-trainer/output_model/onnx/model.onnx' \
                --input_classes_path '~/.vaik-mnist-classification-dataset/classes.txt' \
                --input_image_dir_path '~/.vaik-mnist-classification-dataset/valid' \
                --output_json_dir_path '~/.vaik-mnist-classification-dataset/valid_inference'
```

- input_image_dir_path
    - example

```shell
.
├── eight
│   ├── valid_000000024.jpg
│   ├── valid_000000034.jpg
・・・
│   └── valid_000001976.jpg
├── five
│   ├── valid_000000016.jpg
・・・
```

#### Output
- output_json_dir_path
    - example

```json
{
    "answer": "one",
    "image_path": "~/.vaik-mnist-classification-dataset/valid/one/valid_000000000.jpg",
    "label": [
        "one",
        "seven",
        "four",
        "eight",
        "six",
        "nine",
        "three",
        "zero",
        "five",
        "two"
    ],
    "score": [
        0.9999998807907104,
        7.519184208604202e-08,
        4.9287844916534596e-08,
        1.9263076467268547e-08,
        1.518927739141418e-08,
        2.0775094977665276e-09,
        6.83717971128317e-10,
        1.3445242141862934e-10,
        4.8028431925972725e-11,
        1.8028399953462504e-11
    ]
}
```
-----

### Calc ACC

```shell
python calc_acc.py --input_json_dir_path '~/.vaik-mnist-classification-dataset/valid_inference' \
                --input_classes_path '~/.vaik-mnist-classification-dataset/classes.txt'
```

#### Output

``` text
              precision    recall  f1-score   support

        zero     1.0000    0.9851    0.9925       201
         one     0.9957    1.0000    0.9979       234
         two     0.9783    0.9890    0.9836       182
       three     1.0000    0.9913    0.9956       230
        four     1.0000    0.9946    0.9973       185
        five     0.9829    0.9829    0.9829       175
         six     0.9831    0.9777    0.9804       179
       seven     1.0000    0.9958    0.9979       240
       eight     1.0000    0.9784    0.9891       185
        nine     0.9545    1.0000    0.9767       189

    accuracy                         0.9900      2000
   macro avg     0.9895    0.9895    0.9894      2000
weighted avg     0.9902    0.9900    0.9900      2000
```