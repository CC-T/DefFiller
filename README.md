# DefFiller
This is the repository for "DefFiller: Mask-Conditioned Diffusion for Salient Steel Surface Defect Generation".  
[arXiv Link](https://arxiv.org/abs/2412.15570)
![input-output](https://github.com/CC-T/DefFiller/blob/main/assets/input-output.jpg)

## Dataset
1. Download [SD-saliency-900](https://drive.google.com/file/d/1yQdfow1-WvDilQTZ1zj1EbbErN1DksVF/view?usp=sharing)
2. Place the masks in the directory "./DATA/SD-saliency-900/Ground_truth" and the images in "./DATA/SD-saliency-900/Source_Images".
3. Generate a "caption.json" file for the dataset by referring to "process_json.py".

## Env Install
We follow [GLIGEN](https://github.com/gligen/GLIGEN).

## Train
1. Download the pre-trained model [here](https://huggingface.co/gligen/gligen-generation-sem/blob/main/diffusion_pytorch_model.bin).
2. Put it on the directory named "./model_sem", and rename it to "sem_diffusion_pytorch_model.bin".
3. Start to train:
```
   #python main.py --name=your_experiment_name  -- OUTPUT_ROOT=save_path
```
The experiment will be saved in “OUTPUT_ROOT/name”.

## Inference
```
   #python infer.py
```
Example samples for each checkpoint will be saved in “generation_samples”.

## Acknowledgements
This repo is mainly inspired by [GLIGEN](https://github.com/gligen/GLIGEN). We thank the authors a lot for their valuable efforts.

## Guidelines
Based on our extensive experimentation, we provide the following guidelines for effectively using DefFiller:

1. DefFiller contributes most significantly to detection performance in data-scarce scenarios ($≤100$ samples per defect category). For datasets with abundant samples ($>1000$ per category), the improvements are more modest.
2. When implementing DefFiller for dataset expansion, we recommend using a guidance scale ($\omega_{cfg}$) of 2-4 for optimal results, as values in this range provide the best balance between defect fidelity and background consistency.
3. Generated images should be carefully filtered before adding to the training set. Specifically, we found that including only samples with IoU scores $\geq0.6$ between the conditioning mask and a pre-trained detector's prediction ensures high-quality training samples.
4. The method is less effective for extremely small defects ($<10$ pixels in width) or highly textured backgrounds where defect-background boundaries become ambiguous. In these scenarios, we recommend using more targeted mask conditions that emphasize the defect region.

## Citation
Please consider citing our paper in your publications if the project helps your research. BibTeX reference is as follows.
```
   @misc{tai2024deffillermaskconditioneddiffusionsalient,
      title={DefFiller: Mask-Conditioned Diffusion for Salient Steel Surface Defect Generation}, 
      author={Yichun Tai and Zhenzhen Huang and Tao Peng and Zhijiang Zhang},
      year={2024},
      eprint={2412.15570},
      archivePrefix={arXiv},
      primaryClass={cs.CV},
      url={https://arxiv.org/abs/2412.15570}, 
}
```
