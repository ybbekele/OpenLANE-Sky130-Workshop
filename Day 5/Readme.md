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
For detailed information refer: https://www.vlsisystemdesign.com/maze-routing-lees-algorithm/ <br/>

2. Power Distribution Network and routing <br/>
The power distribution network in a VLSI design is a network which delivers power to all components in the design. The figure below shows the power distribution network for a typical VLSI design. <br/>
<p align="left">
  <a href="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Day%205/Images/Power%20distribution%20network%20depiction.png">
    <img src="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Day%205/Images/Power%20distribution%20network%20depiction.png" alt="Logo" width="300" height="300">
    </a>
<br /> 
3. TritonRoute Features <br/>
TritonRoute is an open source detailed router for modern industrial designs. The router consists of several main building blocks, including pin access analysis, track assignment, initial detailed routing, search and repair, and a DRC engine.

### Lab Exercises
The first step in the lab exercises is to build the power distribution network prior to routing. This is done using the command: <br/>
               gen_pdn <br/>

            
