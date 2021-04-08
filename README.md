# OpenLANE-Sky130-Workshop









<!-- PROJECT LOGO -->
<br />
<p align="center">
  <a href="https://user-images.githubusercontent.com/59030612/113806079-ac01fa80-972f-11eb-8ac4-296657b21b23.png">
    <img src="https://user-images.githubusercontent.com/59030612/113806079-ac01fa80-972f-11eb-8ac4-296657b21b23.png" alt="Logo" width="800" height="400">
  </a>

 

  
</p>



<!-- TABLE OF CONTENTS -->
## Table of Contents

* [OpenLANE Overview](#OpenLANE-Overview)
  * [Installation](#Installation)
* [The OpenLANE Architecture](#The-OpenLANE-Architecture)
  * [Design Stages](#Design-stages)
* [Day 1 Inception of open source EDA, OpenLANE and Sky130 PDK](#Day-1-Inception-of-open-source-EDA,-OpenLANE-and-Sky130-PDK)
  * [How to talk to computers](#How-to-talk-to-computers)
  * [SoC design and OpenLANE](#SoC-design-and-OpenLANE)
* [Day 2 Good floorplan vs bad floorplan and introduction to library cells](#Day-2-Good-floorplan-vs-bad-floorplan-and-introduction-to-library-cells)
  * [Concepts](#Concepts)
  * [Lab Exercises](#Lab-Exercises)
  




<!-- ABOUT THE PROJECT -->
## OpenLANE Overview

OpenLANE is an automated RTL to GDSII flow based on several components including OpenROAD, Yosys, Magic, Netgen, Fault, OpenPhySyn, CVC, SPEF-Extractor, CU-GR, Klayout and custom methodology scripts for design exploration and optimization. The flow performs full ASIC implementation steps from RTL all the way down to GDSII - this capability will be released in the coming weeks with completed SoC design examples that have been sent to SkyWater for fabrication.


### Installation

For a complete step in installing OpenLANE, please follow steps at https://github.com/efabless/openlane.



<!-- GETTING STARTED -->
## The OpenLANE Architecture

The figure below shows the OpenLANE architecture
<p align="center">
  <a href="https://github.com/efabless/openlane/blob/master/docs/_static/openlane.flow.1.png">
    <img src="https://github.com/efabless/openlane/blob/master/docs/_static/openlane.flow.1.png" alt="Logo" width="500" height="400">
  </a>

 

  
</p>

### Design Stages

OpenLANE flow consists of several stages. By default all flow steps are run in sequence. Each stage may consist of multiple sub-stages.

    Synthesis
        yosys - Performs RTL synthesis
        abc - Performs technology mapping
        OpenSTA - Pefroms static timing analysis on the resulting netlist to generate timing reports
    Floorplan and PDN
        init_fp - Defines the core area for the macro as well as the rows (used for placement) and the tracks (used for routing)
        ioplacer - Places the macro input and output ports
        pdn - Generates the power distribution network
        tapcell - Inserts welltap and decap cells in the floorplan
    Placement
        RePLace - Performs global placement
        Resizer - Performs optional optimizations on the design
        OpenPhySyn - Performs timing optimizations on the design
        OpenDP - Perfroms detailed placement to legalize the globally placed components
    CTS
        TritonCTS - Synthesizes the clock distribution network (the clock tree)
    Routing
        FastRoute - Performs global routing to generate a guide file for the detailed router
        CU-GR - Another option for performing global routing.
        TritonRoute - Performs detailed routing
        SPEF-Extractor - Performs SPEF extraction
    GDSII Generation
        Magic - Streams out the final GDSII layout file from the routed def
        Klayout - Streams out the final GDSII layout file from the routed def as a back-up
    Checks
        Magic - Performs DRC Checks & Antenna Checks
        Klayout - Performs DRC Checks
        Netgen - Performs LVS Checks
        CVC - Performs Circuit Validity Checks

For more information on openLANE, please refer to these resources:
https://github.com/efabless/openlane 
https://www.youtube.com/watch?v=EczW2IWdnOM
<!-- DAY 1 -->
## Day 1 - Inception of open-source EDA, OpenLANE and Sky130 PDK
### How to talk to computers 
This section is an introduction to computers and chips with related terms and concepts. It covers:
 1. Introduction to QFN-48 Package, chip, pads, core, die and IPs
 2. Introduction to RISC-V \
 This is a brief introcution of the RISC-V ISA(Instruction Set Architecture).
 3. From Software Applications to Hardware\
 This sub-topic gives a brief overview on the processes such as linking, compilation in transforming user-coded application programs to hardware readable codes.
### SoC design and OpenLANE
This sub-section gives a detailed overiview of OpenLANE and how its flow works. In addition, it discusses the tools that are incorporated in OpenLANE flow which are used for the end to end RTL to GDSII. The official github page for OpenLANE (https://github.com/efabless/openlane ) gives a detailed description and further links to pages for further study on this topic.
### Get familiar to open-source EDA tools
This sub-section starts from describing the directory structure of OpenLANE in detail. The figure below shows the directory structure. 
I did all the experiments with an OpneLANE implementation on my personal workstation.

![Image description](https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Images/Directory%20structure.png)
<br />

The initialization of OpenLANE is shown in figure below.
  <p align="left">
  <a href="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Images/initialization.png">
    <img src="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Images/initialization.png" alt="Logo" width="400" height="300">
  </a> 
    <br />
Then the preparation step for using OpenLANE follows which is used mainly to prepare the environment for the upcoming tasks as shown below.Here we followed 3 steps:<br />
  1. use command ./flow.tcl -interactive to run OpenLANE in interactive mode.<br />
  2. use command package require openlane 0.9 <br />
  3. use command prep -design <design_name>, which is picorv32a in our case <br />
    <p align="left">
  <a href="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Images/preparation.png">
    <img src="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Images/preparation.png" alt="Logo" width="400" height="300">
  </a>
      <br />
      
The next step is running the synthesis of the design under question.
This is done using the commmand:<br />
        <p align="center">
        ```run_synthesis``` 
       </p>
       <br />
After the successful completion of the synthesis part, we can collect/get various statistics including chip area, timing parameters, logic elements' usage and others from the result. In this part of the flow, Yosys and OpenSTA are involved. The results are logged in a log file located in the design specific to that run. For instance in our case the reports and logs are located in <br /> 
  <p align="center">
  ```openlane/designs/picorv32a/runs/08-04_00-16.``` 
  </p>
  
## Day 2 - Good floorplan vs bad floorplan and introduction to library cells
### Concepts

### Lab Exercises
The lab exercises for Day-2 were focusing on floorplanning and placement that was done for the picorv32a design.<br />
1. On day-1 we did the synthesis part and if that is successfully finished, we can go for the floorplanning as shown in figure below. We used the command <br />
       <p align="center">

   ```run_floorplan```

</p>

![Image description](https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Images/Synthesis%20Succesfull%20%2B%20Start%20Floorplan.png)
<br />
After a brief running time, the floorplanning will be finalized and reports/logs will be generated. In this lab we have seen some of the log parameters and how they are related with the configured parameters that we used in our task. In addition to comparing the parameters we can also look at various results from the floorplanning step. For instance,the figure below shows the die area that was consumed by our design. 

![Image description](https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Images/Result%20form%20floor%20plan-%20die%20area.png)
In addition, we have seen on how to use Magic to review the floor plan layout (which is shown below for our design) and how to see various parameters related to that.

<p align="center">
  <a href="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Images/Floorplan%20layout%20from%20magic1.png">
    <img src="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Images/Floorplan%20layout%20from%20magic1.png" alt="Logo" width="200" height="200">
  </a>
<br />

2. The next step is the placement step which basically does the placement of the cells in our die. There are two sub-steps in the placement task. These are the Global placement and the Detailed placement. In the placement step in OpenLANE flow both of these are carried out. We can run placement using the command <br />

 <p align="center">

   ```run_placement```

</p>
The placement running is shown in figure below <br />


<p align="left">
  <a href="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Images/Running%20placement.png">
    <img src="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Images/Running%20placement.png" alt="Logo" width="500" height="200">
    </p>
<br />
As was done for the floorplanning step, we can investigate further on the placed design using Magic view. The figure below shows how Magic depicts our placed design. <br />
<p align="left">
  <a href="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Images/Placement%20from%20magic.png">
    <img src="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Images/Placement%20from%20magic.png" alt="Logo" width="400" height="300">
<br />
