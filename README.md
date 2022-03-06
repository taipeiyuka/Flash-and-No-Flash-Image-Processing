# Flash and No-Flash Image Processing

This application takes a flash and no-flash image pair to denoise and enhance details in the no-flash image.

## Overview
The design is based on the work of Petschnigg et al. [2]. There are three phases of the method, namely, denoising, detail transferring, and artifact detecting. Both the denoising and the detail transferring follow the steps described in the paper. For artifact detecting, we apply our own heuristic.

In the denoising phase, we apply joint-bilateral filter to the input. In the detail transfer phase, we divide the flash image by its bilateral filterred image to obtain the detail layer. We then multiply the detail layer with the denoised output.

The heuristic transforms the images to grey scale, blurs them with Gaussian kernel, normalizes and sets a threshold to detect shadows respectively, and marks pixels that are shadows in the flash image but not shadows in the no-flash image. (The threshold for the flash and no-flash shadow detection is 20% and 5% respectively.) The specularities are detected from the flash image where pixels have value greater than a threshold (245 in our implementation.)

For non-artifacts, we take the result of the denoised and detail transferred image, for pixels detected as artifacts, we can set it as the bilateral filtered no-flash image, or even blend the bilateral filtered no-flash image with the original no-flash image.

## Dataset
Flash and Ambient Illuminations Dataset [1]: http://yaksoy.github.io/faid/

The dataset contains images collected by iphone devices.

## Result
![cropped example of the result](https://github.com/taipeiyuka/Flash-and-No-Flash-Image-Processing/blob/main/Example/Plants_063_compare.png?raw=true)

## Reference
[1] Ya ̆gız  Aksoy,  Changil  Kim,  Petr  Kellnhofer,Sylvain Paris, Mohamed Elgharib, Marc Polle-feys, and Wojciech Matusik. A dataset of flashand ambient illumination pairs from the crowd.InProc. ECCV, 2018.

[2] Georg Petschnigg, Richard Szeliski, Maneesh Agrawala, Michael Cohen, Hugues Hoppe, and Kentaro Toyama. 2004. Digital photography with flash and no-flash image pairs. <i>ACM Trans. Graph.</i> 23, 3 (August 2004), 664–672. DOI:https://doi.org/10.1145/1015706.1015777


