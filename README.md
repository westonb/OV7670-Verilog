# OV7670-Verilog
Verilog modules required to get the OV7670 camera working on the Nexys4-DDR board for MIT's 6.111 Digital Systems Labratory

# Introduction
I highly recommend you first read the data sheet for the camera module: http://www.voti.nl/docs/OV7670.pdf
In summary OV7670 utilizes a 8 bit parallel bus to output video data along with HREF and VSYNC signals to synchronize frames. A input clock is required which is used as a reference for generating the output pixel output clock that the data is aligned to. 

# Configuration 
The OV7670 requires configuration to output the correct color format with the proper color balance. This is done over SCCB which is a copy of the I2C protocol. This interface is over the camera SIOC and SIOD pins. A configuration module is provided for you which will configure the camera with reasonable settings for RGB565 data output. 

# Camera Data Capture
A module is provided which interfaces with the 8 bit parallel and the HREF/VSYNC signals to output pixel data, a pixel valid signal, and a frame done signal. This can be interfaced with a frame buffer of your own creation. To fit on the Nexys4-DDR BRAM memory you will have to downsample the image in either terms of size or the size of the stored pixel. It is also possible, although complicated to full frames in the on board DDR memory.

# Hardware Configuration
The OV7670 outputs its own pixel clock (PCLOCK) that is synchronized with its data output. This must be connected to the FPGA and you must capture the data in this clock domain. Only some PMOD pins are capable of being used as a clock input. The PCLOCK pin must connect to (JB10) for the right PMOD connectors. If you have two cameras you should be able to get away with using one PCLOCK to capture the data from both as long as you connect the clock input from the cameras to the same source. Any of the other PMOD pins can be used for the other camera signals. The 3.3V supply for the camera can also be sourced from the PMOD connectors.

# SCCB Pullup Resistors
The SCCB interface for the camera requires pull up resistors. You need to solder 4.7K resistors from the SIOD and SIOC pins on the camera to the 3.3V supply. You can do this yourself or have the staff in the EDS help you. 

