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

* [OpenLANE Overview](#about-the-project)
  * [Installation](#built-with)
* [The OpenLANE Architecture](#openLANE-Arch)
  * [Design Stages](#design-stages)
* [Day 1 - Inception of open-source EDA, OpenLANE and Sky130 PDK](#Sky130-Day-1)
  * [How to talk to computers](#SKY130-D1-SK1)
  * [SoC design and OpenLANE](#SoC-design-and-OpenLANE)
  * [Get familiar to open-source EDA tools](#Get-familiar-to-open-source-EDA-tools)




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
The initialization of OpenLANE is shown in figure below.
  <p align="center">
  <a href="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Images/initialization.png">
    <img src="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Images/initialization.png" alt="Logo" width="400" height="300">
  </a> 
    <\>
Then the preparation step for using OpenLANE follows which is used mainly to prepare the environment for the upcoming tasks as shown below.\
    <p align="center">
  <a href="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Images/preparation.png">
    <img src="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Images/preparation.png" alt="Logo" width="400" height="300">
  </a>
      <\>
