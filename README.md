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

Note: the 3D scenes are selected from [Gibson](http://gibsonenv.stanford.edu/) and [Matterport3D](https://niessner.github.io/Matterport/) datasets. All RGB frames and depth maps are rendered with the [AI-Habitat](https://aihabitat.org/) simulator. Collision checking is performed with [PyBullet](https://pybullet.org/wordpress/). Per the requirement from the Matterport team, we attach a link to the user license [agreement](https://kaldir.vc.in.tum.de/matterport/MP_TOS.pdf) here. 

## References
* HuMoR: 3D Human Motion Model for Robust Pose Estimation. Rempe, Davis and Birdal, Tolga and Hertzmann, Aaron and Yang, Jimei and Sridhar, Srinath and Guibas, Leonidas J.. International Conference on Computer Vision (ICCV), 2021.
* Gibson env: Real-world perception for embodied agents. Xia, Fei and Zamir, Amir R and He, Zhiyang and Sax, Alexander and Malik, Jitendra and Savarese, Silvio. Proceedings of the IEEE conference on computer vision and pattern recognition, 2018.
* Matterport3d: Learning from rgb-d data in indoor environments. Chang, Angel and Dai, Angela and Funkhouser, Thomas and Halber, Maciej and Niessner, Matthias and Savva, Manolis and Song, Shuran and Zeng, Andy and Zhang, Yinda. arXiv preprint arXiv:1709.06158, 2017.
* Habitat 2.0: Training Home Assistants to Rearrange their Habitat. Andrew Szot and Alex Clegg and Eric Undersander and Erik Wijmans and Yili Zhao and John Turner and Noah Maestre and Mustafa Mukadam and Devendra Chaplot and Oleksandr Maksymets and Aaron Gokaslan and Vladimir Vondrus and Sameer Dharur and Franziska Meier and Wojciech Galuba and Angel Chang and Zsolt Kira and Vladlen Koltun and Jitendra Malik and Manolis Savva and Dhruv Batra. Advances in Neural Information Processing Systems (NeurIPS), 2021.
* Habitat: {A} {P}latform for {E}mbodied {AI} {R}esearch. Manolis Savva and Abhishek Kadian and Oleksandr Maksymets and Yili Zhao and Erik Wijmans and Bhavana Jain and Julian Straub and Jia Liu and Vladlen Koltun and Jitendra Malik and Devi Parikh and Dhruv Batra. Proceedings of the IEEE/CVF International Conference on Computer Vision (ICCV), 2019.
* PyBullet, a Python module for physics simulation for games, robotics and machine learning. Erwin Coumans and Yunfei Bai. \url{http://pybullet.org}, 2016--2021.
