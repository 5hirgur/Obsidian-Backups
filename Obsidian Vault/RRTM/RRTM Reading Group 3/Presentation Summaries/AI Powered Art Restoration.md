#RRTM 
Presentation by Aron Rihal on 05-11-2024

# Importance of Art Restoration 

- Cultural significance
- Preserving cultural heritage
- Deterioration over time

Traditional art restoration use highly skilled conservators using techniques such as cleaning, inpainting and structural repair. There is always a battle between remedying damage and preserving the artists intent. 

# Digital solutions for Art Restoration 

*Transforming Pixels into a Masterpiece*

## Proposed Solution
Using a DDCNN Distributed Denoising Convolutional Neural Networks
Based on Flexible Field-of-View Denoising Network FFDNet
Generative Adversarial Networks GANs were ignored due to introduction of new artifacts. 

### DDCNN

Breaking down images into smaller pieces, identifying patterns and shapes. Convolution layers, Pooling Layers and Fully connecting layers. 

You need a dataset to train this AI, they researchers use custom python program made using Selenium web scraper tool. 20,00 high res RGB images of a diverse range of art styles. Noise and deterioration is added digitally. 
Image deterioration : Custom python program used, not specified which. OpenCV was used.

### Measuring Performance

PSNR Peak Signal to Noise Ration and SSIM Structural Similarity .... are used. 
DDCNN gets a high PSNR and SSIM values. 

## Limitations

Computational resource requirements and potential scalability challenges for large data sets. 

They distorted their own images instead of training AI on actual damaged artworks, restored images were not completely free from noise something a conservator would strive to achieve. The model could take images before and after restoration by a restoration.

This paper did not talk about the parameters while the data for the model was being scraped. 

