# Incremental-Dialogue-System
Code and data for acl2019 paper "Incremental Learning from Scratch for Task-Oriented Dialogue Systems".

If you use any source codes or datasets included in this toolkit in your
work, please cite the following paper. The bibtex are listed below:

    @article{wang2019incremental,
      title={Incremental Learning from Scratch for Task-Oriented Dialogue Systems},
      author={Wang, Weikang and Zhang, Jiajun and Li, Qian and Hwang, Mei-Yuh and Zong, Chengqing and Li, Zhifei},
      journal={arXiv preprint arXiv:1906.04991},
      year={2019}
    }

### Requirements
     python 3.6
     pytorch >= 1.0.0
     numpy
     scipy
     sklearn

## Datasets
Our data is available at https://drive.google.com/file/d/1KYZNxzcU5kximq1-_IDC_4NCFabz40jN/view?usp=sharing. Download and unzip at ./data.
- ./data/preprocessed contains the preprocessed five sub-dataset.
- ./data/original contains the original dialogue episodes before entity replacing.
- ./data/script annotates the dialogue scenarios in each episode.

## Run Models
python run.py

## Change Configurations
Change the parameters in RunConfig at config.py.

## Changes
The following changes were made to the original code:

1.
Replaced line 355 in  cvae.py:
log["loss"].append(loss.item())

with:

if loss is not None:
    log["loss"].append(loss.item())        
else:
    log["loss"].append(None)

2.
Replaced lines 41 and 42 in config.py:

model_save_path = "checkpoints/task_1_deploy_from_scratch_model.pkl"
debug_path = "debug/task_1_deploy_from_scratch_debug.pkl"

with:

import os
import time

#Create "./checkpoints" and "./debug" directories if they don't exist
if not os.path.exists("checkpoints"):
    os.mkdir("checkpoints")
if not os.path.exists("debug"):
    os.mkdir("debug")

#Add task number and timestring to saved models' filename to allow storing multiple models
timestr = time.strftime("%Y%m%d-%H%M%S")    
model_save_path = "checkpoints/{task}_deploy_from_scratch_model_{time}.pkl".format(task=coming_task, time=timestr)
debug_path = "debug/{task}_deploy_from_scratch_debug_{time}.pkl".format(task=coming_task, time=timestr)
            
3. 
Added "encoding="UTF-8" to 'open file' in several places.








