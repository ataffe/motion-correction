# motion-correction

Current motion correction progress from thaotnguyen.

At the moment, only co-tracker is set up for complete video processing. 

tapnet does not seem to be able to handle adding additional points to the query without re-initializing the model each time a new point is added, which is blocking implementation of tapnet. 

It is unclear if omnimotion has that functionality, but it most likely doesn't. In addition, omnimotion's documentation doesn't provide a clear path forward for feeding a video file into it.

## Instructions for use

In order to process a video, the following steps must be performed:
1. Install requirements for each submodule (FLImBrushCNNSeg, co-tracker, tapnet). Follow the documentation present in each repo.
2. Run the code in FLImBrushCNNSeg to create the segmentation mask images for your video. This will create a folder of images that correspond to the tool segmentation mask for each frame of your video.
3. Open generate_segm_mask.py and edit image_dir to point to the folder that you generated in step #2. This will read the images and create a .pkl that has a list whose elements are pairs, with the first element being the frame number and the second being a numpy array that holds the segmentation mask on that frame.
4. Run co-tracker on your video. You may have to go into the code and edit lines 88-90 depending on how your queries file (the file with XY point coordinates and frame numbers that determines what points are queried and when) is set up.
```co-tracker/online_demo.py --video_path path/to/video --mask_path path/to/mask --queries_path path/to/queries```
5. You can also try to run tapnet on your video, but the queries are not fully set up yet because tapnet cannot take additional points after the first frame. If you want to run tapnet, open `live_demo.py` and add your video path to line 33.
```tapnet/live_demo.py```
