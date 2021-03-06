## Day 4 Pre-layout timing analysis and importance of good clock tree
### Concepts
The concepts covered in this part of the workshop are mainly focused on timing analysis using various tools which go with the accompanying lab exercises. Static timing analysis (STA) is a method of validating the timing performance of a design by checking all possible paths for timing violations. STA breaks a design down into timing paths, calculates the signal propagation delay along each path, and checks for violations of timing constraints inside the design and at the input/output interface. <br/>
Another way to perform timing analysis is to use dynamic simulation, which determines the full behavior of the circuit for a given set of input stimulus vectors. Compared to dynamic simulation, static timing analysis is much faster because it is not necessary to simulate the logical operation of the circuit. STA is also more thorough because it checks all timing paths, not just the logical conditions that are sensitized by a set of test vectors. However, STA can only check the timing, not the functionality, of a circuit design. <br/>
Reference: https://www.synopsys.com/glossary/what-is-static-timing-analysis.html <br/>

1. Timing modelling using delay tables <br/>
 Here one of the timing modelling tools, delay tables, are described in detail and their usage scenario is given in example implementation. Cell delay is the amount of delay from input to output of a logic gate in a path. In the absence of back-annotated delay information from an SDF file, the tool calculates the cell delay from delay tables provided in the logic library for the cell. Typically, a delay table lists the amount of delay as a function of one or more variables, such as input transition time and output load capacitance. From these table entries, the tool calculates each cell delay. <br/>
 There are two critical observations that should be considered in Clock Tree Synthesis (CTS): <br/>
   * At every level, each node driving the same load <br/>
   * Identical buffer at the same level <br/>
The figure below shows typical delay tables for the given design and constraints for loads. <br/>
<p align="left">
  <a href="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Day%204/Images/Delay%20Tables.png">
    <img src="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Day%204/Images/Delay%20Tables.png" alt="Logo" width="400" height="300">
    </a>
<br />
2. Timing analysis with ideal clocks using OpenSTA<br/>
Here the timing analysis for ideal clocks. This means that launch as well as capture flip-flops get clock at zero time. In other words, we can assume that clock skew is zero between start and end points. Here the setup time which is time needed for the input at the capture FF for D to reach Qm and Jitter, which is a temporary variation in clock period of the PLL clock source circuit are considered. The jitter is modeled as parameter 'Uncertainity'. The figure below shows the setup time analysis scenario. <br/>
 <p align="left">
  <a href="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Day%204/Images/Timing%20analysis%20with%20ideal%20clock.png">
    <img src="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Day%204/Images/Timing%20analysis%20with%20ideal%20clock.png" alt="Logo" width="400" height="300">
    </a>
<br /> 
3. CTS and Timing Analaysis with real clocks using OpenSTA
In this part the clock that is used is real in that it has physiscal distribution tree and hence delay between its delivery to dfifferent components of the circuit. Clock tree synthesis (CTS) is a process which ensures that all the clock gets distributed evenly to all the sequential elements in the design. The CTS is not a good technique to understand the impact of congestion and timing violations. Therefore, the main goal in CTS stage is to minimize the latency and skew. <br/>
  Related concepts covered: <br/>
  * H-Tree <br/>
  * Buffering <br/>
  * Clock Net Shielding <br/>
The two parts of timing analysis, setup and hold timing analysis, are also covered in this part. Any Input to the Flip-Flop in the design must be stable for small amount of time prior to the sampling clock edge. That small amount of time is called Setup Time. Also, the Input to the Flip-Flop must be stable for a minimum amount of time after the sampling clock edge. This time is called Hold Time. The timing analysis scenarios for the two cases are shown below. <br/>
<p align="left">
  <a href="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Day%204/Images/Setup%20timing%20analysis.png">
    <img src="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Day%204/Images/Setup%20timing%20analysis.png" alt="Logo" width="400" height="300">
    </a>
<br /> 
 <p align="left">
  <a href="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Day%204/Images/Hold%20timing%20analysis.png">
    <img src="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Day%204/Images/Hold%20timing%20analysis.png" alt="Logo" width="400" height="300">
    </a>
<br /> 

### Lab Exercises
Part I <br/>

