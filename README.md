# Novelty Analysis
Matlab and Python code for novelty exploration behavior analysis in mice.
Used after [DeepLabCut](https://github.com/AlexEMG/DeepLabCut) and [MoSeq](http://datta.hms.harvard.edu/research/behavioral-analysis/)  analysis.

## Scripts for DeepLabCut data analysis

#### Basic data analysis
Fisrt, run the DeepLabCut, see [Training a New Network for DeepLabCut](https://github.com/Rxie9596/Novelty_analysis/blob/master/Docs/Training_a_new_network.md) and [Running an existing network (Korleki)](https://github.com/Rxie9596/Novelty_analysis/blob/master/Docs/Using_DLC_in_UchidaLab_Korleki.md)

After that,


0. Edit configuration file 
```
Config_NovAna.m
```

Especially, be sure to use correct `networkname_format`, which is the network name after 'DeepLabCut' without the extension. For example `DeepCut_resnet50_MoSeqNoveltySep12shuffle1_1030000`

Be sure to use correct `videoname_format`, an example file name of your videos, including the '.mp4' or '.avi' extensions. For example, `C4_180907_rgb.mp4`

* You will need to run the following code directly under the folder containing all the videos and `.csv` files, if the videos are placed under subfolders, use:`MoveFromDir.m`

1. To mannually label the position of the arena and object, please use
```
MarkObjPos.m
```
2. Calculate head position, speed, angle etc. Also plotting the trajectory, heatmap, etc. 
```
Analysis.m
```
3. Make labeled videos to check whether the labels are correct. This script generate labeled videos with a side bar showing the frame number, distance, orientation, speed, etc. for mannually labeling some interesting behaviors.
```
VideoLabeling.m
```
#### Further data analysis
* Code for calculating and plotting the time spent around the object / orienting towards the object.
```
TimeStatistic.m
Plot_compare.m
```

* Code for calculating and plotting the time spent at different distances to the object per unit area.
```
DistHistPerUnitArea.m
```
* Code for event-based analyses, calculating and plotting several parameters, including number of interaction, time spent interacting with object, time per interaction, body length index, retreat speed, approach-retreat angle, etc.
```
EventBasedAnalysis.m
```

* Code for finding approach-retreat behavior in stimulus novelty mice.
```
FindingPokeDTW.m
```

## Scripts for MoSeq data analysis
First, run all the Moseq analysis, see [MoSeq Sample Commands](https://github.com/Rxie9596/Novelty_analysis/blob/master/Docs/MoSeq_Example_Command.md)

After that,

0. If necessary, split the RGB videos from the raw data generated by MoSeq.
```
MoSeqMoveRGB.m
```

1. Transfer the data generated by MoSeq to MATLAB readable format.
```
ModelDataTransfer.py
```
Run this script in the `moseq2` conda enviroment and under the directory where you saved this script (eg. `Novelty_analysis/MoSeqAnalysis`), using the following command,
```
python3 ModelDataTransfer.py
```
specify the path of the index file and model file, for example
```
index_file = '/media/alex/DataDrive1/MoSeqData/CvsS_180831/CvsS_20180831_MoSeq/moseq2-index.yaml'
model_file = '/media/alex/DataDrive1/MoSeqData/CvsS_180831/CvsS_20180831_MoSeq/my_model.p'
```
Also, specify where you would like to save the output file, for example,
```
save_directory='/home/alex/Desktop/MoSeqDataFrame.mat'
```

* if you are doing fiber phtotmetry with MoSeq, run the following code to transfer the fiber phtotmetry data to MATLAB readable format.
```
FPDataTransfer.py
```
Also, remember to specify the input and output directory.
```
save_directory='/home/alex/Desktop/MoSeqFP.mat'
filename = '/media/alex/DataDrive1/MoSeqData/MSFP_Test/180922/session_20180922154525/nidaq.dat'
nch=3
```
`nch` is the number of channels plus 1 (timestamps) of your photometry recording. For example, if you are recording two channels, GCaMP and tdTomato, choose `nch=3`

2. Edit mice index file for further analyses, you can find a template here
```
Mice_Index_Template.m
```
In the following scripts, mice indexes and date indexes are used by other scripts as specified in this file , please also spcify where to find this mice index file in the following scripts that you need to run.

3. Make labeled videos which show the syllables numbers and a color bar in the bottom which shows the syllables being used.
```
MoSeqVideoLabeling.m
```

4. Calculate and plot general syllable usage and conpare syllable expression of several different groups.
```
MoSeqGeneralSyllableAnalysis.m
```
Remember to spcify the mice and dates of each group. For example, G1 is contextual novelty mice, and G2 is stimulus novelty mice.
```
G1_Mice=[1 2 3 4];
G2_Mice=[5 6 7 8];
G1_Days=[3 4 5 6];
G2_Days=[3 4 5 6];

% G3 Base line
G3_Mice=1:8;
G3_Days=[1 2];
```
The results are sorted by `(G2-G1)/(G2+G1)`, so on the left hand side are G2 enriched syllables and on the right hand side are G1 enriched syllables.

5. Structure clusting of syllables,
```
MoSeqSyllableClustering.m
```

6. Plot the positions of interesting syllables.
```
MoSeqSyllablePos.m
```
Specify which syllable you would like to plot by setting `IntSyllable`
 
7. Calculate and plot the syllable expression at different distance to the object.
```
MoSeqSyllableDisToObj.m
```

8. Analyze general syllable transition,
```
MoSeqGeneralTransition.m
```
Remember to spcify the mice and dates of each group. 

9. Analyze transitions around an interesting syllable.
```
MoSeqInterestingNodeTransition.m
```
Remember to spcify the mice and dates of each group. Also specify which syllable you are interested in by setting, for example
```
IntNode='70';
```

10. Calculate syllable usage around human labels of an interesting behavior.
```
MoSeqEventAlignedAnalysis.m
```

11. Calculate syllable usage across trials, across days
```
MoSeqEventBasedAnalysis.m
```

* Scripts for sychronizing photometry data,
```
MoSeqFiberPhotometry.m
```

# Sample commands for using DeepLabCut and MoSeq

[Running an existing network (Korleki)](https://github.com/Rxie9596/Novelty_analysis/blob/master/Docs/Using_DLC_in_UchidaLab_Korleki.md)

[Running an existing network (Mitsuko)](https://github.com/Rxie9596/Novelty_analysis/blob/master/Docs/Using_DLC_in_UchidaLab_Mitsuko.md)

[Running an existing network (Sara & Eva)](https://github.com/Rxie9596/Novelty_analysis/blob/master/Docs/Using_DLC_in_UchidaLab_Sara%26Eva.md)




[Training a New Network for DeepLabCut](https://github.com/Rxie9596/Novelty_analysis/blob/master/Docs/Training_a_new_network.md)

[MoSeq Sample Commands](https://github.com/Rxie9596/Novelty_analysis/blob/master/Docs/MoSeq_Example_Command.md)

 
# Running on the cluster
#### DeepLabCut
1. Train a network locally, and copy the network to the cluster
2. Generate a singularity image based on docker image
3. Log in the cluster, Copy video to the cluster (/n/regal/uchida_lab)
4. Start an interactive session with GPUs
5. Load modules and build singularity container
6. Point GPUs to different videos and start extraction


#### MoSeq
1. Log into the cluster
2. Start an interactive session
3. Install  and activate moseq2 conda environment
4. Install moseq packages
5. Use moseq2-batch to generate a shell script
6. Execute the shell script, start jobs inside an interactive session.


