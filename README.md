# event-image-stereo-dataset

Stereo setup of event camera dataset made by Hoonhee Cho @Visual Intelligence Lab. of KAIST. 

Our datasets include the 



The dataset link is: https://drive.google.com/drive/folders/1CmlRc3nw_IDi0_6nBK4yXJ-db8a0IMDe?usp=sharing

left_camera
    - left_event
    - left_image
    - left_depth
right_camera
    - right_event
    - right_image

The resolution of images and events is 346 x 260 as same as DVS346 camera.
In our depth image, because of the blender version, a distance map is provided, not a depth map.
Therefore, we transform the distance map to depth map using camera intrinisic parameter. (camera FoV = 90 degree)

def _get_depth_image(depth_image_path):
    depth_image = np.array(cv2.imread(depth_image_path, cv2.IMREAD_ANYDEPTH))
    depth_image = (depth_image / 655.35)
    invalid_depth1 = (depth_image == 100)
    x = np.linspace(0, 345, 346) 
    y = np.linspace(0, 259, 260)
    X, Y = np.meshgrid(x,y)
    norm_x = 0.0058*X - 1
    norm_y = 0.0058*Y - 0.7514
    norm_scale = np.sqrt(np.multiply(norm_x,norm_x) + np.multiply(norm_y ,norm_y) + 1)
    depth_image = np.divide(depth_image, norm_scale)
    depth_image[invalid_depth1] = float('inf')
    
    return depth_image


If you use any of the dataset, please cite the following publications:

TBD
