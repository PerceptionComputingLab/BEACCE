# BEACCE

Code for our paper "[BEACCE: Branch-Endpoint-Aware Double-DQN for Coronary Centerline Extraction in CT Angiography Images](https://link.springer.com/chapter/10.1007/978-3-030-59725-2_4)". 

- Proposed an uncertainty guided objective function to refine the left atrium segmentation based on Jenson-Shannon (JS) discrepancy.
- Conducted an symmetric multi-level supervision network for multi-scale representation learning.

The pipeline of our method is shown below:

<p align="center">
    <img src="images/framework.png" width="750" height="500"> 



## Requirements

Python 3.6.2

Pytorch 1.7

CUDA 11.2

## Data process

Our model was trained and evaluated on 100 LGE MRI volumes of AF patients, which was provided by 2018 Atrial Segmentation Challenge in the STACOM 2018. Each volume contained 88 slices along Z direction with a spatial dimension of either $576\times576$ or $640\times640$. The ground truth of LA in this dataset was performed by three trained observers. The ground truth included LA endocardial surface with the mitral valve, LA appendage, and an part of the pulmonary veins (PVs).

For data preprocess, we firstly normalized the intensity of each volume with zero-mean-unit-variation. To omit the unrelated region and save the computational cost, we cropped each volume into $256\times256\times88$ at the heart region. The 100 volumes were randomly divided into training (N=70), validation (N=10), and testing (N=20) sets.

## Training

**Run**

```python
train: python train.py
test: python test.py
```

## Results

Our segmentation model is evaluated by four evaluation metrics, which are **Dice score**, **Jaccard score**,  **Average Symmetric Surface Distance (ASSD)**, and **Hausdorff distance (HD)**. We performed three group of experiments to evaluate the performance of the proposed model. Please refer to the original paper for more details.

The individual score of metrics during the test stage is shown in the box diagrams. The tiny box, black &diams;, and -- in each box indicated the mean, outliers, and media, respectively. In each subplot, the x and y axes denote the model name and the score of each metric.

<p align="center">
    <img src="images/box_compare_result.png" width="1000" height="200">
</p>


We reconstructed one predicted case in multi-view for our ablation experiments. The ground truth is shown as green contour on each blue prediction. The last row is the corresponding 3D signed distance map between prediction and ground truth. The positive (or negative) sign indicated over (or under) segmentation. 

<p align="center">
    <img src="images/multiview.png" width="700" height="300"> 
</p>

## Cite

Please consider citing this project in your publications if it helps your research. The following is a BibTeX reference. The BibTeX entry requires the url LaTeX package.

    @article{liu2022uncertainty,
      title={Uncertainty-guided symmetric multi-level supervision network for 3D left atrium segmentation in late gadolinium-enhanced MRI},
      author={Liu, Yashu and Wang, Wei and Luo, Gongning and Wang, Kuanquan and Liang, Dong and Li, Shuo},
      journal={Medical Physics},
      publisher={Wiley Online Library}
      doi={10.1002/mp.15670}
    }
