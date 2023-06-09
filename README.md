### Kaggle Shopee Price Matching Multimodal Project (2021.3-2021.5)
  ***Repository:*** [Solution for shopee-product-matching](https://github.com/SZU-WenjieHuang/Kaggle-Shopee-Price-Matching-Multimodal-Project)\
  ***Competition Website:*** [Kaggle Shopee Price Matching Multimodal Project](https://www.kaggle.com/competitions/shopee-product-matching)\
  ***My Notebook Solition:*** [Latest Version](https://www.kaggle.com/code/szuwenjiehuang/nfnet-l0-nfnetl1-efficientnet-b5-pred-02b5aa)\
  ***Dataset:*** [35000(Trianing set)+7000(Test set) products in Shopee with image / image_phash / title / id / label](https://www.kaggle.com/competitions/shopee-product-matching/data)\
  ***Description:*** Developed a model recommend similar products to customers through image and text model. (CV+NLP)Used multiple image and text models to train a significant amount of data. And a voting method for Post-processing.
  
- #### [Datasets](https://www.kaggle.com/competitions/shopee-product-matching/data)
  ![image](https://user-images.githubusercontent.com/82434538/235440204-d1ba5aa5-ddc2-40ca-9487-62bc8fb2e939.png)
  The dateset contains 34250 images in the training set and roughly 70,000 images in the hidden test set. And each item have several attributes:</p>
   ***[train/test].csv***\
   ***posting_id:*** the ID code for the posting.\
   ***image:*** the image id.\
   ***image_phash:*** a perceptual hash of the image.\
   ***title:*** the product description for the posting.\
   ***label_group:*** ID code for all postings that map to the same product. Not provided for the test set.</p>
   ***[train/test]images***\
   the images associated with the items.(34250/70000)

- #### My Solution
  ![image](https://user-images.githubusercontent.com/82434538/235440367-c6d55678-23a8-4ebf-8642-a5ebfebbfcb5.png)

- ***Comparison:*** \
  ***Baseline*** ( TFIDF + ResNet18 + Result Splicing) : LB Score: 0.653 Top 80% \
  ***My Solution (on graph)*** (Nfnet-l0 + TFIDF + Indonesian BERT + Multi-Modal(EfficientNet-B3 + EfficientNet-B5 + TFIDF) : LB Score: 0.732 Top 17% \
  ***My Latest Solution*** (Nfnet-l0 + Nfnet-l1 + TFIDF + Multi-Modal(EfficientNet-B5 + TFIDF)) : LB Score: 0.734 Top 11% \
  ***Top Solution*** (Nfnet-l0 + swin-small + EfficientNet-B0 + BERT + Indonesian-BERT + Multlingual-v1 + TFIDF) : LB Score:0.746 Top 1% </p>


- #### Image Part
  In Image part I developed an ensemble model for multimodal fusion prediction, leveraging multiple deep learning models including EfficientNet B3, EfficientNet B5, and NFNet-L0. Each individual model was trained on the same dataset. The final prediction was obtained by combining the output of each model using an appropriate fusion strategy.\
  In the latest version, we replaced EfficientNet B3 with Nfnet-L1. Nfnet-L0 and Nfnet-L1 were used to generate separate predictions, while EfficientNet B5 and TFIDF were combined to form a hybrid model for prediction. By using this approach, we obtained better prediction results compared to the previous versions.

- #### Text Part
  In a similar strategy to the textual part and image part, we trained the TF-IDF and BERT models on the same dataset and separately obtained predictions from these two models.\
  Possibly due to the absence of a voting scheme, incorporating the prediction results of BERT actually resulted in a decrease in the prediction accuracy. Therefore, in the latest version, we only utilized the training results of the TFIDF text model, which alone achieved a prediction accuracy of 59%.

- #### Vote Prediction (Top solution's Method)
  ![image](https://user-images.githubusercontent.com/82434538/235440930-98d93a9b-dd93-4b02-ac85-b0c922341c83.png)
  The Top Solution proposed an excellent model fusion method: each model individually computed KNN or cosine similarity and obtained predictions at different thresholds. Starting from the smallest threshold, the predictions of each model were evaluated. If 5 out of 7 models had positive predictions, the result was accepted. If only one item ID was predicted at a threshold, the threshold was expanded until it reached 0.5. This method was adopted because it was observed that a large number of prediction errors occurred when a label was associated with only one item. By gradually expanding the threshold, accuracy was ensured while avoiding the situation where one label corresponded to only one item.

- ***Future Works:*** \
  After comparing with the winning kernel of the competition. The most serious deficiency of our kernel is post-processing and vote in prediction. According to the prediction results of the optimal LB score model in the early stage, we found that there are a large number of unmatched samples in the statistical results, that is, the matching results only match themselves, so we can reduce the matching standard (increase the matching distance threshold or reduce the similarity threshold).
