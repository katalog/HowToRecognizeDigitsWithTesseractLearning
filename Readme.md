# How to recognize digits from images with tesseract + ML.

## Requirements

```
tesseract >= 4.0

tesstrain : https://github.com/tesseract-ocr/tesstrain

python
```

## Training images set
```
images : ground_truth/.png
correct_text : ground_truth/.txt
```
> Image files should be png type.

## checking images set

> Do not reuse images from the training set.

> It needs to use different images from the training set.

## Sample ground truth image, text
Sample image : 36-0001.png

![](./Sample/36-0001.png)

Sample text : 36-0001.gt.txt

36

## Files prep
> bestdata folder and python files are that getting from the tesstrain project.
```
.
├── bestdata
│   ├── eng.traineddata
│   ├── ....
│   ├── script
│   │   ├── Arabic.traineddata
│   │   └── ....
│   └── ...
├── data
│   └── my-model-ground-truth
│       ├── 0-0001.gt.txt
│       ├── 0-0001.png
│       ├── 0-0002.gt.txt
│       ├── 0-0002.png
│       ├── 0-0003.gt.txt
│       ├── 0-0003.png
│       └── ....
├── generate_gt_from_box.py
├── generate_line_box.py
├── generate_line_syllable_box.py
├── generate_wordstr_box.py
├── normalize.py
├── requirements.txt
├── shuffle.py
└── tree.txt
```

## Model making

make training MODEL_NAME=my-model START_MODEL=eng TESSDATA=./bestdata

## How long takes time to make model?

system :  Intel(R) Core(TM) i5-7300HQ CPU @ 2.50GHz

image size : 160x80

image nums : 1000 images

recognize target : signle digit

```
real	9m54,756s
user	29m45,056s
sys	0m31,379s
```

## Output

```
./data/my-model.traineddata
```

copy your traineddata to tesseract tessdata
```
/usr/share/tesseract-ocr/4.00/tessdata/
```

## Test

tesseract 36-1003.png --psm 8 -l my-model

## References

https://stackoverflow.com/questions/43352918/how-do-i-train-tesseract-4-with-image-data-instead-of-a-font-file

https://github.com/tesseract-ocr/tesstrain

https://github.com/tesseract-ocr/tessdata_best

## tesseract help
```
Page segmentation modes:
  0    Orientation and script detection (OSD) only.
  1    Automatic page segmentation with OSD.
  2    Automatic page segmentation, but no OSD, or OCR.
  3    Fully automatic page segmentation, but no OSD. (Default)
  4    Assume a single column of text of variable sizes.
  5    Assume a single uniform block of vertically aligned text.
  6    Assume a single uniform block of text.
  7    Treat the image as a single text line.
  8    Treat the image as a single word.
  9    Treat the image as a single word in a circle.
 10    Treat the image as a single character.
 11    Sparse text. Find as much text as possible in no particular order.
 12    Sparse text with OSD.
 13    Raw line. Treat the image as a single text line,
       bypassing hacks that are Tesseract-specific.

OCR Engine modes: (see https://github.com/tesseract-ocr/tesseract/wiki#linux)
  0    Legacy engine only.
  1    Neural nets LSTM engine only.
  2    Legacy + LSTM engines.
  3    Default, based on what is available.
```

