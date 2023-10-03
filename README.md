# COPILOT: Human-Environment Collision Prediction and Localization from Egocentric Videos
Boxiao Pan, Bokui Shen*, Davis Rempe*, Despoina Paschalidou, Kaichun Mo, Yanchao Yang, Leonidas J. Guibas. (* equal contribution)

ICCV 2023. 

[[Website]](https://sites.google.com/stanford.edu/copilot) [[Arxiv]](https://arxiv.org/abs/2210.01781)

## Update
* 10/03/2023: Released data files.

## Synthetic Dataset
We released our synthetic dataset (detailed in main paper Sec. 3.2 and supplement Sec. C.3) [here](https://drive.google.com/drive/folders/1YAHLZdjGOkswgMrjH092XcDRHxpH941p?usp=drive_link). The full dataset is split into 6 zips, each containing data files organized under scene names. After unzipping all, put all scene folders under a top-level folder. The file structure should look like:
* copilot_dataset
  * 17DRP5sb8fy
    * BioMotionLab_NTroje_rub025_0027_jumping1_poses_457_frames_30_fps_b9346seq0
      * observations
      * depth
      * motion_seq.npz
      * penetration_label.npy
      * (col_coords.npy)
      * (col_spot_timesteps.npy)
    * ...
  * 29hnd4uzFmX
  * ...

Each scene contains several motion sequences (e.g., `BioMotionLab_NTroje_rub025_0027_jumping1_poses_457_frames_30_fps_b9346seq0`). Each sequence has a `motion_seq.npz`, which a human motion sequence that follows the [HuMoR](https://github.com/davrempe/humor) format. `observations` and `depth` are the RGB and depth frames recorded.  `penetration_label.npy` is the penetration label obtained via our collision checking procedure, which records the body parts involved in the collision (0: "torso"; 1: "left elbow"; 2: "right elbow"; 3: "left hand"; 4: "right hand"; 5: "head"; 6: "left leg"; 7: "right leg"; 8: "left foot"; 9: "right foot"; 100: "no collision"). `col_coords.npy` records the image frame coordinates of collision obtained by projecting the 3D collision vertices, while `col_spot_timesteps.npy` stores the time steps when collisions happen. These two files only exist for sequences that have collisions happened. Both are (6,) numpy arrays, following the order of `["pelvis", "head", "left wrist", "right wrist", "left knee, right knee"]`. `col_coords.npy` then notes for each step in `col_spot_timesteps.npy`, the image coordinates of collision on that body joint.
