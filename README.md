# ProMISe: Promptable Medical Image Segmentation using SAM

The [paper](https://openreview.net/pdf?id=apG2vDGpN5) has been accepted by NeuriIPs
.
Our main page in paperwithcode is [here](https://paperswithcode.com/paper/promise-promptable-medical-image-segmentation)

# 1. Introduction
With the proposal of Segment Anything Model (SAM), finetuning SAM for medical image segmentation (MIS) has become popular. However, due to the large size of the SAM model and the significant domain gap between natural and medical images, fine-tuning-based
strategies are costly with potential risk of instability, feature damage
and catastrophic forgetting. Furthermore, some methods of transferring
SAM to a domain-specific MIS through fine-tuning strategies disable the
model’s prompting capability, severely limiting its utilization scenarios.
In this paper, we propose an Auto-Prompting Module (APM), which provides SAM-based foundation model with Euclidean adaptive prompts
in the target domain. Our experiments demonstrate that such adaptive prompts significantly improve SAM’s non-fine-tuned performance
in MIS. In addition, we propose a novel non-invasive method called Incremental Pattern Shifting (IPS) to adapt SAM to specific medical domains.  Experimental results show that the IPS enables SAM to achieve
state-of-the-art or competitive performance in MIS without the need for
fine-tuning. By coupling these two methods, we propose ProMISe, an
end-to-end non-fine-tuned framework for Promptable Medical Image
Segmentation. Our experiments demonstrate that both using our methods individually or in combination achieves satisfactory performance in
low-cost pattern shifting, with all of SAM’s parameters frozen.
# 2. Framework
![image](https://github.com/xinkunwang111/ProMISe/assets/130198762/1e1ff6cf-7eb6-4ab9-a2a5-7fc28661c3a5)

[![PWC](https://img.shields.io/endpoint.svg?url=https://paperswithcode.com/badge/promise-promptable-medical-image-segmentation/medical-image-segmentation-on-isic-2018-1)](https://paperswithcode.com/sota/medical-image-segmentation-on-isic-2018-1?p=promise-promptable-medical-image-segmentation)

[![PWC](https://img.shields.io/endpoint.svg?url=https://paperswithcode.com/badge/promise-promptable-medical-image-segmentation/medical-image-segmentation-on-cvc-colondb)](https://paperswithcode.com/sota/medical-image-segmentation-on-cvc-colondb?p=promise-promptable-medical-image-segmentation)

[![PWC](https://img.shields.io/endpoint.svg?url=https://paperswithcode.com/badge/promise-promptable-medical-image-segmentation/medical-image-segmentation-on-etis)](https://paperswithcode.com/sota/medical-image-segmentation-on-etis?p=promise-promptable-medical-image-segmentation)

[![PWC](https://img.shields.io/endpoint.svg?url=https://paperswithcode.com/badge/promise-promptable-medical-image-segmentation/lesion-segmentation-on-isic-2018)](https://paperswithcode.com/sota/lesion-segmentation-on-isic-2018?p=promise-promptable-medical-image-segmentation)

[![PWC](https://img.shields.io/endpoint.svg?url=https://paperswithcode.com/badge/promise-promptable-medical-image-segmentation/medical-image-segmentation-on-kvasir-seg)](https://paperswithcode.com/sota/medical-image-segmentation-on-kvasir-seg?p=promise-promptable-medical-image-segmentation)


# 3. Usage
## 3.1 Packages
Please see SAM.yaml.
## 3.2 Datasets 
1. [cvc300(Endoscene)](https://pages.cvc.uab.es/CVC-Colon/index.php/databases/cvc-endoscenestill/)
2. [Clinic-DB](https://polyp.grand-challenge.org/CVCClinicDB/)
3. [Colon-DB](https://figshare.com/articles/figure/Polyp_DataSet_zip/21221579)
4. [ETIS-LARIBPOLYPDB](https://polyp.grand-challenge.org/ETISLarib/)
5. [Kvasir-SEG](https://www.kaggle.com/datasets/meetnagadia/kvasir-dataset)
6. [ISIC-2018](https://challenge.isic-archive.com/data/#2018)
   
The input dataset csv format should follow the "combined_5_1024.csv"




## 3.3 Train
Please use train_ProMISe.sh.  You can change the model different   `net_name`

1. `APM_resnet`: For only use APM with resnet34
2. `APM_IPS_resnet`: Use resnet34 as APM, and use IPS block
3. `IPS_GT`:Use GT points as prompt, and use IPS block

You can load the pre-trained model's checkpoint into `check_point_path`.

## 3.4 Evaluation
Please use eval_ProMISe.sh.  You can change the model different   `net_name`

1. `APM_resnet`: For only use APM with resnet34
2.  `APM_IPS_GT_resnet`: Use checkpoint trained in `APM_IPS_resnet`, but use GT to provide point prompts.
3.  `IPS_GT`:Use GT points as prompt, and use IPS block


You can load the trained model's checkpoint into `TEST_check_point_path`.If you want to acquire the metrics for different dataset, you can input the split csv file of the other datasets into `TEST_IF_SPLIT_CSV`. (You can refer the format of 6 csv files in `Data_set_format` folder.)

## 3.5 Checkpoints
1. [APM_resnet](https://drive.google.com/file/d/1bjyRUKolZ5ON-egnSnfpLNdyDQvcOmWL/view?usp=drive_link)
2. [APM_IPS_resnet](https://drive.google.com/file/d/1HSX4HgrrBreAoVDSUcOZhpN8BnKEnJO-/view?usp=drive_link)
3. [IPS_GT](https://drive.google.com/file/d/1R1eqzYkEjoynSynn8OP4maL6YjZjgW-f/view?usp=drive_link)

# 4. Notes
## 4.1  Random Seed
In training process with `IPS_GT`, the random seed is important. In order to keep the stability and generalization when evaluation, we recommend you do not set random seed in training  process. If you choose random seed, please keep the same random seed when you do the evaluation. This might help you get better performance.
## 4.2 Postprocessing
We use ` cv2.morphologyEx(image, cv2.MORPH_OPEN, kernel)` to do the postprocessing. However, the best choice of `kernel size` and `cv2.MORPH_OPEN/cv2.MORPH_CLOSE` may vary with models and datasets.

# 5. Acknowledge
We are very grateful for the endeavour and works from Meta. Their work on SAM provide the fundament for our framework.



   


