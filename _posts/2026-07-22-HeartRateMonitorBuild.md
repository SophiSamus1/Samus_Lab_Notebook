---
layout: post
title: Heart Rate Monitor Build
date: '2026-07-22'
tags: [ ʻopihi, Thermal Performance ]
---

The heart rate monitor used for thermal performance trials was built based off of the methods from [Burnett et al. (2013)](https://doi.org/10.4319/lom.2013.11.91).     

I used [KiCad](https://www.kicad.org/) to design the PCB and generate gerber files for printing. I ordered the PCBs from [JLCPCB](https://jlcpcb.com/).   

In KiCad, I copied the original schematic from Burnett et al. (2013)

![Burnett schematic](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/HRbuild/HRbuild_schematic_Burnett.png?raw=true)     

This is my copy in KiCad:
![my schematic](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/HRbuild/HRbuild_schematic.png?raw=true)     

This is the PCB I designed following the schematic:
![PCB](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/HRbuild/HRbuild_PCB.png?raw=true)      

In KiCad, footprints for each piece must be chosen but traces are automatically generated based on schematic.     

Footprints used:
| Designator 					| Footprint 										| Designation 		|
|-------------------------------|---------------------------------------------------|-------------------|
| SW1 							| SW_Slide_1P2T_CK_OS102011MS2Q 					| SW_SPST 			|
| BT1 							| JWT_A3963_1x02_P3.96mm_Vertical 					| Battery 			|
| C3,C4 						| CP_Radial_D5.0mm_P2.00mm 							| C_Polarized_US 	|
| D1G1 							| LED_D3.0mm 										| LED 				|
| PC1 							| TO-220-3_Vertical 								| LM7805_TO220 		|
| Z1,Z2 						| D_DO-35_SOD27_P5.08mm_Vertical_KathodeUp 			| D_Zener 			|
| R10,R4,R9,R3,R2,R11,R13,R12,R7| R_Axial_DIN0207_L6.3mm_D2.5mm_P7.62mm_Horizontal 	| R 				|
| P1 							| Potentiometer_Bourns_3299Z_Horizontal 			| R_Potentiometer_US|
| J1 							| RJ14_Connfly_DS1133-S4_Horizontal 				| 4P4C 				|
| BNC1 							| BNC_Amphenol_031-6575_Horizontal 					| Conn_Coaxial_Power|
| C6,C5 						| C_Rect_L7.2mm_W2.5mm_P5.00mm_FKS2_FKP2_MKS2_MKP2 	| C 				|
| R1 							| R_Axial_DIN0204_L3.6mm_D1.6mm_P5.08mm_Horizontal 	| r=R 				|
| R5 							| R_Axial_DIN0207_L6.3mm_D2.5mm_P10.16mm_Horizontal | R 				|
| C7 							| CP_Radial_D8.0mm_P5.00mm 							| C 				|
| R8 							| R_Axial_DIN0207_L6.3mm_D2.5mm_P7.62mm_Horizontal 	| r=R 				|
| D2R1 							| LED_D5.0mm 										| LED 				|
| U1 							| DIP-8_W7.62mm 									| LM358 			|
| R14 							| R_Axial_DIN0411_L9.9mm_D3.6mm_P15.24mm_Horizontal | R 				|
| C2 							| CP_Radial_D5.0mm_P2.00mm 							| c=C_Polarized_US 	|
| C1 							| CP_Radial_D8.0mm_P5.00mm 							| c=C_Polarized_US 	|
| R6 							| R_Axial_DIN0204_L3.6mm_D1.6mm_P5.08mm_Horizontal 	| R 				|



*Note: I never got the LEDs to work on the PCB (they did work on the breadboard) but the monitor itself was successful*