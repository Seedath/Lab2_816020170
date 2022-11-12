# _3006 Lab 2_

## Branching

 * The main branch only contains information about the repo and serves as the information oage
 * Each question number is on a different branch since they build of each other
 * If a question number has multiple parts, they will also be on a new and separate branch in the project
 
## Round Robin Scheduling

Round robin scheduling is used by FreeRTOS when the priorities of tasks are the same. configUSE_TIME_SLICING and configUSE_PREEMPTION must also be in use to allow for the tasks to switch on each tick interrupt.

## Run Time Stats

For run time stats to be obtained, configGENERATE_RUN_TIME_STATS, portCONFIGURE_TIMER_FOR_RUN_TIME_STATS() and portGET_RUN_TIME_COUNTER_VALUE() must be defined in FreeRTOSConfig.h which can be set by configuring the files using the "make menuconfig" command and configuring the components.
