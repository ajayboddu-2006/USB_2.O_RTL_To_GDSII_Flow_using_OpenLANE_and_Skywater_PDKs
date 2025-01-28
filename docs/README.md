# RTL-to-GDSII Flow for High-Speed USB 2.0 Device

## Introduction
This document outlines the complete RTL-to-GDSII flow implemented for a **High-Speed USB 2.0 device**. The project demonstrates how open-source tools, primarily **OpenLANE**, can be used to implement a structured ASIC design flow, covering all stages from RTL design to the final GDSII layout.

## Objectives
- To implement the ASIC design flow for a `High-Speed USB 2.0 device` while adhering to USB 2.0 specifications.
- To demonstrate each step of the flow, including **synthesis**, **floorplanning**, **placement**, **routing**, and **signoff**.
- To showcase the integration of open-source tools like **OpenLANE**, **Yosys**, **Magic**, and **KLayout** into a comprehensive design pipeline.

## OpenLane Project Directory Structure

The **OpenLane** project directory is organized to facilitate the complete ASIC design flow. Below is a typical directory structure with a brief explanation of each component:
```
Openlane/
├── Designs/
│   ├── usb/
│   |   ├── config.tcl
│   |   ├── sky130A_sky130_fd_sc_hs_config.tcl
│   |   ├── sky130A_sky130_fd_sc_ls_config.tcl
│   |   ├── sky130A_sky130_fd_sc_ms_config.tcl
│   |   ├── sky130A_sky130_fd_sc_hd_config.tcl
│   |   ├── sky130A_sky130_fd_sc_hdll_config.tcl
│   |   ├── src/
│   |   |   ├── usb_2p0_core.v
├── configuration/
│   ├── checkers.tcl
│   ├── cts.tcl
│   ├── floorplan.tcl
│   ├── general.tcl
│   ├── lvs.tcl
│   ├── placement.tcl
│   ├── routing.tcl
│   ├── synthesis.tcl
│   ├── README.md
├── flow.tcl         
├── clean_runs.tcl
```

To start the OpenLANE flow, first open the terminal, and get into the openlane directory as shown below:
#####################

To start the OpenLANE flow, type `docker` inside the openlane directory. You can check your current directory which is shown as `**OpenLANE_flow**`

In OpenLane, designs can be run in two primary modes:

**1. Interactive Mode**
- This mode allows users to execute each stage of the design flow step by step, providing flexibility and control over the process.
- Useful for debugging and understanding the design flow.

**2. Autonomous Mode:**
- This mode runs the entire design flow from RTL to GDSII in a single command.
- Suitable for quick execution or batch processing of designs.

RTL to GDS Flow of USB 2.0 is going to be run in an interactive mode in which we are able to notice the changes happenning to the design interactively.
To run the openlane in interactive mode, run the command `./flow.tcl -interactive` as shown below:

###############

You can see the OpenLANE prompt has started. Now intialize the required package(0.9) required for openlane as follows and run the command `prep -design usb` to intitialize the design for which you want continue the interactive mode of process.

#############

You can see after this, all LEF files getting merged and showing all related information related to design as above.
Our design has to  proceed with `6 layers` as per availability shown above.
In addition to this, inside `usb` directory, we can see another sub directory is created wiith name `runs`. This folder contains all stats of the design including `results` and `reports`. 
The directroy structure of `runs` is as follows:

```
usb/
├── runs/
│   ├── 25-01_11-17/
│   |   ├── cmds.log
│   |   ├── config.tcl
│   |   ├── logs
│   |   |   ├── o-prep_runtime.txt
│   |   |   ├── cts/
│   |   |   ├── cvc/
│   |   |   ├── floorplan/
│   |   |   ├── flow_summary.log
│   |   |   ├── klayout/
│   |   |   ├── lvs/
│   |   |   ├── magic/
│   |   |   ├── placement/
│   |   |   ├── routing/
│   |   |   ├── synthesis/
│   |   ├── OPENLANE_VERSION
│   |   ├── PDK_SOURCES
│   |   ├── reports/
│   |   |   ├── cts/
│   |   |   ├── cvc/
│   |   |   ├── floorplan/
│   |   |   ├── klayout/
│   |   |   ├── lvs/
│   |   |   ├── magic/
│   |   |   ├── placement/
│   |   |   ├── routing/
│   |   |   ├── synthesis/
│   |   ├── results/
│   |   |   ├── cts/
│   |   |   ├── cvc/
│   |   |   ├── floorplan/
│   |   |   ├── klayout/
│   |   |   ├── lvs/
│   |   |   ├── magic/
│   |   |   ├── placement/
│   |   |   ├── routing/
│   |   |   ├── synthesis/
│   |   ├── tmp/
```

Inside `runs`, a sub-directory with name current date and time is created in which we will have log files, reports and results of the respective process during RTL to GDS Flow.
 ## Synthesis
As a first step of deisgn flow, run the command `run_synthesis` in the openlane prompt as shown below:

#####################


When the `run_synthesis` command is executed in OpenLane, the following processes take place, performed by the respective tools:
```
- RTL Synthesis
    - Tool: yosys
        - Yosys converts the high-level RTL (Verilog) design into a gate-level netlist by performing logic synthesis. It optimizes the design based on the constraints and the standard cell library provided.

- Technology Mapping
    - Tool: abc
        - ABC maps the logic to the specific gates available in the target standard cell library, ensuring that the synthesized design adheres to the technology's requirements.

- Static Timing Analysis (STA)
    - Tool: OpenSTA
        - OpenSTA performs timing analysis on the synthesized netlist to ensure it meets timing constraints. It generates reports detailing the timing paths, slack, and potential violations.
        - These steps collectively result in a gate-level netlist (.vg file) optimized for the specified PDK and constraints.
```
After Synthesis was successful, you can see the synthsis file `usb.synthesis.v` has been created inside the `results` directory as shown below

###############

You can open the file and able to view the content as shown below:

#################

To view the netlist, run the command `yosys` to start the yosys prompt, and inside the yosys prompt run the commands `read_verilog usb.synthesis.v` and `show usb`
     
