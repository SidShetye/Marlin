# Marlin 3D Printer Firmware

[Upstream source](https://github.com/MarlinFirmware/Marlin).

## Building Marlin 2.1

To build for the Ender 3 + SKR Mini E3 v1.2, the build config to use is `STM32F103RC_btt_512K` from the Auto-Build Marlin page in VSCode.

Rebased to upstream 2.1.2.5 source and added my specific customizations as follows

**Full Changelog**: https://github.com/SidShetye/Marlin/compare/2.1.2.5-SidEnder3-20250611...2.1.2.5-SidEnder3-20250612-2

## Functional changes from baseline 2.1.2.5

### General Metadata and Build

- **Author and Version Metadata** (`#define STRING_CONFIG_H_AUTHOR`, `#define CUSTOM_VERSION_FILE`, `#define SOURCE_CODE_URL`): Updated to reference Sid Shetye as author, added custom version file, and linked to new source URL.
- **README Simplification**: Major simplification to README with specific build instructions for Ender 3 + SKR Mini E3 v1.2.

---

### Temperature Control & Tuning

- **Hotend PID Tuning** (`#define DEFAULT_Kp_LIST`, `#define DEFAULT_Ki_LIST`, `#define DEFAULT_Kd_LIST`): Updated PID values based on custom tuning (2025/6/11).
- **Bed PID Control** (`#define PIDTEMPBED`, `#define DEFAULT_bedKp`, `#define DEFAULT_bedKi`, `#define DEFAULT_bedKd`): Enabled PID for bed and set new tuned values (2025/6/11).
- **PID Menus** (`#define PID_EDIT_MENU`, `#define PID_AUTOTUNE_MENU`): Enabled PID editing and autotune menus on LCD.
- **Preheat Presets** (`#define PREHEAT_1_TEMP_HOTEND`, `#define PREHEAT_1_TEMP_BED`, `#define PREHEAT_2_LABEL`, `#define PREHEAT_2_TEMP_HOTEND`, `#define PREHEAT_2_TEMP_BED`): Changed PLA/PETG presets for bed and hotend.
- **Mesh Validation** (`#define MESH_TEST_HOTEND_TEMP`, `#define MESH_TEST_BED_TEMP`): Updated mesh test temps.
- **Preheat Before Leveling** (`#define PREHEAT_BEFORE_LEVELING`, `#define LEVELING_NOZZLE_TEMP`, `#define LEVELING_BED_TEMP`): Enabled preheat before leveling and set temperatures.

---

### Motion, Feedrate, and Print Quality

- **Feedrate** (`#define DEFAULT_MAX_FEEDRATE`): Increased max Z and E feedrates for higher speed.
- **Slowdown Divisor** (`#define SLOWDOWN_DIVISOR`): Increased to 4 for better print quality.
- **Adaptive Step Smoothing** (`#define ADAPTIVE_STEP_SMOOTHING`): Enabled for improved motion.
- **Homing Speed** (`#define HOMING_FEEDRATE_MM_M`): Increased XY homing speeds.
- **Maximum Z Height** (`#define Z_MAX_POS`): Reduced Z max to 210mm due to BLTouch side mount.
- **Linear Advance** (`#define ADVANCE_K`): Set calibrated K value for better extrusion control.

---

### Bed Leveling & Probing

- **BLTouch Support** (`#define BLTOUCH`): Enabled BLTouch probe for auto bed leveling.
- **Probe Offsets and Margins** (`#define NOZZLE_TO_PROBE_OFFSET`, `#define PROBING_MARGIN`): Set new probe offsets and increased probing margin.
- **Probe Repeatability Test** (`#define Z_MIN_PROBE_REPEATABILITY_TEST`): Enabled probe repeatability test.
- **Auto Bed Leveling** (`#define AUTO_BED_LEVELING_BILINEAR`, `#define ENABLE_LEVELING_AFTER_G28`, `#define PREHEAT_BEFORE_LEVELING`): Switched to bilinear leveling, enabled auto leveling post-homing and preheating before leveling. Set preheat temps.
- **Z Safe Homing** (`#define Z_SAFE_HOMING`): Enabled safe Z homing for probe-based homing.

---

### Printing, Recovery, and User Experience

- **Print Counter** (`#define PRINTCOUNTER`): Enabled print statistics tracking.
- **Power Loss Recovery** (`#define POWER_LOSS_RECOVERY`, `#define PLR_ENABLED_DEFAULT`): Enabled and defaulted power loss resume.
- **Progress Reporting** (`#define SET_REMAINING_TIME`, `#define SET_INTERACTION_TIME`, `#define M73_REPORT`, `#define SHOW_REMAINING_TIME`, `#define PRINT_PROGRESS_SHOW_DECIMALS`): Enhanced print progress and time reporting.
- **Status Feedback and Animation** (`#define STATUS_HEAT_PERCENT`, `#define BOOT_MARLIN_LOGO_ANIMATED`): Enabled status bar enhancements and boot animation.
- **Babystepping Enhancements** (`#define BABYSTEP_ZPROBE_OFFSET`, `#define BABYSTEP_ZPROBE_GFX_OVERLAY`): Enabled advanced Z babystepping features and graphics.
- **G2/G3 Arc Support** (`#define ARC_SUPPORT`): Enabled arc support for smoother curves.
- **Filament Change Lengths** (`#define FILAMENT_CHANGE_UNLOAD_LENGTH`, `#define FILAMENT_CHANGE_FAST_LOAD_LENGTH`): Increased lengths for Bowden setup.

---

### Communications, Host, and Monitoring

- **Command Buffer Sizes** (`#define BUFSIZE`, `#define TX_BUFFER_SIZE`): Increased serial command buffer sizes.
- **Binary File Transfer** (`#define BINARY_FILE_TRANSFER`): Enabled for faster file uploads.
- **Stepper Driver Monitoring** (`#define MONITOR_DRIVER_STATUS`): Enabled stepper driver health monitoring.
- **Host Action Commands** (`#define HOST_ACTION_COMMANDS`, `#define HOST_PAUSE_M76`, `#define HOST_PROMPT_SUPPORT`, `#define HOST_START_MENU_ITEM`): Enabled host-based actions and feedback.

## Changes from version 2.1.2.5-SidEnder3-20250611

- **Source Code Reference Updated** (`#define SOURCE_CODE_URL`):  
  Updated the source code URL to reference the new branch/tag for this release.

- **Bed Leveling Behavior**:
  - **Leveling State After Homing** (`#define ENABLE_LEVELING_AFTER_G28`):  
    Switched from restoring the previous leveling state after homing (RESTORE_LEVELING_AFTER_G28) to always enabling bed leveling after homing (ENABLE_LEVELING_AFTER_G28).
  - **Preheat Before Leveling** (`#define PREHEAT_BEFORE_LEVELING`):  
    Now enabled, so the printer will preheat before bed leveling.
  - **Preheat Temperatures** (`#define LEVELING_NOZZLE_TEMP`, `#define LEVELING_BED_TEMP`):  
    Increased the nozzle preheat temperature from 120°C to 200°C and the bed from 50°C to 60°C prior to leveling.

- **Host Action Commands**:
  - **General Enablement** (`#define HOST_ACTION_COMMANDS`):  
    Host Action Commands are now enabled, allowing Marlin to interact with the host for events like filament runout.
  - **Host Pause and Prompt Support** (`#define HOST_PAUSE_M76`, `#define HOST_PROMPT_SUPPORT`):  
    Enabled host-side pause commands and user prompt support.
  - **Start Menu Item** (`#define HOST_START_MENU_ITEM`):  
    Added a menu item to allow the host to start prints via menu interaction.