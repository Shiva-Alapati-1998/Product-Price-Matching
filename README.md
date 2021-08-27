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
        <li><a href="#installation">Installation</a></li>
      </ul>
    </li>
    <li><a href="#usage">Usage</a></li>
    <li><a href="#roadmap">Roadmap</a></li>
    <li><a href="#contributing">Contributing</a></li>
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
| ------------- | ------------- |  |
| Ensemble of NFNet with EffNet-B3 and BERT  | Content Cell  | |
| Ensemble of ViT with TF-IDF vectorizer  | Content Cell  | |
| Ensemble of EffNet-B3 and BERT with TF-IDF|cc| |
| HED contour-masked images and Ensemble of ViT with TF-IDF| | |


  F-1 Score
 Test 0.733
 Test 0.722
 Test 0.701


Training 0.537
Ensemble of ViT with TF-IDF Training 0.514
HED images and Ensemble of ViT with TF-IDF Training 0.499
Table 1: Models and corresponding F-1 scores

when evaluated against the unprocessed training images. In contrast, when applying the HED and
contour-masking image pre-processing to the training images and evaluating those against the
ViT/TF-IDF model, a score of 0.537 was achieved. The images produced from the HED model
without the contour-masking was also tried against the training images and the ViT/TF-IDF model,
however this produced a lesser F-1 score of 0.499.
An additional ensemble of ViT for the image embeddings and BERT for the text embeddings (instead
of TF-IDF) was attempted, however this model did not perform as well compared to using TF-IDF.
Therefore, this model was discarded after some initial evaluation.



<!-- ROADMAP -->
## Roadmap

See the [open issues](https://github.com/othneildrew/Best-README-Template/issues) for a list of proposed features (and known issues).



<!-- CONTRIBUTING -->
## Contributing

Contributions are what make the open source community such an amazing place to be learn, inspire, and create. Any contributions you make are **greatly appreciated**.

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request



<!-- LICENSE -->
## License

Distributed under the MIT License. See `LICENSE` for more information.



<!-- CONTACT -->
## Contact

Your Name - [@your_twitter](https://twitter.com/your_username) - email@example.com

Project Link: [https://github.com/your_username/repo_name](https://github.com/your_username/repo_name)



<!-- ACKNOWLEDGEMENTS -->
## Acknowledgements
* [GitHub Emoji Cheat Sheet](https://www.webpagefx.com/tools/emoji-cheat-sheet)
* [Img Shields](https://shields.io)
* [Choose an Open Source License](https://choosealicense.com)
* [GitHub Pages](https://pages.github.com)
* [Animate.css](https://daneden.github.io/animate.css)
* [Loaders.css](https://connoratherton.com/loaders)
* [Slick Carousel](https://kenwheeler.github.io/slick)
* [Smooth Scroll](https://github.com/cferdinandi/smooth-scroll)
* [Sticky Kit](http://leafo.net/sticky-kit)
* [JVectorMap](http://jvectormap.com)
* [Font Awesome](https://fontawesome.com)





<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[contributors-shield]: https://img.shields.io/github/contributors/othneildrew/Best-README-Template.svg?style=for-the-badge
[contributors-url]: https://github.com/othneildrew/Best-README-Template/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/othneildrew/Best-README-Template.svg?style=for-the-badge
[forks-url]: https://github.com/othneildrew/Best-README-Template/network/members
[stars-shield]: https://img.shields.io/github/stars/othneildrew/Best-README-Template.svg?style=for-the-badge
[stars-url]: https://github.com/othneildrew/Best-README-Template/stargazers
[issues-shield]: https://img.shields.io/github/issues/othneildrew/Best-README-Template.svg?style=for-the-badge
[issues-url]: https://github.com/othneildrew/Best-README-Template/issues
[license-shield]: https://img.shields.io/github/license/othneildrew/Best-README-Template.svg?style=for-the-badge
[license-url]: https://github.com/othneildrew/Best-README-Template/blob/master/LICENSE.txt
[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=for-the-badge&logo=linkedin&colorB=555
[linkedin-url]: https://linkedin.com/in/othneildrew
[product-screenshot]: images/screenshot.png

