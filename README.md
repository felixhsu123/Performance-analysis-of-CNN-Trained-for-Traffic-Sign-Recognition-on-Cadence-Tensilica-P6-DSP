# Introduction
PAP stands for Power,Area,Performance.The PAP analysis has become the De facto standard for measuring the efficiency of a hardware system for a target function. For the purpose of implementing a Neural Network on some hardware, like a DSP, analysis of these parameters becomes extremely essential.This will help us in optimizing one or the other parameter so that the system works efficiently in real time. Autonomous Driver Assistance System uses neural networks trained for various tasks such as Lane Detection, traffic sign Detection & Recognition, Pedestrian Detection etc.The target hardware that is selected to implement the neural network must be efficient in terms of power consumed,performance and area consumed.  
# Summary of Softwares used:  
1)NVIDIA DIGITS - For training AlexNet.  
2)Xtensa Neural Network Compiler - For generating optimized,fixed-point code for target DSP.   
3)Xtensa Xplorer - Viewing performance report.   
4)Xtensa Processor Generator - For generating RTL code for Xtensa architecture based Vision P6 processor.
# Dataset: -  
The dataset under consideration was that of german traffic signs. The dataset was taken from the website http://benchmark.ini.rub.de/?section=home&subsection=news    
# Trained Model: -   
The caffe trained model for GTSRB can be downloaded from https://github.com/magnusja/GTSRB-caffe-model  
# Optimizations:-
Before actually implementing the neural network first it needs to be optimized for the target hardware.Optimization refers to converting to fixed point code without the loss of accuracy and also some other code optimizations with respect to the hardware.The compiler gives only Performance parameter as output along with the optimized code.For this task Cadence's Xtensa Neural Network compiler software was used.The optimized code is then sent to Xtensa Processor Generator which generates the RTL equivalent code of the DSP implementing the Traffic Sign Recognition system.This RTL code can then finally be dumped on a FPGA for performing power and area analysis.      
# Target System:-  
All the software's used are Cadence's proprietary software's.Cadence's Tensilica Vision P6 DSP was choosen as the target hardware, due to the licence availablity of this hardware with my institution, on which the neural network was implemented.
# Installing Nvidia Digits:-  
The ConvNet(AlexNet) was trained for traffic sign recognition task by performing transfer learning using NVIDIA DIGITS web based API.In all the image dataset consisted of 43 classes of german traffic signs. The installation steps for DIGITS are mentioned on this [link](https://github.com/patilninad/DIGITS).  
The framework used for training was caffe. The purpose of choosing Caffe was the Xtensa Neural Network Compiler requires .caffemodel as input for performing further optimizations. Hence once the model was trained a .caffemodel file was generated which contained the weights.  
# Xtensa Neural Network Compiler:-   
The purpose of the Xtensa Neural Network Compiler (XNNC) is to convert a floating-point
Convolutional Neural Network (CNN) into an optimized, fixed-point solution for Xtensa
processors.  
XNNC input:-  
1).prototxt/.caffemodel file  
2)Calibration and validation image set    
XNNC output:-  
1)Optimized CNN code for target Xtensa DSP    
2)Accuracy and performance report    
The XNNC undergoes a multi-stage process to generate an optimized version of your neural
network. In this process, it analyzes the layer activations of the floating-point network, and evaluates quantization profiles (min/max ranges of the outputs from each layer) across a range of empirical distributions observed in the calibration and validation image sets supplied by the user.Based on this evaluation, scaling factors for fixed-point conversion of each layer are determined.The XNNC then takes these quantization parameters and generates optimized, fixed-point code for your network.  
The generated code is provided in the form of a workspace which can be imported into Xtensa Xplorer for viewing accuracy and performance parameters.  
XNNC supports classification, segmentation, and object detection networks as well
as custom layers.XNNC supports all major CNN architectures.     
# Xtensa Xplorer IDE: -  
The XNNC undergoes a multi-stage process to generate an optimized version of the CNN. In this process, it analyses the layer activations of the floating-point network and evaluates quantization profiles (min/max ranges of the outputs from each layer) across a range of experimental distributions observed in the calibration and validation image sets supplied by the user. Based on this evaluation, scaling factors for fixed-point conversion of each layer are determined. The XNNC then takes these quantization parameters and generates an optimized, fixed-point neural network. The optimized code along with other supporting software files needed for the application is provided in the form of a workspace. This workspace file is generated with a .xws extension. This workspace file can then be imported into Xtensa Xplorer to get a performance report. The Xtensa Xplorer IDE serves as the graphical user interface (GUI) for the entire design process[7]. From the Xtensa Xplorer IDE, designers with existing application software can profile their application, identify hot spots, decide on configuration options, add instructions and execution units to optimize performance, and then generate a new processor. This puts flexibility directly into the hands of the designer with a tool that integrates software development, processor optimization, and multi-processor SoC architecture in one IDE. Xtensa Xplorer IDE is a part of the Cadence Tensilica Xtensa SDK. The Tensilica Xtensa SDK provides a comprehensive collection of code generation and analysis tools that speeds the application software development process. Xtensa Xplorer IDE can be configured for analysing the performance on the Vision P6 DSP, by importing the P6 DSP core from XPG. Once the Xtensa IDE is configured for Vision P6 DSP then the performance report of the neural network can be generated by importing the previously generated workspace from XNNC. The Xtensa Processor Generator creates a complete hardware design with matching software tools, including a mature, world-class compiler, a cycle-accurate SystemC-compatible ISS, and the full industry-standard GNU toolchain.
# Cadence XNNC output: -  
The complete files generated at the output of XNNC can be found in this link. https://drive.google.com/drive/folders/1pDJtDUQFtld74pogilrqQNa-C157GLVH?usp=sharing
# Cadence Xtensa Xplorer output(Performance report in terms of FPS):-
![](https://github.com/patilninad/Performance-analysis-of-ConvNet-trained-for-Traffic-Sign-Recognition-on-Cadence-Tensilica-P6-DSP/blob/master/PerformanceReport.jpeg)  
__________________________________________________________________________________________  
Performance came out to be 116.54 frames per second @ 1000.00MHz system clock.   
This gives us an idea of the performance of the neural network when it will be actually implemented on the FPGA/ASIC for real time recognition task.  
Some further optimization facilities are also available within the software that optimizes the networks performance/accuracy.    
  
