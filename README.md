# Panorama_stitch-images
Stitching multiple images from surrounding area to generate its unbroken view called as "panorama"

Flow of the approach is as shown in figure below.
![image](https://user-images.githubusercontent.com/65898464/130512205-e9fbf537-d503-4dee-94d0-1c7dbe39d101.png)

I) Keypoints identification
Extract features using SIFT: Features that best matches in both the images are obtained using SIFT. The best matched features act as the basis for stitching.
Find keypoints and descriptors:The keypoints and descriptors for the images are then extracted to be stitched using SIFT detector.
![image](https://user-images.githubusercontent.com/65898464/130512554-398a1fac-cd7b-450c-85d2-bcb307681c02.png)

II) Matching descriptors (Bfmatcher and KNN match)
BFmatcher matches the most similar features and knnMatcher with k=2 gives 2 best matches for each descriptor. Some features that may be existing in many places of the image can mislead future operations. So, all the matches are filtered out to obtain the best ones by applying ratio test. Hamming distance is used as a measure of similarity between two feature descriptors.
![image](https://user-images.githubusercontent.com/65898464/130513106-ce23e870-3adb-4e40-bf27-5ce868f9aacd.png)

III) Finding homography
Homography is a transformation that maps the points in one image to the corresponding points in the other image. A homography matrix is needed to perform the transformation
and requires atleast 4 matches. It utilizes a robust estimation technique called Random Sample Consensus (RANSAC) which produces the right result even in the presence of large number of bad matches.

IV) Warping
Once an accurate homography has been calculated, the transformation can be applied to all pixels in one image to map it to the other image. This is done using the warpPerspective function in OpenCV.

V) Triming (Removing undesired portion)
Small portion from right of stitched image are trimed and cropped to remove the undesired black portion obtained after stitching.

Intermediate results
![image](https://user-images.githubusercontent.com/65898464/130513457-1ac9fc47-34a0-4564-9a65-fbfab1ab0181.png)

Final results
![image](https://user-images.githubusercontent.com/65898464/130513558-ce7f443b-038e-4cf5-95fa-10e2e33dd44e.png)
