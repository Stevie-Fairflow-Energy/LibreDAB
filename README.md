# LibreDAB
An open source bi-directional Dual Active Bridge converter for connecting a Sodium Ion Battery to a 400 V DC link
Taking strong inspiration from the OwnTech microinverter: https://github.com/owntech-foundation/micro-inverter/

![Development Stage](https://img.shields.io/badge/development%20stage-planning-red.svg)  Development Stage - Planning - Design has not started.

- **Manifesto**
	- The project goals are to:
		- Develop an open source bi-directional Dual Active Bridge converter for connecting a Sodium Ion Battery to a 400 V DC link.
		- Make the design repairable in itself.
		- Make the design a useful module within the context of solar PV, batteries and inverters. (e.g. a portable power station)
- **Open, for everyone, forever**
	- This project welcomes community input. With strong links to the OwnTech foundation and Fairflow Energy.
	- The collective work generated is meant to remain open.
	- Design files are made with open source software - Namely KiCAD.
- **Specifications**

Category | Requirement | Notes 
:---|:---|:---
Battery chemistry | Sodium Ion | New battery technology with abundant raw material availability 
Battery voltage range | 23.8 V - 58.8 V | 14 Series Cells of ~1.7 V to 4.2 V per cell. This enables compatibility with LibreSolar BMS C1 which sets a maximum voltage of 60 V. (https://github.com/LibreSolar/bms-c1) 
Nominal Battery Voltage | 42 V | Based on 3 V per cell 
Nominal Battery Current | 20 A | At 42 V and 800 W power transfer to DC link 
Peak Battery Current | 35.3 A | At 23.8 V and 800 W power transfer to DC link 
DC Link Voltage | 400 V | Based on a 230 V AC inverter 
Nominal DC link current | 2 A | 
Rated DC link Power | 800 W | Sufficient for a plug-in solar and storage application 
Efficiency | >95% | Target at nominal conditions 
Size | Target 70 mm x 280 mm PCB footprint | Similar size to 14 x 18650 cells next to each other 

- **Repairability**
	- Golden rules:
		- Components only placed on a single side of the PCB to allow simple rework
		- Components should be handle-able with standard tweezers (no smaller than 0402 packages)
		- Physical mounting is done with screws or other re-mountable arrangements
		- No invasive potting to enable inspection and service
		- There shall be test points available for all major power and control nets
	- Preferences:
		- Use of pin-compatible parts. e.g. a common footprint that has multiple options from different manufacturers to meet the same function
		- Minimise the number of different passive components used. e.g. parallel or series common components on the BOM where possible.
	- Notes:
		- Long-term relevance will be maintained at a whole module level. I.e. This DAB should be maintained and updated as a functional block when components used become unavailable. The physical size, mounting arrangements and connections should be maintained in future revisions.
	  
- **Control**
	- LibreDAB shall follow a bi-directional power reference. Therefore it needs to know voltage and current on both sides of the converter.
	- The reference can be delivered either as an analogue voltage signal or via serial.
	- LibreDAB shall provide a "No Error" indication, the absence of that indication should be read as an error.
   
- **Key Component Selections**
	- <100 V switch
		- TI LMG5200MOFR - 80 V, 10 A half bridge with driver
		- EPC2152 - 80 V, 15 A half bridge with driver
		- **EPC23102 - 100 V, 35 A half bridge with driver** - https://epc-co.com/epc/products/gan-fets-and-ics/epc23102
	- . >500 V switch
		- **TI LMG2652 GaN Integrated Half Bridge and driver** 650 V, 140 mOhm - https://www.ti.com/product/LMG2652
		- Tokmas CID12N65D(TOKMAS) GaN single switch with integrated driver 650 V,  - 140 mOhm https://www.lcsc.com/product-detail/C21547657.html?s_z=n_q_C21547657&globalKeyword=C21547657
	- Controller
		- OwnTech SPIN https://www.owntech.org/spin-2/
	
