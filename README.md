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
* [Day 1 Inception of open source EDA, OpenLANE and Sky130 PDK](#https://github.com/ybbekele/OpenLANE-Sky130-Workshop/tree/main/Day%201)
  * [How to talk to computers](#How-to-talk-to-computers)
  * [SoC design and OpenLANE](#SoC-design-and-OpenLANE)
* [Day 2 Good floorplan vs bad floorplan and introduction to library cells](#Day-2-Good-floorplan-vs-bad-floorplan-and-introduction-to-library-cells)
  * [Concepts](#Concepts)
  * [Lab Exercises](#Lab-Exercises)
* [Day 3 Design library cell using Magic Layout and ngspice characterization](#Day-3-Design-library-cell-using-Magic-Layout-and-ngspice-characterization)
  * [Concepts](#Concepts)
  * [Lab Exercises](#Lab-Exercises)
* [Day 4 Pre-layout timing analysis and importance of good clock tree](#Day-4-Pre-layout-timing-analysis-and-importance-of-good-clock-tree)
  * [Concepts](#Concepts)
  * [Lab Exercises](#Lab-Exercises)
* [Day 5 Final steps for RTL2GDS using tritonRoute and openSTA](#Day-5-Final-steps-for-RTL2GDS-using-tritonRoute-and-openSTA)
  * [Concepts](#Concepts)
  * [Lab Exercises](#Lab-Exercises)
* [Acknowledgement](#Acknowledgement)



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

For more information on openLANE, please refer to these resources: <br />
* https://github.com/efabless/openlane <br />
* https://www.youtube.com/watch?v=EczW2IWdnOM

## Acknowledgement 

Kunal Ghosh - Co-founder (VSD Corp. Pvt. Ltd) <br />
Nickson Jose - Teaching Assistant <br />
Praharsha - Teaching Assistant <br />
Akurathi Radhika - Teaching Assistant <br />
Tim Edwards - Founder (Opencircuitdesign) <br />
