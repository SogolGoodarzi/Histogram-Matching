# Histogram-Matching
### Image Histogram
The image histogram indicates the intensity distribution of an image. In other words, the image histogram shows the number of pixels in an image having a specific intensity value. As an example, assume a normal image with pixel intensities varying from 0 to 255. In order to generate its histogram we only need to count the number of pixels having intensity value 0, then 1 and continue to 255. In the following figure, we have a sample 5*5 image with pixel diversities from 0 to 4. In the first step for generating the histogram, we create the Histogram Table, by counting the number of each pixel intensities. Then we can easily generate the histogram by creating a bar chart based on the histogram table.

![image](https://user-images.githubusercontent.com/125180530/219502667-bbdb2402-ff6c-4ab5-8af6-68134a4964bd.png)

Most of the time when we create a histogram, we normalize the histogram by dividing the number of pixels with each intensity value by the normalizing factor which is the multiplication of the image width and image height.

### Equalize an Image Histogram
Histogram equalization is commonly used in order to enhance the contrast of the image. Accordingly, this technique can’t guarantee to always improve the quality of the image. Calculating CDF (cumulative distributive function) is a common way to equalize the histogram of an image. In the figure below, we have calculated the CDF for the sample image that we created in the previous figure. Furthermore, we show the equalized histogram of the previous sample.

![image](https://user-images.githubusercontent.com/125180530/219503072-32a0ae6d-26d1-4aa1-9627-cfe8ae159973.png)

Here are 3 different images taken and used as examples. As shown in the following figure, for the first image the histogram shows that the number of pixels with low intensity is more than the brighter pixels. The situation is totally reversed for the second image, where the density of the brighter pixels is much more than the darker ones. The third image seems to have a semi-normal histogram.

![image](https://user-images.githubusercontent.com/125180530/219506394-30da8285-dfd3-4ccc-95c5-e01025bf0a2a.png)

### Histogram Matching
Assume we have two images and each has its specific histogram. So we want to answer this question before going further, is it possible to modify one image based on the contrast of another one? And the answer is YES. In fact, this is the definition of histogram matching. In other words, given images A, and B, it is possible to modify the contrast level of A according to B.

Histogram matching is useful when we want to unify the contrast level of a group of images. In fact, Histogram equalization is also can be taken as histogram matching, since we modify the histogram of an input image to be similar to the normal distribution.

In order to match the histogram of images A and B, we need to first equalize the histogram of both images. Then, we need to map each pixel of A to B using the equalized histograms. Then we modify each pixel of A based on B.

Let’s clarify the above paragraph using the following example, in the following figure:

![image](https://user-images.githubusercontent.com/125180530/219504287-eee364ff-d8bb-452f-ac0f-6f322e5b1dd4.png)

We have image A as the input image and Image B as the target image. We want to modify the histogram of A, based on the distribution of B. In the first step, we calculate both the histogram and the equalized histogram of both A, and B. Then we need to map each pixel of A, based on the value of its equalized histogram to the value of B. So, for example for pixels with the intensity level of 0 in A, the corresponding value of A equalized histogram is 4. Now, we take a look at the B equalized histogram and find the intensity value corresponding to 4, which is 0. So we map the 0 intensity from A to 0 from B. We continue for all intensity values of A. If there is no map from the equalized histogram of A to B, we just need to pick the nearest value.

An example of histogram matching and its result is shown in the figure below:

![image](https://user-images.githubusercontent.com/125180530/219504541-c08eaf6f-aa49-4eaf-8a29-9624e5b75ffe.png)

Now we implement this algorithm for the following images and match them:

#### Reference Image:
![Reference](https://user-images.githubusercontent.com/125180530/219504680-7c29ab0d-996b-4eb4-a634-70d1c4543c4f.jpg)

#### Source Image:
![Source](https://user-images.githubusercontent.com/125180530/219505262-7d36b173-6ed6-44cc-9d4e-20bff1222cad.jpg)

#### Matched Image:
![Matched_Image](https://user-images.githubusercontent.com/125180530/219505407-19bab706-3123-40d4-b84c-1cd896da61c5.jpg)
