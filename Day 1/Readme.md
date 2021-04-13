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
  openlane/designs/picorv32a/runs/08-04_00-16. 
  </p>
