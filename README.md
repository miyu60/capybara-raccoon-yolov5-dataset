# Capybara and raccoon YOLOv5 detection dataset

This repository contains the detection-ready version of the user's Roboflow export `Capybara Raccoon Detection.v1.zip`.

## Structure

```text
data.yaml
train/images/  (40 JPEGs)
train/labels/  (40 YOLO text files)
valid/images/  (5 JPEGs)
valid/labels/  (5 YOLO text files)
test/images/   (5 JPEGs)
test/labels/   (5 YOLO text files)
```

`data.yaml` preserves the source class order: `0: capybara`, `1: raccoon`. It uses paths relative to the YAML file. Supply the absolute path to this `data.yaml` when training with YOLOv5.

## Preparation from the supplied export

The source labels contained 97 polygon annotations and 4 bounding boxes. Each polygon was converted to its enclosing axis-aligned bounding box using the minimum and maximum normalized x and y coordinates. Existing bounding boxes were retained. The images, train/valid/test assignments, class IDs, and the number of annotated objects were preserved.

After conversion, all 101 annotation lines have the YOLO detection format `class_id x_center y_center width height`, with normalized coordinates. The image/label pair counts and annotation ranges were checked for every split.

The `roboflow` metadata in `data.yaml`, including `license: Private`, is retained from the original export for provenance. Repository visibility does not change the dataset's licensing terms.

## Upload to GitHub (the Lab workflow)

1. Sign in at GitHub, select **New repository**, enter `capybara-raccoon-yolov5-dataset`, choose **Public**, select **Add a README file**, then select **Create repository**.
2. In the repository, select **Add file > Upload files**. Upload `data.yaml` to the repository root.
3. Open or create `train/images`, `train/labels`, `valid/images`, `valid/labels`, `test/images`, and `test/labels`. Use **Add file > Upload files** inside each matching directory and select its image or label files. Commit each batch to `main`.
4. Confirm that every image has a `.txt` file with the same stem in the matching `labels` directory. Do not upload only the original ZIP; YOLOv5 needs the extracted directory tree.
5. Large individual files above GitHub's normal file limit require Git LFS or external dataset storage. This dataset's largest file is below 100 KB, so standard GitHub files are sufficient.

For Google Colab, clone this repository under `/content`, then pass the absolute path to its `data.yaml` or create a run-specific YAML inside `yolov5/data` as shown in `Capybara_Raccoon_YOLOv5_Lab.ipynb`.
