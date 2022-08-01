# Style Transfer with Bio-realistic Appearance Manipulation for Skin-tone Inclusive rPPG
Yunhao Ba*, Zhen Wang*, Kerim Doruk Karinca, Oyku Deniz Bozkurt, and Achuta Kadambi

University of California, Los Angeles

Project Website
----------------
https://visual.ee.ucla.edu/rppg_augmentation.htm/

Abstract
---------
Data-driven remote vital sign estimation provides an efficient alternative to on-site clinical monitoring, however, its performance can be biased due to the imbalanced training sets. In this work, we take remote photoplethysmography (rPPG) as an example to examine the performance bias from skin tone variations in non-contact heart rate estimation. In rPPG, recent deep learning models have significantly improved the accuracy of the physiological measurement, however, the existing datasets MMSE-HR, AFRL, and UBFC-RPPG only contain roughly 10%, 0%, and 5% of dark-skinned subjects respectively. The imbalanced training sets result in a poor generalization capability of these models and lead to unwanted bias toward different demographic groups. In Western academia, it is regrettably difficult in a university setting to collect data on these dark-skinned subjects. Here we show a first attempt to overcome the lack of dark-skinned subjects by synthetic augmentation. A joint optimization framework is utilized to translate real videos from light-skinned subjects to dark skin tones while retaining their pulsatile signals. In the experiment, our method exhibits around 38% reduction in mean absolute error for the dark-skinned group and 49% improvement on bias mitigation, as compared with the previous work trained with just real samples.

Training
--------
This GitHub repository provides access to the code used for the primary results of the paper. The code is tested with PyTorch 1.7.1. Please follow the following steps to set up the training experiment.

1. Request access to the [UBFC-RPPG Dataset](https://sites.google.com/view/ybenezeth/ubfcrppg).
2. Crop the videos from the UBFC-RPPG Dataset using [MTCNN](https://github.com/ipazc/mtcnn). The cropping region should be 160% width and height of the detected bounding box.
3. Apply the Caucasian-to-African translation to the cropped frames using the pretrained model from [Exploring Racial Bias within Face Recognition via per-subject Adversarially-Enabled Data Augmentation](https://github.com/seymayucer/VGG1200-Races). These translated frames will be used as the pseudo ground truth.
4. Convert the cropped videos to H5 format for each subject.
    - The frames should be stored with a "dataset_1" key.
    - The PPG waves should be stored with a "ppg" key.
 5. Download the pretrained [weights](https://drive.google.com/drive/folders/1zDrmhfAJJ2igJcuokHKBF76ysrq3K44f?usp=sharing) for the generator and the estimator. As described in the paper, the generator is first pretrained to reproduce the pseudo ground truth, and the rPPG estimator is first pretrained to estimate the waves from real subjects.
 6. Change the paths for the dataloaders and pretrained weights to your local paths in the rppg_aug.ipynb notebook and start training.

Transferred Videos
------------------
Since the transferred videos involve human subjects, the final transferred videos are only available on request. Please contact us if you need to get access to the transferred videos from our model. Also please make sure you have been permitted to use UBFC-RPPG Dataset in advance.

Contact
-------
If you have any questions, feel free to contact yhba@ucla.edu and zhenwang@ucla.edu.
