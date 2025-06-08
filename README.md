
The *mapKurator-system* requires that *cuda_11.3*, along with *cudnn* and *nvidia-smi*, is properly installed and functional on the host operating system. For successful installation, it is recommended to use *cuda_11.3-devel*. You can learn more [here](https://github.com/NVIDIA/nvidia-docker/wiki/CUDA).

Note that *cuda_11.3* officially supports only *Ubuntu 20.04* and earlier at the time this document was created.

### Step 0: Log in to DockerHub
You should have your personal access token ready. If not, please contact KarttaFoundation.

To log in using the Docker CLI:

1. Run
```
docker login -u karttafoundation
```

2. At the password prompt, enter the personal access token.

### Step 1: Pull docker image 

First pull the docker image with the following command:

```docker pull karttafoundation/spotting_2023:palette-multi```

Then run the container:
```
docker run -it --name YOUR_CONTAINER_NAME --gpus all -v /PATH/TO/INPUT/FOLDER/ON/HOST_MACHINE:/home/mapkurator-test-images/input/ -v /PATH/TO/OUTPUT/FOLDER/ON/HOST_MACHINE:/home/mapkurator-test-images/output/  karttafoundation/spotting_2023:palette-multi
```

Inside the container, run `conda activate mapKurator` to activate the mapkurator environment. 

**NOTE**: 
1) Remember to change `/PATH/TO/INPUT/FOLDER/ON/HOST_MACHINE` and `/PATH/TO/OUTPUT/FOLDER/ON/HOST_MACHINE` in the above command to two actual directory paths on your host machine. 
2) The -v option in the command above gives your docker container access to the folders on host machine. More documentation can be found at this [link](https://docs.docker.com/storage/volumes/)


### Step 2: Run commands 
Place any test images in the /PATH/TO/INPUT/FOLDER/ON/HOST_MACHINE mentioned above.

To run mapKurator from the docker image, first change directory as -     
```
cd /home/mapkurator-system/
```

Then you can run spotting on the test images.     


To run the **English** model:
```
python run_img.py --map_kurator_system_dir /home/mapkurator-system/ --input_dir_path /home/mapkurator-test-images/input/ --expt_name mapKurator_test --module_cropping --module_get_dimension --module_text_spotting --text_spotting_model_dir /home/spotter-palette/PALETTE --spotter_model palette --spotter_config /home/spotter-palette/PALETTE/configs/palette-test.yaml --spotter_expt_name english --module_img_geojson --output_folder /home/mapkurator-test-images/output/ --gpu_id 0
```

To run the **Chinese** model:
python run_img.py --map_kurator_system_dir /home/mapkurator-system/ --input_dir_path /home/mapkurator-test-images/input/ --expt_name mapKurator_test --module_cropping --module_get_dimension --module_text_spotting --text_spotting_model_dir /home/spotter-palette/PALETTE --spotter_model palette --spotter_config /home/spotter-palette/PALETTE/configs/palette-test-tc.yaml --spotter_expt_name chinese --module_img_geojson --output_folder /home/mapkurator-test-images/output/ --gpu_id 0

