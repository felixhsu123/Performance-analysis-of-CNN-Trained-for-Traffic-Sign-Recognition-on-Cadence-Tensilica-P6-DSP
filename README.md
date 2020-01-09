# PAP analysis of ConvNets trained for Traffic sign classification on Cadence's Tensilica Vision P6 DSP  
PAP stands for Power,Area,Performance.Analysis of these parameters is essential for selecting a neural network and the corresponding efficient target hardware.
The ConvNet(AlexNet) was trained by performing transfer learning using NVIDIA DIGITS.The installation steps for DIGITS are mentioned on this [link](https://github.com/patilninad/DIGITS).  
The framework used for training was caffe.Hence once the model was trained a .caffemodel file was generated which contained the weights.  
Cadence's Tensilica Vision P6 DSP was choosen as the target hardware on which the neural network was implemented.The PAP parameters were calculated for P6 DSP as target hardware.Before actually implementing the neural network it needs to be optimized for the target hardware.This compiler also gives PAP parameters as output.For this task Cadence's Xtensa Neural Network compiler was used.The optimized code is then sent to Cadence's server which generates it's verilog code.This verilog code can then finally be implemented on a FPGA.

