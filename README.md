# Introduction
PAP stands for Power,Area,Performance.The PAP analysis has become the De facto standard for measuring the efficiency of a hardware system for a target function. For the purpose of implementing a Neural Network on some hardware, like a DSP, analysis of these parameters becomes extremely essential.This will help us in optimizing one or the other parameter so that the system works efficiently in real time. Autonomous Driver Assistance System uses neural networks trained for various tasks such as Lane Detection, traffic sign Detection & Recognition, Pedestrian Detection etc.The target hardware that is selected to implement the neural network must be efficient in terms of power consumed,performance and area consumed.
# Installing NVIDIA DIGITS:-  
The ConvNet(AlexNet) was trained for traffic sign recognition task by performing transfer learning using NVIDIA DIGITS web based API.In all the image dataset consisted of 43 classes of german traffic signs. The installation steps for DIGITS are mentioned on this [link](https://github.com/patilninad/DIGITS).  
The framework used for training was caffe. The purpose of choosing Caffe was the Xtensa Neural Network Compiler requires .caffemodel as input for performing further optimizations. Hence once the model was trained a .caffemodel file was generated which contained the weights.  
# Target System:-  
Cadence's Tensilica Vision P6 DSP was choosen as the target hardware, due to the licence availablity of this hardware with my institution, on which the neural network was implemented.
# Optimizations:-
Before actually implementing the neural network first it needs to be optimized for the target hardware.Optimization refers to converting to fixed point code without the loss of accuracy and also some other code optimizations with respect to the hardware.The compiler gives only Performance parameter as output along with the optimized code.For this task Cadence's Xtensa Neural Network compiler software was used.The optimized code is then sent to Xtensa Processor Generator which generates the RTL equivalent code of the DSP implementing the Traffic Sign Recognition system.This RTL code can then finally be dumped on a FPGA for performing power and area analysis.    
# Summary of Softwares used:  
1) NVIDIA DIGITS - For Training AlexNet.
2) Cadence's Xtensa Neural Network Compiler - For generating optimized code for target hardware and performance report(in fps).
3) Cadence's Xtensa Processor Generator - For generating RTL code for Xtensa architecture based Vision P6 processor.
4) Xilinx FPGA and ISE design suit/VIVADO - for dumping code on the FPGA.  
# Xtensa Neural Network Compiler:-  
# Final output given by compiler: Performance report in terms of FPS
![](https://github.com/patilninad/Training/blob/master/PerformanceReport.jpeg)  
# Power and Area Analysis:-  
The RTL code obtained is dumped onto the FPGA. Once dumped we can find out how much area of the FPGA it is occupying in terms of number/percentage of CLB's.
