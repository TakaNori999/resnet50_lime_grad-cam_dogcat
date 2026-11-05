# ResNet50 Dog/Cat Classification with LIME and Grad-CAM

[日本語版 README](README_ja.md)

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/TakaNori999/resnet50_lime_grad-cam_dogcat/blob/main/ResNet50_DogCat_LIME_GradCAM.ipynb)

A **Google Colab notebook** that fine-tunes an ImageNet-pretrained ResNet50 for binary dog/cat classification and visualizes **LIME and Grad-CAM explanations for the same model, input image, and target class**.

**Code only:** The training images, test images, trained model files, and previous execution outputs are **not included**. Users must provide their own images. The output of a newly trained model may differ from figures published elsewhere.

## Quick start

1. Click **Open in Colab** above and sign in to your Google account. Choose a GPU runtime if available.
2. Put your **own** images in Google Drive. The default settings expect **100 cat images and 100 dog images**:

   ```text
   MyDrive/
   └── dog_cat_100images/
       ├── cat/
       │   └── [100 images]
       └── dog/
           └── [100 images]
   ```

   Supported formats: JPG/JPEG, PNG, BMP and WebP. The folder name is merely an example; change `DATA_DIR` in Section 2 if yours differs. To use fewer images for exploration, update `EXPECTED_PER_CLASS` accordingly; this changes the experimental conditions.
3. In **Section 2**, verify `DATA_DIR`, `OUTPUT_ROOT` and the learning settings. Run the notebook from the beginning and authorize Google Drive access for **your own account**.
4. After training, set `TEST_IMAGE_PATH` in **Section 10** to an image in your Drive not used for training or validation. The initial value is blank, so this step is optional until you provide a path. Alternatively, set `TEST_IMAGE_DIR` in Section 11 to choose an image from a dropdown.
5. The original image, positive LIME overlay and Grad-CAM overlay are generated side-by-side and saved to `OUTPUT_ROOT`, along with diagnostic plots, model weights and metadata for **your** session. These are not uploaded to this repository.

## Method overview

| Setting | Default |
| --- | --- |
| Base architecture | ResNet50 (`weights="imagenet"`, `include_top=False`) |
| Head | `original`: Conv2D(1024, 3×3, ReLU) → global average pooling → dropout → Dense(256, ReLU) → dropout → Dense(1) + sigmoid; optional `simple` head |
| Optimization and loss | Adam, binary cross-entropy |
| Training | batch size 32; 2 epochs (head only) + 3 epochs (fine-tune ResNet50 `conv5_` block, BatchNorm frozen) |
| Data split | Stratified 80% train / 20% validation; separate external test image by path |
| LIME | SLIC target ~200 segments; 2,000 perturbations; 20 fitted features, up to 12 displayed positive regions |
| LIME visualization | **Positive coefficients only**: low values remain transparent, higher positive coefficients appear red. Signed coefficients are retained in CSV/NPZ. |
| Grad-CAM | Class-specific logit (dog: `z`; cat: `-z`) and last selected convolutional map. Nonnegative ReLU map shown with a blue→red colormap. |
| Model selection | Lowest validation loss during the fine-tuning stage |

Important: The **numerical magnitudes of LIME coefficients and Grad-CAM maps are not directly comparable**. Visual sharpness alone is not proof of attribution faithfulness. The single validation split is used for model selection, so it is not an independent final test result.

## Reproducibility and limitations

- The original images were obtained from third-party websites; their redistribution rights are not available. No image files are included here.
- The notebook relies on Google Colab/Google Drive, Internet access to retrieve ImageNet weights and install LIME, and the available Colab runtime. Compute resources and library versions can change.
- Original data, model weights, and execution outputs are **not archived in GitHub or Zenodo**; this repository supports reproducing the **workflow**, not the exact trained model or published predictions.
- The notebook uses `lime==0.2.0.1`. Check runtime/package versions saved in its per-run metadata. If numerical reproduction is essential, retain your own environment snapshot, your own data, and your own saved model weights.
- If adapting the code for redistribution, comply with the licenses of any third-party dependencies and any dataset used.

## Files

```text
.
├── README.md
├── README_ja.md
├── LICENSE
├── CITATION.cff
├── requirements.txt
├── .gitignore
├── notebooks/
│   └── ResNet50_DogCat_LIME_GradCAM.ipynb
└── docs/
    └── PUBLISHING_GUIDE_ja.md
```

## License

The code in this repository is provided under the [MIT License](LICENSE). Third-party libraries, pretrained weights downloaded by TensorFlow and users' datasets retain their respective terms. No dataset is licensed or distributed through this repository.

## How to cite

See [CITATION.cff](CITATION.cff) and the **Cite this repository** link displayed by GitHub. Version `v1.0.0` is the planned first release. Once archived through Zenodo, add the **actual** version DOI to this file and the README. **No DOI has been assigned yet.**

Author metadata currently uses the provided GitHub handle **TakaNori999** as a temporary public display name. Before the first DOI release, replace it with the preferred scholarly author name and add coauthors/ORCID identifiers where appropriate.

## GitHub / Zenodo publishing

Instructions in Japanese: [Publishing guide](docs/PUBLISHING_GUIDE_ja.md).
