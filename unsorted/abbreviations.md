| Abbreviation             | Definition                                                                                                                                                                                                                                                                                                                                                                                                       |
| ------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| SiLU                     | Sigmoid Linear Unit, aka. Swish                                                                                                                                                                                                                                                                                                                                                                                  |
| DFL                      | Distribution Focal Loss – Focal Loss has proven to be effective at balancing loss by increasing the loss on hard-to-classify classes                                                                                                                                                                                                                                                                             |
| BoF                      | Bag of Freebies are those methods which change the training, not the inference PANNet = Path Aggregation Network                                                                                                                                                                                                                                                                                                 |
| SAT                      | Self Adversarial Training                                                                                                                                                                                                                                                                                                                                                                                        |
| CSP                      | Cross-Stage Partial Connection                                                                                                                                                                                                                                                                                                                                                                                   |
| CBN                      | Cross Batch Normalization – takes mean and standard deviation of the four last batches                                                                                                                                                                                                                                                                                                                           |
| CmBN                     | Cross Iteration Mini Batch Normalization – takes CBN further, assumes four batches inside a single batch                                                                                                                                                                                                                                                                                                         |
| SPP                      | Spatial Pyramid Pooling, increases the receptive field                                                                                                                                                                                                                                                                                                                                                           |
| SENet                    | Squeeze and Excitation Network, finds which channel are more/less important in a feature map                                                                                                                                                                                                                                                                                                                     |
| SAM                      | Special Attention Module                                                                                                                                                                                                                                                                                                                                                                                         |
| IDD                      | Independent and identically distributed data                                                                                                                                                                                                                                                                                                                                                                     |
| Non-IDD                  | Non Independent and identically distributed data                                                                                                                                                                                                                                                                                                                                                                 |
| NICO                     | Non-IID Image dataset with contexts                                                                                                                                                                                                                                                                                                                                                                              |
| IoU                      | Intersection over Union                                                                                                                                                                                                                                                                                                                                                                                          |
| Precision                | Relevant Retrieved / Retrieved                                                                                                                                                                                                                                                                                                                                                                                   |
| Recall                   | Relevant retrieved / Relevant                                                                                                                                                                                                                                                                                                                                                                                    |
| AP                       | Average Precision: It measures the accuracy by calculating the area under the precision-recall curve.                                                                                                                                                                                                                                                                                                            |
| AP@[0.5:0.95]            | IoU between 50\% and 95\% taken into account                                                                                                                                                                                                                                                                                                                                                                     |
| mAP                      | Averaged over all classes                                                                                                                                                                                                                                                                                                                                                                                        |
| APsmall                  | AP for small objects (area < 322)                                                                                                                                                                                                                                                                                                                                                                                |
| APmedium                 | AP for medium objects (322 < area < 962)                                                                                                                                                                                                                                                                                                                                                                         |
| APlarge                  | AP for large objects (area > 962)                                                                                                                                                                                                                                                                                                                                                                                |
| Residual                 | $ Y = F(x) + x $                                                                                                                                                                                                                                                                                                                                                                                                 |
| Image Segmentation       | things (countable, e.g. birds) vs stuff (not countable, e.g. grass)                                                                                                                                                                                                                                                                                                                                              |
| Semantic Segmentation    | Studies stuff (e.g. SegNet, U-Net, DeconvNet), measurement: IoU                                                                                                                                                                                                                                                                                                                                                  |
| Instance Segmentation    | Studies things (e.g. Masked R-CNN, Faster R-CNN, PANet, YOLCAT), measurement: AP                                                                                                                                                                                                                                                                                                                                 |
| Panoptic Segmentation    | Studies both (most models are based on Mask R-CNN)                                                                                                                                                                                                                                                                                                                                                               |
| Padding                  | Padding is the process of adding extra pixels around the input image or feature map. It is commonly used in convolutional neural networks to preserve spatial dimensions and prevent information loss at the edges of the image. Padding can be done with zeros (zero-padding) or with values from the original image (reflective padding or symmetric padding).                                                 |
| Stride                   | Stride refers to the number of pixels the convolutional kernel moves at each step during the convolution operation. A stride of 1 means the kernel moves one pixel at a time, while a stride of 2 means the kernel moves two pixels at a time. Stride affects the output size of the feature map, as well as the amount of computation required.                                                                 |
| Pooling                  | Pooling is a downsampling operation that reduces the spatial dimensions of the input feature map. It is commonly used to reduce the computational complexity of the network and to extract the most important features. The most common types of pooling are max pooling and average pooling, which take the maximum or average value within a pooling window, respectively.                                     |
| Batch Normalization      | Batch normalization is a technique that normalizes the activations of each batch in a neural network. It helps to stabilize and speed up the training process by reducing internal covariate shift and allowing higher learning rates. Batch normalization is commonly used in deep neural networks.                                                                                                             |
| Dropout                  | Dropout is a regularization technique that randomly sets a fraction of the input units to zero during training. It helps to prevent overfitting by reducing the co-adaptation of neurons and encouraging the network to learn more robust features. Dropout is commonly used in deep neural networks.                                                                                                            |
| Skip Connection          | Skip connection, also known as residual connection, is a technique that adds the input of a layer to the output of a subsequent layer. It allows the network to learn residual functions, which can help to alleviate the vanishing gradient problem and improve the flow of gradients during training. Skip connections are commonly used in deep residual networks (ResNet).                                   |
| Upsampling               | Upsampling is the process of increasing the spatial dimensions of an image or feature map. It is commonly used in tasks such as image super-resolution, semantic segmentation, and generative modeling. Upsampling can be done using techniques such as transposed convolution, nearest-neighbor interpolation, or bilinear interpolation.                                                                       |
| Mosaic Data Augmentation | Mosaic data augmentation is a technique used in computer vision tasks, such as object detection, to improve the performance of deep learning models. It involves combining multiple images into a single mosaic image and using it as training data. Mosaic data augmentation helps to increase the diversity and complexity of the training data, leading to better generalization and robustness of the model. |