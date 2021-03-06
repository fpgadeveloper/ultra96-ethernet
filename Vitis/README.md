Vitis Project files
===================

### How to build the Vitis workspace

In order to make use of these source files, you must first generate
the Vivado project hardware design (the bitstream) and export the hardware.
Check the `Vivado` folder for instructions on doing this from Vivado.

Once the bitstream is generated and exported, then you can build the
Vitis workspace using the provided `build-vitis.tcl` script.

### Scripted build

The Vitis directory contains a `build-vitis.tcl` script which can be run to automatically
generate the Vitis workspace. Windows users can run the `build-vitis.bat` file which
launches the Tcl script. Linux users must use the following commands to run the build
script:
```
cd <path-to-repo>/Vitis
/<path-to-xilinx-tools>/Vitis/2020.2/bin/xsct build-vitis.tcl
```

The build script does three things:

1. Prepares a local software repository containing a modified version of lwIP library,
required by the echo server example application. This local software repository is
a folder called `embeddedsw` that is created inside the `Vitis` folder/workspace.
2. Adds the modified sources from the Git repo's `EmbeddedSw` directory to the local 
software repository `Vitis/embeddedsw`.
3. Generates a lwIP Echo Server example application for each exported Vivado design
that is found in the Git repo's `Vivado` directory. Most users will only have one exported
Vivado design.

### Run the application

1. Open Xilinx Vitis.
2. Power up your hardware platform and ensure that the JTAG is
connected properly.
3. Select Xilinx Tools->Program FPGA. You only have to do this
once, each time you power up your hardware platform.
4. Click Run from the toolbar to run your application. You can modify the code
and click Run as many times as you like, without going through
the other steps.

### How to change the Ethernet port targetted by the application

The echo server example design currently can only target one Ethernet port at a time.
Selection of the Ethernet port can be changed by modifying the defines contained in the
`platform_config.h` file in the application sources. Set `PLATFORM_EMAC_BASEADDR`
to one of the following values:

For designs using the GEMs:
* Port 0: `XPAR_XEMACPS_0_BASEADDR`
* Port 1: `XPAR_XEMACPS_1_BASEADDR`
* Port 2: `XPAR_XEMACPS_2_BASEADDR`
* Port 3: `XPAR_XEMACPS_3_BASEADDR`

For designs using AXI Ethernet:
* Port 0: `XPAR_AXIETHERNET_0_BASEADDR`
* Port 1: `XPAR_AXIETHERNET_1_BASEADDR`
* Port 2: `XPAR_AXIETHERNET_2_BASEADDR`
* Port 3: `XPAR_AXIETHERNET_2_BASEADDR`

