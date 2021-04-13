## Day 5 Final steps for RTL2GDS using tritonRoute and openSTA
### Concepts
This is the final step in the design flow which is basically Routing and SPEF Extraction steps. The following are the main concepts covered: <br/>
1. Routing and design rule check (DRC) <br/>
Here the basic idea in the routing algorithm used in design flow. The main algorithm discussed here is Maze Routing (Lee's Algorithm). There are 3 steps to follow in this algorithm: <br/>
 * Identify the ‘Source’ and ‘Target’ pins for and create Routing grid as shown in the figure below <br/>
<p align="left">
  <a href="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Day%205/Images/step1.png">
    <img src="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Day%205/Images/step1.png" alt="Logo" width="200" height="200">
    </a>
<br />
 * Based on the distance of wave-front, from ‘S’, the adjacent grid boxes are progressively filled till it hits target node ‘T’ <br/>
 <p align="left">
  <a href="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Day%205/Images/step2.png">
    <img src="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Day%205/Images/step2.png" alt="Logo" width="200" height="200">
    </a>
<br />
 * The shortest and the least detoured path is back-traced from ‘T’ to ‘S’ <br/>
 <p align="left">
  <a href="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Day%205/Images/step3.png">
    <img src="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Day%205/Images/step3.png" alt="Logo" width="200" height="200">
    </a>
<br /> 


### Lab Exercises
