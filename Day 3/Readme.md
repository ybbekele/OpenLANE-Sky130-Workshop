## Day 3 Design library cell using Magic Layout and ngspice characterization
### Concepts
### Lab Exercises
PART I <br />

The lab exercises for Day 3 are mainly focused on how to use ngspice to characterize cells and using Magic for DRC violation checking. This part reports the lab activities related to ngspice and characterization of an inverter cell.<br />
We started by cloning the github repo that is used to design an inverter cell from scratch. The gihub repo is:<br />
https://github.com/nickson-jose/vsdstdcelldesign <br />
It is cloned as shown in figure below 
<p align="left">
  <a href="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Images/cloning%20vsdstdcelldesign.png">
    <img src="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Images/cloning%20vsdstdcelldesign.png" alt="Logo" width="400" height="300">
    </a>
<br />
Then the next task is to closely analyze the sky130 LEF and basic layers layout using the inverter design that is cloned from the Github repo previously. This is done by invoking Magic using sky130 technology file and the .mag (Magic Circuit Layout) file. The depicted inverter cell is shown below:<br />
  <p align="left">
  <a href="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Images/Inverter%20after%20invoking%20magic1.png">
    <img src="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Images/Inverter%20after%20invoking%20magic1.png" alt="Logo" width="400" height="300">
    </a>
<br />
After opening the cell design in Magic, we have seen how to analyse the design through the different commands and buttons in Magic.<br /> 
The next task is to generate a spice file from the Magic design we have. The generated Spice file is shown below:<br />
 <p align="left">
  <a href="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Images/extracted%20spice%20file%20from%20magic.png">
    <img src="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Images/extracted%20spice%20file%20from%20magic.png" alt="Logo" width="400" height="300">
    </a>
<br />
 Then we added various components to the originally exported Spice file for the inverter. These components are VDD, VSS, a (Input voltage) with various parameters. In addition, a transient analysis is done on this new design using a PULSE signal. The output of the simulation on ngspice is shown below.<br />
 <p align="left">
  <a href="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Images/ngspice%20simulation%20of%20inverter.png">
    <img src="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Images/ngspice%20simulation%20of%20inverter.png" alt="Logo" width="400" height="300">
    </a>
<br />
The plot for the output signal (Y) and input signal (a) as a function of time is shown below. <br />
 <p align="left">
  <a href="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Images/ngspice%20plot%20for%20inverter.png">
    <img src="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Images/ngspice%20plot%20for%20inverter.png" alt="Logo" width="400" height="300">
    </a>
<br />
Using this plot, we tried to characterize the inverter circuit that we designed for various characterization parameters such as: <br />
   
   1. Transition time (rise and fall) usually measured 20% - 80% <br />
   2. Propagation delay (rise and fall) usually measured at 50% ouput to input <br />

   
PART II <br />
The second part of the lab exercise deals with Magic tool and how to handle DRC rules as pertained to Sky130 technology. For this part of the lab we cloned the github repository that contains magic .mag file, technology file for Sky130 and a script that runs magic. <br />
As the main aim of this lab part is to detect and mitigate violations, the first step is to check why the violations are occuring and this is done using why drc command as shown below.<br />
 <p align="left">
  <a href="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Images/DRC%20why.png">
    <img src="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Images/DRC%20why.png" alt="Logo" width="400" height="300">
    </a>
<br />
 On the given design (poly.mag) there was a spacing violation for poly.9 and that got fixed by adding a spacing drc rule for all poly layers in the technology file as: <br />
  spacing npres *nsd 480 touching_illegal \ <br/>
	"poly.resistor spacing to N-tap < %d (poly.9)" <br/>
 spacing npres allpolynonres 480 touching_illegal \ <br/>
	"poly.resistor spacing to N-tap < %d (poly.9)" <br/>
Rerunning Magic including the new rules shows that the DRC violation is now resolved<br/>
<p align="left">
  <a href="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Images/fixed%20drc%20on%20ploy%209.png">
    <img src="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Images/fixed%20drc%20on%20ploy%209.png" alt="Logo" width="400" height="300">
    </a>
<br />
**** There is a continuous work to include in this lab******
