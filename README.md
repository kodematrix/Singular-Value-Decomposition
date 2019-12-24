# SVD Image compression
SVD minimizes the size of an image in bytes to an acceptable level of quality. This means that you are able to store more images in the same disk space as compared to before. Image compression takes advantage of the fact that only a few of the singular values obtained after SVD are large. You can trim the three matrices based on the first few singular values and obtain a compressed approximation of the original image. Some of the compressed images are nearly indistinguishable from the original by the human eye.

*Let's take an RGB image of a butterfly to perform Singular Value Decomposition*

| Matrix Image |
| ------------- |
|![ButterFly](https://user-images.githubusercontent.com/54346057/71386585-da040f80-25bc-11ea-87ba-5b8f86014e67.JPG)|

*Splittig image by color and assigning to a variable*
```{r}
red <- matrix(image@red, nrow = image@size[1], ncol = image@size[2])
green <- matrix(image@green, nrow = image@size[1], ncol = image@size[2])
blue <- matrix(image@blue, nrow = image@size[1], ncol = image@size[2])
```


*By applying SVD to red matrix, it yields one diagonal and two orthogonal matrices*
```{r}
red_svd <- svd(red)
d <- red_svd$d  
u <- red_svd$u
v <- red_svd$v
```



*Next I used Mathematica to compute the singular value decomposition of the underlying matrix of numbers. When I keep just one term. We can compare the images for singular column values.* 

| 10 Singular Values | 20 Singular Values  |
| ------------- |:-------------:|
| ![b10](https://user-images.githubusercontent.com/54346057/71386587-da9ca600-25bc-11ea-94ac-3eefdab2a060.JPG)| ![b20](https://user-images.githubusercontent.com/54346057/71386588-da9ca600-25bc-11ea-962f-d946142f7926.JPG)|




| 30 Singular Values        | 50 Singular Values | 
| ------------- |:-------------:| 
| ![b30](https://user-images.githubusercontent.com/54346057/71386583-da040f80-25bc-11ea-9712-cb24df089412.JPG)| ![b50](https://user-images.githubusercontent.com/54346057/71386584-da040f80-25bc-11ea-8d9e-ca900cb3a1ec.JPG)| 

*Now the last column i.e.,. Singular Values with 50 image is nearly perfect. Compression is small but we get a very good picture and still some substantial savings. we have reduced the number of columns and hence we need very less memory to show this image compared to the space needed to represent the original red color matrix.*
