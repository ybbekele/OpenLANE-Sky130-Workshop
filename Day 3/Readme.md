## Day 3 Design library cell using Magic Layout and ngspice characterization
### Concepts
The following main concepts are covered under this topic. <br/>
1. Spice deck creation for CMOS Inverter <br/>
 Here the main steps in creating a spice deck are covered. These include component connectivity, component values, identifying nodes in our cell design and generating a model file. The concepts are also accompanied by a practical design example which is shown in the figure below. <br/>
 <p align="left">
  <a href="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Day%203/Images/Spice%20simulation.png">
    <img src="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Day%203/Images/Spice%20simulation.png" alt="Logo" width="400" height="300">
    </a>
<br />
2. 16-mask CMOS Process <br/>
The other main concept covered in this part is the 16-mask CMOS manufacturing process. A mask is a specification of geometric shapes that need to be created on a certain layer. Masks are used to create specific patterns of each material in a sequential manner and create a complex pattern of several layers. The main steps in this process are: <br/>
	* Selecting a substrate <br/>
	* Creating active region for transistor --- LOCOS process <br/>
	* N-well and P-well formation <br/>
	* Formation of gate <br/>
	* Lightly Doped Drain (LDD) formation --- Plasma anisotropic etching <br/>
	* Source and Drain formation --- High temperature annealing <br/>
	* Steps to form contacts and interconnects <br/>
	* Higher level metal formation <br/>
For further information look at the VSD - Custom Layout course: https://www.udemy.com/course/vlsi-academy-custom-layout/
	
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
	To see the Layout of this Inverter in Magic Tool, we need two files:

    sky130A_inv.mag (obtained from cloning the Git Repo.)
    sky130A.tech (copied from openlane_working_dir/pdks/sky130A/libs.tech/magic to designs/vsdstdcelldesign directory)
<br />

	
Then the next task is to closely analyze the sky130 LEF and basic layers layout using the inverter design that is cloned from the Github repo previously. This is done by invoking Magic using sky130 technology file and the .mag (Magic Circuit Layout) file. The depicted inverter cell is shown below:<br />
	To view the layout in Magic Tool, the following command is given as shown:- <br />
	magic -T sky130A.tech sky130_inv.mag <br />
  <p align="left">
  <a href="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Images/Inverter%20after%20invoking%20magic1.png">
    <img src="https://github.com/ybbekele/OpenLANE-Sky130-Workshop/blob/main/Images/Inverter%20after%20invoking%20magic1.png" alt="Logo" width="400" height="300">
    </a>
<br />
After opening the cell design in Magic, we have seen how to analyse the design through the different commands and buttons in Magic.<br /> 
The next task is to generate a spice file from the Magic design we have. <br />
	  Parasitic Extraction in Magic

Extraction of Parasitic .spice file is done in the tkcon window of Magic by the use of the following commands:-

    extract all command to create the .ext (extraction) file.
    ext2spice command to create the .spice file from the .ext file.<br />

	  The generated Spice file is shown below:<br />
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
