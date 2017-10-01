# Vehicle-License-Plate-Recognition-and-Positioning-in-a-Parking-Lot
This is a repository for a **recognition system of vehicle license plate and parking space number**. In order to help the owner to find the parking location or available parking space.  It also provides servers' easier vehicle identification and parking management in the parking lot.

This project mainly explored the non-Chinese character recognition of vehicle license plate. Added the new feature of parking space number recognition to support quickly locate available parking space.

System modules are as follows:

+ [Vehicle License Plate Part](#vehicle-license-plate-part)
  + [License plate location and extraction](#license-plate-location-and-extraction)
  + [License plate image segmentation](#license-plate-segmentation)
  + [License plate recognition](#license-plate-recognition)
+ [Parking Space Number Part](#parking-space-number-part)
  + [Space number extraction](#space-number-extraction)
  + [Space number recognition](#space-number-recognition)
+ [Demo](#demo)
+ [Conclusion](#Conclusion)



# <a name = "vehicle-license-plate-part"></a>Vehicle License Plate Part

Original Image ==> Preprocessing ==> Location and Extraction ==> Segmentation ==> Recognition

## <a name = "license-plate-location-and-extraction"></a>License plate location and extraction

There are four kinds of vehicle licenses in mainland China, namely, the civil blue-white license plate, the black and white license plate, the police station with black and white license plate and the foreign license plate. China's license plate mainly has the following characteristics:

+ The license plate consists of two or three colors
+ The contour size of the license plate is 440 mm × 140 mm, the width and height ratio is about 3;
+ The character area is about 20% of  the entire license plate area
+ The interval between adjacent symbols is usually 12 mm, the distance between the second and third symbols is 34 mm, and the size of the character is 45 mm × 90 mm

In general, the license plate is generally considered to be rectangular in the image, but maybe quadrilateral due to the different image intake angles. So this project used **Canny edge detection algorithm** combined with OpenCV contour search algorithm for license plate positioning. First, the canny algorithm for edge detection; and then binarization, and then use `cvFindContours` search contour, and finally from the contours found in accordance with the number of corners, the angle of the degree and the size of the contour to determine the rectangular position. The algorithm flow chart is shown in the following figure:

![](https://ws3.sinaimg.cn/large/006tNc79gy1fk2tql63m9j30eu0t0wg6.jpg)

![](https://ws1.sinaimg.cn/large/006tNc79gy1fk2txv0sdxj30zq0wyq90.jpg)



## <a name = "license-plate-segmentation"></a>License plate image segmentation

+ Redefine the boundary
  Converting color images to B&W. Since the edge of the license plate may have a certain white area after the binarization, and the processing of these areas will only waste time and resources, so to re-select the more appropriate boundaries
+ Area-based character segmentation
  According to the observation of the current mainstream license plate, including Chinese characters, each license plate has 7 characters, and each character occupies the size of the space is basically the same. In addition, there is a black dot between the second character and the third character, the horizontal width is about 1/20 of the license plate width.
+ Remove the extra parts of the license plate image 

![](https://ws2.sinaimg.cn/large/006tNc79gy1fk2u7jcetsj30k70lp0ud.jpg)

## <a name = "license-plate-recognition"></a>License plate recognition

Using the **minimum distance classifier** for character recognition.

![](https://ws2.sinaimg.cn/large/006tNc79gy1fk2u8e64m9j30k00bwq47.jpg)

![](https://ws1.sinaimg.cn/large/006tNc79gy1fk2u9hwn72j30vo07owfh.jpg)



# <a name = "parking-space-number-part"></a>Parking Space Number Part

Original Image ==> Preprocessing ==> Location and Extraction ==> ~~Segmentation~~ ==> Recognition

## <a name = "space-number-extraction"></a>Space number extraction

![](https://ws2.sinaimg.cn/large/006tNc79gy1fk2uax8rqcj30xg0awjw2.jpg)

![](https://ws3.sinaimg.cn/large/006tNc79gy1fk2uc4veqqj30y410qtcq.jpg)



## <a name = "space-number-recognition"></a>Space number recognition

![](https://ws2.sinaimg.cn/large/006tNc79gy1fk2ucpy6sbj30vs0dwmyb.jpg)

# <a name = "demo"></a>Demo

![](https://ws1.sinaimg.cn/large/006tNc79gy1fk2uh6x9wjj30wq0jq0vj.jpg)

# <a name = "conclusion"></a>Conclusion

License plate character recognition is the most crucial part of the license plate recognition system. We processed image with binarization, image smoothing and noise reduction. Using the license plate feature to position and extract license plate, then segmented license plate character, and also improved the segmentation method. Finally recognized the character through the character features to identify a part of the license plate of Chinese characters, letters and numbers.

However, there are still many deficiencies in the Chinese recognition, and if the license plate images are blurred,  or with complex background, etc., the license plate positioning accuracy is not very high. There are still some follow-up works to complete to make the system more perfect.