The ultimate goal of this part of the lab is to include our cell into the picorv32a design. <br/>
The first step is to convert the grid info to track info. Then extract the lef file from the .mag file and then plug the lef file into Picorv32a design. <br/>
The first thing that we should do in order to create our own cell is to make sure that the inout and output ports are located at the intersection of horizontal and vertical grids and this can be ensured by enabling grids using the command:<br/>
grid 0.46um 0.34um 0.23um 0.17um <br/>
The result shown below shows that the ports are located at the intersection.<br/>
<p align="left">
  <a href="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Images/ports%20at%20junction.png">
    <img src="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Images/ports%20at%20junction.png" alt="Logo" width="400" height="300">
    </a>
<br />
In order to make our own cell that we can use integrating in the picorv32a design we gave names and use parameters for each port. This is done by adding the parameters in Magic as shown below: <br/>
 <p align="left">
  <a href="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Images/Params%20for%20the%20ports.png">
    <img src="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Images/Params%20for%20the%20ports.png" alt="Logo" width="400" height="300">
    </a>
<br />
After this step we extracted our cell as .lef file from Magic using the following sequence of commands. <br/>
  * save <file_name>.mag <br/>
  * magic -T <tech_file_path> <.mag_file_in_previous_step> & <br/>
  * lef write <br/>
This generates the .lef file that we include in our design (picorv32a). The following figure shows part of our extracted .lef file which shows the cell parameters that we set/defined in earlier steps. <br/>
<p align="left">
  <a href="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Day%204/Images/extracted%20lef%20file.png">
    <img src="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Day%204/Images/extracted%20lef%20file.png" alt="Logo" width="200" height="400">
    </a>
<br />  
 The next step is incorporating our new cell (sky130_vsdinv) in the original design. The procedures for this step are clearly indicated in https://github.com/nickson-jose/vsdstdcelldesign and are followed in this lab exercise too. After this we run synthesis and see if our new cells are included. One indicator in the synthesis process as whether our cells are included is show below shoing our cells in the component list.<br/>
 <p align="left">
  <a href="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Day%204/Images/an%20indicator%20that%20our%20design%20is%20included%20in%20synthesis.png">
    <img src="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Day%204/Images/an%20indicator%20that%20our%20design%20is%20included%20in%20synthesis.png" alt="Logo" width="400" height="300">
    </a>
<br /> 
  After the synthesis step is done, we continued with the floorplanning and placement steps to see graphically if our new cell is included in the design using Magic. As can be seen in the figure below, our new cell is included in picorv32a design. <br/>
  <p align="left">
  <a href="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Day%204/Images/generated%20picorv32a%20including%20our%20cell.png">
    <img src="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Day%204/Images/generated%20picorv32a%20including%20our%20cell.png" alt="Logo" width="400" height="300">
    </a>
<br /> 
 <p align="left">
  <a href="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Day%204/Images/our%20sky130_vsdinv%20in%20picorv32a.png">
    <img src="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Day%204/Images/our%20sky130_vsdinv%20in%20picorv32a.png" alt="Logo" width="400" height="300">
    </a>
<br />   
The other task that was part of Day 4's lab was using OpenSTA to do static timing analysis on the design that we generated previously in this lab. For this an pre_sta.conf file is generated which is used to capture the parameters that we wanted to monitor/modify in the primary goal of reducing the slack in our design. These tasks are basically trial and error kind procedures whichare usually done by checking our desig for cells/components producing bigger delay values and do some modifications on those. In addition, we can also change the synthesis/palcement configuration parameters to see their effect on the output slack of our design run. The figure below shows the modification on the slack value that we got as compared to the initial slack value of -17.6 by modifying the SYNTH_SIZING and SYNTH_STRATEGY configuration parameters. <br/>
 <p align="left">
  <a href="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Day%204/Images/optimize%20synthesis%20to%20reduce%20setup%20time%20violations.png">
    <img src="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Day%204/Images/optimize%20synthesis%20to%20reduce%20setup%20time%20violations.png" alt="Logo" width="400" height="300">
    </a>
<br />    
  This procedure is repeated with a thorough analysis of the design run outputs until we get a slack value that is close to zero (the ideal requirement case).
