## Segger module for Zephyr RTOS

This repository is the Zephyr project module for integrating Segger [RTT](https://www.segger.com/products/debug-probes/j-link/technology/about-real-time-transfer) ([wiki](https://wiki.segger.com/RTT)), [SystemView](https://www.segger.com/products/development-tools/systemview/) ([wiki](https://wiki.segger.com/SystemView)) and [Monitor mode debugging](https://www.segger.com/products/debug-probes/j-link/technology/monitor-mode-debugging/) with Zephyr RTOS.

The code here is predominantly untouched public Segger source code with changes to support Zephyr RTOS.

This README identifies the origin of upstream Segger files and suggests a procedure to follow when updating to a new Segger release.

### Upstream Segger source code
Segger's [official GitHub repository](https://github.com/SEGGERMicro) is not currently actively maintained, hence Segger code is obtained from publicly accessible download links posted on Segger's website.

#### RTT and SystemView
[Download](https://www.segger.com/downloads/jlink/systemview_target_src) "SystemView, Target Sources" from the SystemView downloads [page](https://www.segger.com/downloads/systemview/). This download contains both RTT and SystemView sources.

#### Monitor mode debugging
[Download](https://www.segger.com/downloads/pub/Generic_Cortex-M_MonitorModeSystickExample_SES.zip) "Example project" from the [Monitor mode debugging](https://www.segger.com/products/debug-probes/j-link/technology/monitor-mode-debugging/) webpage.

### Updating to a new Segger release
Upgrading to a new Segger release means migrating existing Zephyr changes to the latest Segger code. There are many tools (`diff`, `patch`, `git diff`, etc.) and different approaches to accomplishing this -- use what you are familiar with. The following procedure is a guide to achieving the desired result.

1. Obtain the updated Segger code and prepare for subsequent steps
    1. Download upstream code from the links above
    2. Extract the SystemView update and delete the `Samples` directory
    3. Extract the Monitor mode example and delete _non_-JLINK_MONITOR* files
    4. Organize the files to match the directory structure of this repository
    5. Convert line endings of all files to Unix style LF (`\n`)
    6. Strip trailing white space of all files
2. Establish the Zephyr patches that will be applied in step 3
    1. Download the SystemView release this repository is _currently_ based on (refer to "SystemView version: x.yy" in the source files to determine the current release)
    2. Repeat step 1 parts ii-vi for these downloaded files
    3. Compare the files of this repository to those of step 2 part ii to identify the existing Zephyr changes (the "diff", or "patch") needed for step 3
3. Apply the Zephyr changes to the new Segger release
    1. Apply the patches from step 2 part iii to the files of step 1
    2. Sanity check the result and revise as needed
4. Review/update the list of patched files below
5. Commit the updated + modified Segger files and push the change
6. Open a pull-request to merge the change into this repository

### Patched files
Segger source files with Zephyr specific changes:
1. `Config/SEGGER_RTT_Conf.h`
    * Defines related to RTT buffers, memory region, locking mechanism
2. `Config/SEGGER_SYSVIEW_Conf.h`
    * Defines related to SystemView buffers, memory region, locking mechanism
3. `SEGGER/SEGGER_RTT.c`
    * RTT initialization options
