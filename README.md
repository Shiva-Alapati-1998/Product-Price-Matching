# Product-Matching





<!-- TABLE OF CONTENTS -->
<details open="open">
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
      <ul>
        <li><a href="#built-with">Built With</a></li>
      </ul>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
      </ul>
    </li>
    <li><a href="#data-description">Data Description</a></li>
    <li><a href="#files">Files</a></li>
    <li><a href="#Pre-Processing">Pre-Processing</a></li>
    <li><a href="#Results">Results</a></li>
    <li><a href="#future-work">Future Work</a></li>
    <li><a href="#license">License</a></li>
    <li><a href="#contact">Contact</a></li>
    <li><a href="#acknowledgements">Acknowledgements</a></li>
  </ol>
</details>



<!-- ABOUT THE PROJECT -->
## About The Project

Product matching on shopee dataset (Kaggle Competition)
In the modern era, customers can buy products from hundreds of e-commerce
websites. However customers find it hard to get the similar items with good quality
and cheaper price because these items are listed at multiple websites for different
prices. Leading e-commerce companies are always in search of building robust AI
technology to make their customers comfortable in searching the products and
attract the customers to buy their products at rates competitive to sold by other
retailers in the market.

Here we present deep learning approach based on Holistically-Nested Edge Detec-
tion (HED), EfficientNet-B3 (EffNet-B3), Bidirectional Encoder Representations

from Transformers (BERT), Normalizer-Free Networks (NFNet), Vision Trans-
former (ViT), and Term Frequency–Inverse Document Frequency (TF-IDF) to find

images and text embeddings. During model execution for a particular image, we
use KNN to get the top 50 similar products based on the embeddings which can be
used to compare the price of a product.

### Built With

* Python
* Pytorch
* Hugging Face



<!-- GETTING STARTED -->
## Getting Started

This is an example of how you may give instructions on setting up your project locally.
To get a local copy up and running follow these simple example steps.

### Prerequisites

Kaggle Shopee - Price Match Guarantee Dataset

### Data Description

Finding near-duplicates in large datasets is an important problem for many online businesses. In Shopee's case, everyday users can upload their own images and write their own product descriptions, adding an extra layer of challenge. Your task is to identify which products have been posted repeatedly. The differences between related products may be subtle while photos of identical products may be wildly different!

As this is a code competition, only the first few rows/images of the test set are published; the remainder are only available to your notebook when it is submitted. Expect to find roughly 70,000 images in the hidden test set. The few test rows and images that are provided are intended to illustrate the hidden test set format and folder structure.

### Files
[train/test].csv - the training set metadata. Each row contains the data for a single posting. Multiple postings might have the exact same image ID, but with different titles or vice versa.

posting_id - the ID code for the posting.

image - the image id/md5sum.

image_phash - a perceptual hash of the image.

title - the product description for the posting.

label_group - ID code for all postings that map to the same product. Not provided for the test set.

[train/test]images - the images associated with the postings.

sample_submission.csv - a sample submission file in the correct format.

posting_id - the ID code for the posting.

matches - Space delimited list of all posting IDs that match this posting. Posts always self-match. Group sizes were capped at 50, so there's no need to predict more than 50 matches.


## Pre-Processing
There were a couple of image pre-processing techniques experimented with in order to try and
improve our models performance during testing. Both of these methods incorporated using the HED to produce high detail contours of the images, which was then used to determine which contours contained the most essential details of the image.

Initially, the largest contour based on contour area was chosen as the most relevant area of the image
to keep. However after further evaluation, it was shown this didn’t perform well in masking off
enough of the irrelevant features within an image. Therefore a different approach was taken, where
the smallest-to-largest of the contours generated were kept in the image until the total contour area
reached that of the total image area. Since the smallest contours in the image can be children of
surrounding contours when using a contour hierarchy, there will be overlapping contour areas in the
image. The more complex the image is, the less of the overall image will be preserved an the more
individual features will be kept, since they will contain more overlapping contour areas. Therefore, a
total contour area that is equivalent to the image area is different than preserving the entire image.
This method proved to provide the best results in keeping many of the relevant features from an
image and masking off some of the irrelevant ones.
<!-- USAGE EXAMPLES -->
## Results

An ensemble model using NFNet for the image embeddings and EffNet-B3 with BERT for the text
embeddings, achieved an F-1 score of 0.733 when used against the test dataset. This was the best
score out of all of our models. Whereas an ensemble of ViT for the image embeddings and TF-IDF
vectorizer for the text embeddings achieved an F1 score of 0.722, this was the second highest score
achieved. Lastly, the ensemble of EffNet-B3 and BERT for the image embeddings with TF-IDF for
the text embeddings produced a score of .701 on the test dataset, which was the lowest score among
the various models ensembled.
Using the image pre-processing techniques mentioned regarding HED and contour-masking, a better
F-1 score was achieved when compared to the unprocessed images from the training dataset. The
ViT and TF-IDF model ensemble training on the training dataset produced an F1-score of 0.514
| Architecture  | Dataset Header | F-1 Score|
| ------------- | ------------- | ------------- |
| Ensemble of NFNet with EffNet-B3 and BERT  | Test  | 0.733 |
| Ensemble of ViT with TF-IDF vectorizer  | Test  | 0.722 |
| Ensemble of EffNet-B3 and BERT with TF-IDF| Test | 0.701 |
| HED contour-masked images and Ensemble of ViT with TF-IDF| Training | 0.537 |
| Ensemble of ViT with TF-IDF | Training | 0.514 |
| HED images and Ensemble of ViT with TF-IDF | Training | 0.499 |

*Models and corresponding F-1 scores

when evaluated against the unprocessed training images. In contrast, when applying the HED and
contour-masking image pre-processing to the training images and evaluating those against the
ViT/TF-IDF model, a score of 0.537 was achieved. The images produced from the HED model
without the contour-masking was also tried against the training images and the ViT/TF-IDF model,
however this produced a lesser F-1 score of 0.499.
An additional ensemble of ViT for the image embeddings and BERT for the text embeddings (instead
of TF-IDF) was attempted, however this model did not perform as well compared to using TF-IDF.
Therefore, this model was discarded after some initial evaluation.



<!-- ROADMAP -->
## Future Work

Using a combination of the smallest-to-largest contours in the image in order to mask off
irrelevant features in the image improved the model performance on training dataset. This was done
as a pre-processing step to the images fed into the already trained inference model. Future work here
could include training the models on the pre-processed images in addition to using this method on the
test images. Based on the improvement observed, this could further improve our models accuracy.
Unfortunately, some of the models have a large inference time. We look to analyse models with less
inference time in future work, which would allow them to be used in real-time applications. In order
to improve our accuracy, we will look into giving more attention to the Recall scoring metric during
training. This would allow the model to better detect true positives..






<!-- LICENSE -->
## License

Distributed under the MIT License. See `LICENSE` for more information.



<!-- CONTACT -->
## Contact

Shiva Maruth Alapati - alapati.shiva1998@gmail.com

Project Link: [https://github.com/your_username/repo_name](https://github.com/your_username/repo_name)



<!-- ACKNOWLEDGEMENTS -->
## Acknowledgements
* [Kaggle](https://www.kaggle.com/)
* [Hugging Face](https://huggingface.co/)

