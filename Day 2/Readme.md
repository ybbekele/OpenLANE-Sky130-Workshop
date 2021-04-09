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
As was done for the floorplanning step, we can investigate further on the placed design using Magic view. The figure below shows how Magic depicts our placed design. <br />
<p align="left">
  <a href="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Images/Placement%20from%20magic.png">
    <img src="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Images/Placement%20from%20magic.png" alt="Logo" width="400" height="300">
    </a>
<br />
