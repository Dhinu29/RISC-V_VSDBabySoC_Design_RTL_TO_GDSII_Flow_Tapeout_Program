# P_DINESH_WEEK_7_RISC_V_SoC_Tapeout_Program_VSD
#VSDBabySoC OpenLane & OpenROAD Flow
This repository contains the VSDBabySoC design implemented using the Sky130 PDK and processed with OpenLane and OpenROAD tools. Below is a summary of the steps followed, including synthesis, floorplanning, routing, and viewing the layout in Magic.

#1. Design Configuration
The design is configured with a config.tcl file in OpenLane:

```
bash
# Design name
set ::env(DESIGN_NAME) "vsdbabysoc"

# Source files
set ::env(VERILOG_FILES) "$::env(DESIGN_DIR)/src/vsdbabysoc_synth.v"
set ::env(VERILOG_INCLUDE_DIRS) "$::env(DESIGN_DIR)/src/include"
set ::env(EXTRA_LIBS) [glob $::env(DESIGN_DIR)/src/lib/*.lib]
set ::env(EXTRA_LEFS) [glob $::env(DESIGN_DIR)/src/lef/*.lef]
set ::env(EXTRA_GDS_FILES) [glob $::env(DESIGN_DIR)/src/gds/*.gds]

# SDC constraints
unset ::env(BASE_SDC_FILE)
set ::env(BASE_SDC_FILE) "$::env(DESIGN_DIR)/src/sdc/vsdbabysoc_synthesis.sdc"

# Clock configuration
set ::env(CLOCK_PERIOD) "20.0"
set ::env(CLOCK_PORT) "CLK"
set ::env(CLOCK_NET) $::env(CLOCK_PORT)

# IO and power nets (for PDN/tap)
set ::env(FP_IO_UNMATCHED_ERROR) 0
set ::env(VDD_PIN) "VPWR"
set ::env(GND_PIN) "VGND"
set ::env(FP_POWER_NET) $::env(VDD_PIN)
set ::env(FP_GROUND_NET) $::env(GND_PIN)

set ::env(PDN_POWER_STRAPS) "VPWR"
set ::env(PDN_GROUND_STRAPS) "VGND"
set ::env(FP_PDN_ENABLE_MACROS_GRID) 0

# Floorplanning configuration
set ::env(FP_PIN_ORDER_CFG) [glob $::env(DESIGN_DIR)/src/layout_conf/vsdbabysoc/pin_order.cfg]
set ::env(FP_SIZING) "absolute"
set ::env(DIE_AREA) "0 0 2500 2500"
set ::env(BOTTOM_MARGIN_MULT) 40
set ::env(TOP_MARGIN_MULT) 40
set ::env(LEFT_MARGIN_MULT) 150
set ::env(RIGHT_MARGIN_MULT) 150

# Tap/Decap configuration
set ::env(FP_TAP_HORIZONTAL_HALO) 10
set ::env(FP_TAP_VERTICAL_HALO) 10
set ::env(FP_TAPCELL_DIST) 14
set ::env(FP_ENDCAPCELL) "sky130_fd_sc_hd__decap_3"

# Placement configuration
set ::env(MACRO_PLACEMENT_CFG) [glob $::env(DESIGN_DIR)/src/layout_conf/vsdbabysoc/macro.cfg]

# Magic configuration
set ::env(MAGIC_ZEROIZE_ORIGIN) 0
set ::env(MAGIC_EXT_USE_GDS) 1

# PDN configuration
set ::env(FP_PDN_MACRO_HOOKS) ""
set ::env(FP_PDN_CHECK_NODES) 0

# Run options
set ::env(RUN_MCSTA) 0
set ::env(WRITE_DB) 1

# Ready for interactive flow
puts "Config loaded for design $::env(DESIGN_NAME). Ready for interactive flow."
```
#2. Running OpenLane Interactive Flow
```
cd /openlane
prep -design designs/VSDBabySoC
```
```
run_synthesis
run_floorplan
run_placement
run_cts
run_routing
run_magic
run_klayout
```

<img width="1855" height="886" alt="VSDBABYSOC_GDSII" src="https://github.com/user-attachments/assets/a366c0ca-bc03-4353-9d9f-f4a0f04cd4c6" />
<img width="1911" height="943" alt="ROUTING_!" src="https://github.com/user-attachments/assets/210e0ff2-3472-4c5b-8b14-0ae2d5737d94" />
<img width="1910" height="882" alt="HEATMAP_PLACEMENT" src="https://github.com/user-attachments/assets/86f8e322-5053-4e2b-93b3-edaa6cd72b4e" />
<img width="1913" height="947" alt="PLACEMENT" src="https://github.com/user-attachments/assets/e099fe6b-5d3c-4fdf-8fe1-c0d1fd59e12c" />
<img width="1916" height="966" alt="PLACEMENT_1" src="https://github.com/user-attachments/assets/5fbb1529-262a-44ad-9798-44aa0c1477c1" />
<img width="1918" height="882" alt="ROUTING" src="https://github.com/user-attachments/assets/0c2df9ac-7390-47b1-b440-9fd6ea551fcc" />
