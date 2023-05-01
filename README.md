### Kaggle Shopee Price Matching Multimodal Project (2021.3-2021.5)
  ***Repository:*** [Solution for shopee-product-matching](https://github.com/SZU-WenjieHuang/Kaggle-Shopee-Price-Matching-Multimodal-Project)\
  ***Competition Website:*** [Kaggle Shopee Price Matching Multimodal Project](https://www.kaggle.com/competitions/shopee-product-matching)\
  ***My Notebook Solition:*** [Jupyter Notebook in Kaggle](https://www.kaggle.com/code/szuwenjiehuang/nfnet-l0-nfnetl1-efficientnet-b5-pred-02b5aa)\
  ***Dataset:*** [35000(Trianing set)+7000(Test set) products in Shopee with image / image_phash / title / id / label](https://www.kaggle.com/competitions/shopee-product-matching/data)\
  ***Description:*** Developed a model recommend similar products to customers through image and text model. (CV+NLP)Used multiple image and text models to train a significant amount of data. And a voting method for Post-processing.
  
- #### [Datasets](https://www.kaggle.com/competitions/shopee-product-matching/data)
![image](https://user-images.githubusercontent.com/82434538/235440204-d1ba5aa5-ddc2-40ca-9487-62bc8fb2e939.png)
 The dateset contains 34250 images in the training set and roughly 70,000 images in the hidden test set. And each item have several attributes:</p>
   ***[train/test].csv***\
   ***posting_id:*** the ID code for the posting.\
   ***image:*** the image id/md5sum.\
   ***image_phash:*** a perceptual hash of the image.\
   ***title:*** the product description for the posting.\
   ***label_group:*** ID code for all postings that map to the same product. Not provided for the test set.</p>
   ***[train/test]images***\
   the images associated with the items.(34250/70000)

- #### My Solution
![image](https://user-images.githubusercontent.com/82434538/235440367-c6d55678-23a8-4ebf-8642-a5ebfebbfcb5.png)

***Comparison:*** \
  ***Baseline*** ( TFIDF + ResNet18 + Result Splicing) : LB Score: 0.653 Top 80% \
  ***My Solution*** (EfficientNet-B3 + EfficientNet-B5 + Nfnet-l0 + TFIDF + BERT + (Multi-Modal)) : LB Score: 0.734 Top 11% \
  ***Top Solution*** (Nfnet-l0 + swin-small + EfficientNet-B0 + BERT + Indonesian-BERT + Multlingual-v1 + TFIDF) : LB Score:0.746 Top 1% </p>
***Future Works:*** \
  After comparing with the winning kernel of the competition. The most serious deficiency of our kernel is post-processing and vote in prediction. According to the prediction results of the optimal LB score model in the early stage, we found that there are a large number of unmatched samples in the statistical results, that is, the matching results only match themselves, so we can reduce the matching standard (increase the matching distance threshold or reduce the similarity threshold).


- #### Image Part
![image](https://user-images.githubusercontent.com/82434538/235440677-8aa26466-9355-4783-9010-b4e8c574680f.png)

- #### Text Part
![image](https://user-images.githubusercontent.com/82434538/235440749-ddb8aaaa-1c7f-4658-bb41-98a45cb52027.png)

- #### KNN Similarity
![image](https://user-images.githubusercontent.com/82434538/235440865-df1c03db-2bff-46a7-a286-cd6286d900f1.png)

- #### Vote Prediction
![image](https://user-images.githubusercontent.com/82434538/235440930-98d93a9b-dd93-4b02-ac85-b0c922341c83.png)

- #### Summary
![image](https://user-images.githubusercontent.com/82434538/235441054-b8c76eee-aca8-47d8-abf9-96f623bb414c.png)

