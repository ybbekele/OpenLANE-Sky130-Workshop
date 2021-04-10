## Day 4 Pre-layout timing analysis and importance of good clock tree
### Concepts
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

