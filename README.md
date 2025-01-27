# RTL to GDSII Flow

## Overview
This repository demonstrates the complete ASIC design flow from RTL (Register Transfer Level) to GDSII using open-source tools like OpenLane, Yosys, Magic, and KLayout. The project follows a structured approach covering synthesis, floorplanning, placement, routing, and signoff steps, leading to the final GDSII layout.

## Objectives
- Understand and implement the RTL to GDSII flow.
- Optimize the design for area, power, and performance.
- Generate clean GDSII files with successful DRC and LVS signoff.

  
## OpenLANE Design Stages

OpenLANE flow consists of several stages. By default, all flow steps are run in sequence. Each stage may consist of multiple sub-stages. We can run Openlane in interactive mode also.

1. **Synthesis**
    - **yosys**: Performs RTL synthesis.
    - **abc**: Handles technology mapping.
    - **OpenSTA**: Performs static timing analysis on the resulting netlist to generate timing reports.

2. **Floorplan and PDN**
    - **init_fp**: Defines the core area for the macro, the rows (used for placement), and the tracks (used for routing).
    - **ioplacer**: Places the macro input and output ports.
    - **pdn**: Generates the power distribution network.
    - **tapcell**: Inserts welltap and decap cells in the floorplan.

3. **Placement**
    - **RePLace**: Performs global placement.
    - **Resizer**: Performs optional optimizations on the design.
    - **OpenPhySyn**: Performs timing optimizations on the design.
    - **OpenDP**: Performs detailed placement to legalize the globally placed components.

4. **CTS**
    - **TritonCTS**: Synthesizes the clock distribution network (the clock tree).

5. **Routing**
    - **FastRoute**: Performs global routing to generate a guide file for the detailed router.
    - **CU-GR**: Another option for performing global routing.
    - **TritonRoute**: Performs detailed routing.
    - **SPEF-Extractor**: Performs SPEF extraction for post-routing analysis.

6. **GDSII Generation**
    - **Magic**: Streams out the final GDSII layout file from the routed DEF and performs DRC and antenna checks.
    - **KLayout**: Streams out the final GDSII layout file as a backup option and provides additional DRC checks.

7. **Checks**
    - **Magic**: Performs DRC checks and antenna checks.
    - **KLayout**: Performs additional DRC checks.
    - **Netgen**: Performs LVS checks.
    - **CVC**: Verifies circuit validity.


## Directory Structure
```
RTL-to-GDSII-Flow/
├── README.md          # Project overview and instructions
├── LICENSE            # Licensing information
├── docs/              # Documentation and flow diagrams
├── rtl/               # RTL design and testbench files
├── synthesis/         # Synthesis scripts, logs, and reports
├── floorplan/         # Floorplanning scripts and results
├── placement/         # Placement results and logs
├── routing/           # Routing results and logs
├── signoff/           # DRC, LVS, and STA reports
├── results/           # Final GDSII and other outputs
└── scripts/           # Automation scripts for the flow
```

## Flow Overview
1. **RTL Design**: Write the Verilog code for the design and verify functionality using a testbench.
2. **Synthesis**: Convert the RTL code into a gate-level netlist using Yosys.
3. **Floorplanning**: Define chip dimensions, I/O pin placement, and macro placement.
4. **Placement**: Place standard cells and macros on the floorplan.
5. **Routing**: Connect all components with metal layers.
6. **Signoff**: Perform DRC, LVS, and timing checks to ensure the design is fabrication-ready.
7. **GDSII Generation**: Export the final layout in GDSII format.

## How to Use
1. Clone this repository:
   ```bash
   git clone https://github.com/yourusername/RTL-to-GDSII-Flow.git
   cd RTL-to-GDSII-Flow
   ```
2. Install the required tools (Yosys, OpenLane, Magic, etc.).
3. Follow the step-by-step instructions in the `docs/` folder for each stage of the flow.
4. Run the provided scripts in the `scripts/` directory to automate the flow.

## Results
- **Area**: [Add area details]
- **Timing**: [Add timing results]
- **Power**: [Add power consumption details]
- **Final GDSII**: Located in the `results/` directory.

## Documentation
Detailed documentation for each step of the flow is available in the `docs/` folder, including:
- Tool installation and setup
- Command sequences for synthesis, placement, and routing
- Flow diagrams and explanations

## Acknowledgments
- OpenLane project by efabless
- SkyWater PDK for the 130nm process
- Open-source EDA tools community

## Contributing
Contributions are welcome! Feel free to fork this repository, submit issues, or open pull requests to enhance the flow.

