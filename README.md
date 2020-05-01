# Introduction
PAP stands for Power,Area,Performance.Analysis of these parameters is essential for selecting a neural network and the corresponding efficient target hardware.This PAP analysis has become the De facto standard for measuring the efficiency of a hardware system for a target function.Autonomous driving system uses neural networks trained for traffic sign recognition.The target hardware that is selected to implement the neural network must be efficient in terms of power consumed,performance(in terms of no of cycles).Traffic sign recognition will become real time once these parameters are taken care of.  
# Installing NVIDIA DIGITS:-  
The ConvNet(AlexNet) was trained by performing transfer learning using NVIDIA DIGITS.The installation steps for DIGITS are mentioned on this [link](https://github.com/patilninad/DIGITS).  
The framework used for training was caffe.Hence once the model was trained a .caffemodel file was generated which contained the weights.  
# Target System:-  
Cadence's Tensilica Vision P6 DSP was choosen as the target hardware, due to the licence availablity of this hardware with my institution, on which the neural network was implemented.The PAP parameters were calculated for P6 DSP.
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
# Work in progress - power and area analysis is remaining.
