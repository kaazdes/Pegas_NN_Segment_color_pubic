# **Crop segmentation in the field**

The materials contain the experience of applying synthetic data in Deep Learning problems on the example of the test part of the big problem of navigation of agricultural machines in the field. 

Task: segmenting field photos into two classes of «plants» and «earth», using DL algorithms.

Images are obtained from the video stream of the camera, which is fixed to the machine (https://pegas-agro.ru/):

![Aspose Words c763260b-02b7-4ab1-98ae-11cabcd55d11 001](https://github.com/kaazdes/Pegas_NN_Segment_color_pubic/assets/78611665/9ff7e047-3083-4f92-a575-1485a8084a88)

The machine is used night and day on fields with different plants:

![Aspose Words c763260b-02b7-4ab1-98ae-11cabcd55d11 002](https://github.com/kaazdes/Pegas_NN_Segment_color_pubic/assets/78611665/d152622e-727c-4379-9379-4cfe2e7df56c)

Training NN with a teacher implies a fairly large set of tagged data: 

![Aspose Words c763260b-02b7-4ab1-98ae-11cabcd55d11 003](https://github.com/kaazdes/Pegas_NN_Segment_color_pubic/assets/78611665/acccea3e-2159-453f-b4c0-0cdfa7cc0b90)

This task is very time-consuming and financially costly, even if you use pretrain NN.
In this paper the possibility of using generated artificial data - photos is considered. Different plants, rows, ground their different configurations are generated in the image.  This is the artificial data. On the NVIDIA website there is an interesting publication on this topic «What Is Synthetic Data?». (Link for interested https:/blogs.nvidia.com/blog/what-is-synthetic-data/ ).  The basic idea is not to mark data manually (if any) but to synthesize it. NVIDEA provides a developed tool for this. Teamwork with my allowed to make a prototype of the simplest generator that generates a field picture and mask (Friends: Sergey Murin  - programmer and developer of control systems and Nastya Murina - graphic designer):  
![Aspose Words c763260b-02b7-4ab1-98ae-11cabcd55d11 004](https://github.com/kaazdes/Pegas_NN_Segment_color_pubic/assets/78611665/02ad4443-c996-4e3e-b5b1-740617e3a402)

And with the process of augmentation

![Aspose Words c763260b-02b7-4ab1-98ae-11cabcd55d11 005](https://github.com/kaazdes/Pegas_NN_Segment_color_pubic/assets/78611665/520bf090-4775-45c4-a46a-f67bcbe4bc75)

Folder structure

![Aspose Words c763260b-02b7-4ab1-98ae-11cabcd55d11 006](https://github.com/kaazdes/Pegas_NN_Segment_color_pubic/assets/78611665/d89de544-a1f2-44bf-b7df-5335a3141690)

Networks such as SegNet, U-net, Resnet, Deplabv3 were considered. It was interesting to see what algorithms could do with synthetic data. For this reason, the initialization of NN was accidental, meaning NN were not pretrain.
All the obtained variants of the networks were trained and changed before reaching the characteristic values: when increasing the number of learning epochs, the accuracy curve «validation» strive for the accuracy curve «learning», which indicates that there is no effect of retraining the network:

![Aspose Words c763260b-02b7-4ab1-98ae-11cabcd55d11 007](https://github.com/kaazdes/Pegas_NN_Segment_color_pubic/assets/78611665/08ce26d0-217f-42b8-9224-021bef022102)

Some results are given in tabular form:

![Aspose Words c763260b-02b7-4ab1-98ae-11cabcd55d11 008](https://github.com/kaazdes/Pegas_NN_Segment_color_pubic/assets/78611665/723d77b4-f25b-4e06-bb16-1596e63d2bf2)

Since plant rows cover more than 30% of the image area, the accuracy parameter quite satisfactorily conveys the quality of the segmentation. And for all networks, the accuracy is higher than 92%.  The number of parameters of each network can be said to be very small. This is another advantage of networks trained for specific tasks. 
And now let’s see,  what is a neural network trained on artificial data. How does it recognize real data?:

![Aspose Words c763260b-02b7-4ab1-98ae-11cabcd55d11 009](https://github.com/kaazdes/Pegas_NN_Segment_color_pubic/assets/78611665/eb363e18-dd4f-445c-b622-fac813ea2da4)

examples:

![Aspose Words c763260b-02b7-4ab1-98ae-11cabcd55d11 010](https://github.com/kaazdes/Pegas_NN_Segment_color_pubic/assets/78611665/092575c4-8510-4b5b-878c-626aa2eaa1f9)

Analysis of the quality of the obtained segmented images showed the possibility of applying the strategy of learning the neural network on artificial data. Further work on the project is ongoing

An example code is better to open in GoogleColab, where there is a possibility of navigation and elements of the code architecture.
