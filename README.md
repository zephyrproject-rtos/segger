## Segger module for Zephyr RTOS

This repository is the Zephyr project module for integrating Segger [RTT][1] ([wiki][2]),
[SystemView][3] ([wiki][4]) and [Monitor mode debugging][5] with Zephyr RTOS.

The code here is predominantly untouched public Segger source code with changes to support Zephyr
RTOS.

This README identifies the origin of upstream Segger files and suggests a procedure to follow when
updating to a new Segger release.

### Upstream Segger source code
Segger's [official GitHub repository][6] is not currently actively maintained, hence Segger code is
obtained from publicly accessible download links posted on Segger's website.

#### RTT and SystemView
[Download][7] "SystemView, Target Sources" from the SystemView downloads [webpage][8]. This
download contains both RTT and SystemView sources.

#### Monitor mode debugging
[Download][9] "Example project" from the Monitor mode debugging [webpage][10].

### Updating to a new Segger release
Upgrading to a new Segger release means migrating existing Zephyr changes to the latest Segger
code. There are many tools (`diff`, `patch`, `git diff`, etc.) and different approaches to
accomplishing this -- use what you are familiar with. The following procedure is a guide to
achieving the desired result.

1. Obtain the updated Segger code and prepare for subsequent steps
    1. Download upstream code from the links above
    2. Extract the SystemView update and delete the `Samples` directory
    3. Extract the Monitor mode example and delete _non_-JLINK_MONITOR* files
    4. Organize the files to match the directory structure of this repository
    5. Convert line endings of all files to Unix style LF (`\n`)
    6. Strip trailing white space of all files
2. Establish the Zephyr patches that will be applied in step 3
    1. Download the SystemView release this repository is _currently_ based on (refer to
       "SystemView version: x.yy" in the source files to determine the current release)
    2. Repeat step 1 parts ii-vi for these downloaded files
    3. Compare the files of this repository to those of step 2 part ii to identify the existing
       Zephyr changes (the "diff", or "patch") needed for step 3
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

[1]: https://www.segger.com/products/debug-probes/j-link/technology/about-real-time-transfer
[2]: https://wiki.segger.com/RTT
[3]: https://www.segger.com/products/development-tools/systemview
[4]: https://wiki.segger.com/SystemView
[5]: https://www.segger.com/products/debug-probes/j-link/technology/monitor-mode-debugging
[6]: https://github.com/SEGGERMicro
[7]: https://www.segger.com/downloads/jlink/systemview_target_src
[8]: https://www.segger.com/downloads/systemview
[9]: https://www.segger.com/downloads/pub/Generic_Cortex-M_MonitorModeSystickExample_SES.zip
[10]: https://www.segger.com/products/debug-probes/j-link/technology/monitor-mode-debugging
