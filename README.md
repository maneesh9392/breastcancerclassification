# breastcancerclassification
-I have done this project using Breakhis datset which is publicly available in kaggle.
-Leveraging the DenseNet121 architecture pre-trained on the ImageNet dataset for transfer learning by utilizing its convolutional base as a fixed feature extractor or for fine-tuning downstream tasks.

This architecture is designed as a two-stage hierarchical deep learning model for breast cancer histopathology image classification. In the first stage, the model performs a binary classification to determine whether an image belongs to the benign or malignant class. The backbone is DenseNet121, from which intermediate feature maps (conv3_block12_concat, conv4_block24_concat, conv5_block16_concat) are extracted to capture multi-scale visual patterns. Each feature branch is processed with global average pooling, normalization, dense layers with L2 regularization, and batch normalization, ensuring both fine-grained and high-level representations are learned. These features are then fused and passed through dense layers with dropout, leading to a softmax output for binary prediction.

In the second stage, once the primary class is identified, a separate multi-class classifier is triggered to predict one of the four subtypes within that class (e.g., adenosis, fibroadenoma, phyllodes tumor, and tubular adenoma for benign; ductal, lobular, mucinous, and papillary carcinoma for malignant). This stage follows the same fusion-based architecture but with a final softmax layer sized for four outputs instead of two. Together, this pipeline ensures that the system first makes a coarse decision (benign vs malignant) and then a fine-grained decision (subtype classification), enabling more interpretable and clinically useful outcomes.

👉 Essentially, this makes the model a hierarchical cancer classifier that combines binary diagnosis and subtype classification in a structured way.

# GAN implementation:
Since you’re working on hierarchical breast cancer classification, one of the key challenges is class imbalance, where some subtypes (both benign and malignant) have fewer samples compared to others. This imbalance can cause the model to overfit majority classes while underperforming on underrepresented subtypes. To address this, you have implemented a Generative Adversarial Network (GAN) to synthesize new histopathology images for the minority subtypes.

The GAN consists of a generator that learns to create realistic synthetic images from random noise (or latent space) and a discriminator that learns to distinguish between real images from the dataset and generated ones. Through adversarial training, the generator gradually improves its ability to mimic the morphological patterns and tissue textures of real histopathology samples. By generating additional images for underrepresented subtypes, you are able to balance the dataset distribution, allowing the classification model to learn equally well across all classes.

This augmentation strategy enhances feature diversity, reduces bias toward majority subtypes, and improves generalization performance during training. Integrating GAN-based augmentation with your two-stage classification pipeline (binary → subtype classification) ensures that the model has sufficient data to capture the subtle morphological variations necessary for accurate and fair subtype predictions.

👉 In short, your GAN addresses the data imbalance problem by enriching the dataset with realistic synthetic images, making the hierarchical classification model more robust, balanced, and clinically reliable.

You notice the accuracy difference between the benign and malignant subtypes,the reason behind it is I have implemented GAN to generate systhesized images of BENIGN subtypes to make a balanced dataset,and i have not implemented it on MALIGNANT subtypes. 

