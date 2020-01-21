
zephyr_include_directories_ifdef(CONFIG_USE_SEGGER_RTT SEGGER Config)
zephyr_sources_ifdef(CONFIG_USE_SEGGER_RTT
  SEGGER/SEGGER_RTT.c
  SEGGER/SEGGER_RTT_ASM_ARMv7M.S
  SEGGER_RTT_zephyr.c
	)
zephyr_include_directories_ifdef(CONFIG_SEGGER_SYSTEMVIEW SEGGER Config)
zephyr_sources_ifdef(CONFIG_SEGGER_SYSTEMVIEW SEGGER/SEGGER_SYSVIEW.c)
