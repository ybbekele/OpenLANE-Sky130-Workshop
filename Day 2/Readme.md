## Day 2 - Good floorplan vs bad floorplan and introduction to library cells
### Concepts
In this part of the workshop the following main concepts are covered. <br/>
1. Utilization Factor and Aspect Ratio <br/>
These parameters are used to describe the utilization of our design from the specified core area. <br/>

   Aspect ratio (AR): defines the ratio of the width to height of the chip. The aspect ratio should take into account the number of routing resources available. If there are more horizontal layers, then the rectangle should be long and width should be small and vice versa if there are more vertical layers in the design. <br/>

   Utilization Factor: is defined as the percentage of the area that has been utilized in the chip. In the initial stages of the floorplan design, if the size of the chip is unknown, then the starting point of the floorplan design is utilization.<br/>
   
    Inputs for floorplanning: 
    - Gate level Netlist
    - Libraries (.lef &.lib)
    - Constraints  <br/>
     Outputs of floorplan: floorplan of the design in the form of DEF file  <br/>

    During floorplanning, following steps are to be done:  <br/>

    Initialization of a floorplan of appropriate dimension  <br/>
    Placement of I/O pins  <br/>
    Macro placement considering the communication between them through fly lines.  <br/>
    Creation of power straps.  <br/>
    Applying appropriate placement blockages near the macros, near the I/O pins, densely packed cell areas etc.  <br/>
    Pre-Placement of Tap cells, switch cells, ESD cells, Isolation cells for Low power design-LPD  <br/>
    Creation of multiple voltage, power domains for LPD  <br/>
    Clustering of level shifter between the different power domain  <br/>
    etc  <br/>


   For more information refer: https://vlsibasic.blogspot.com/2014/01/floorplaning.html <br/>

2. Pre-placed cells <br/>
Pre-placed cells are cells that are placed manually and won't be affected by the automatic PnR. <br/>
3. De-coupling Capacitors <br/>
Decoupling capacitors (decaps) are a popular means for reducing power-supply noise in integrated circuits. Since the decaps are usually inserted in the white space of the device layer,decap  management  during  the  floorplanning  stage  is  desirable. On-chip decaps are widely used to mitigate the power-supply-noise problem. By charging  up during the steady state, decaps canassume the role of the power supply and provide the current needed during the  simultaneous switching of multiple functional blocks.<br/>
4. Power planning <br/>
The issue of distributing power in a circuit design is one of the issues that is covered in floorplanning. In order to distribute power efficiently in the circuit it is better to use a distributed approach. <br/>
<p align="left">
  <a href="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Day%202/images/power%20planning.PNG">
    <img src="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Day%202/images/power%20planning.PNG" alt="Logo" width="400" height="300">
  </a>
<br />
5. Binding netlist and initial placement design, placement and optimizing placement <br/>
Placement is the process of finding a suitable physical location for each cell in the block. The placement tool only determine the location of each standard cell on the die. After the inital placement is done, we need to optimize placement design using an estimated wire length & capacitance and based on that inserting repeaters. This results in signal integrity in our design. Here the concept of library cell characterization is also covered. Cell library characterization is a process of analyzing a circuit using static and dynamic methods to generate models suitable for chip implementation flows.<br/>
6. Cell Design and characterization flow <br/>
The entire cell design flow is revisited in this part. The cell design flow covered in this part is summarized in the figure below. <br/>
   <p align="left">
  <a href="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Day%202/images/Cell%20design%20flow.png">
    <img src="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Day%202/images/Cell%20design%20flow.png" alt="Logo" width="300" height="400">
  </a>
<br />    

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
For viewing Floorplan on Magic Layout Tool, 3 files are needed as inputs:-

    Magic technology file (sky130A.tech)
    DEF file of floorplan (md5.floorplan.def)
    Merged LEF file (merged.lef)

Inside the results/floorplan directory (containing picorv32a.floorplan.def), run the following command:
 magic -T /home/adept007/OpenLane/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read md5.floorplan.def &

<p align="left">
  <a href="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Images/Floorplan%20layout%20from%20magic1.png">
    <img src="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Images/Floorplan%20layout%20from%20magic1.png" alt="Logo" width="400" height="300">
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
    </a>
<br />
   Output of Placement Stage: A DEF (Design Exchange Format) file 
 Viewing Placement in Magic

For viewing Placement on Magic Layout Tool, 3 files are needed as inputs:-

    Magic technology file (sky130A.tech)
    DEF file of Placement (md5.placement.def)
    Merged LEF file (merged.lef)

Inside the results/placement directory (containing md5.placement.def), run the following command: <br />
   magic -T /home/adept007/OpenLane/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read md5.placement.def &
<br />
<p align="left">
  <a href="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Images/Placement%20from%20magic.png">
    <img src="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Images/Placement%20from%20magic.png" alt="Logo" width="400" height="300">
    </a>
<br />
Standard Cell Characterization

Standard Cell Libraries consist of cells with different functionality/drive strengths. These cells need to be characterized by liberty files to be used by synthesis tools to determine optimal circuit arrangement. The open-source software GUNA is used for characterization.
Cell Design Flow

The three stages of Standard cell design flow are:-

    Inputs: PDKs, DRC & LVS rules, SPICE models, Library and User-defined specifications.
    Design: Circuit Design, Layout Design, Standard cell Characterization (performed by GUNA). Types of characterization includes Timing characterization, Power characterization and Noise characterization.
    Outputs: CDL (Circuit Description Language), GDSII, LEF, extracted Spice netlist (.cir).
