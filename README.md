# _3006 Lab 2_

## Run Time Stats

For run time stats to be obtained, configGENERATE_RUN_TIME_STATS, portCONFIGURE_TIMER_FOR_RUN_TIME_STATS() and portGET_RUN_TIME_COUNTER_VALUE() must be defined in FreeRTOSConfig.h which can be set by configuring the files using the "make menuconfig" command and configuring the components.

## Round Robin Scheduling

Round robin scheduling is used by FreeRTOS when the priorities of tasks are the same. configUSE_TIME_SLICING and configUSE_PREEMPTION must also be in use to allow for the tasks to switch on each tick interrupt.

## Priority Inheritance 

Priority inheritance means that if a high priority task blocks while attempting to obtain a mutex that is currently held by a lower priority task, then the priority of the task holding the mutex is temporarily raised to that of the blocked task. (Source: https://embeddedcomputing.com)

The 3 tasks are task1_on (LED ON), task2_off (LED OFF) and task3_print (Print Status). Their priorities were varied to observe the effect priority inheritance by checking the run time stats and looking for priority inversion and utilization. The output files for each version (V1-6) are available but a summary of the results are shown below:

V1: LED ON (P=1) LED OFF (P=2) Print Status (P=3)
![v1](https://user-images.githubusercontent.com/113147843/201496965-bafe8580-bf8f-4350-a18c-7d5d75e2f7c4.JPG)

V2: LED ON (P=1) LED OFF (P=3) Print Status (P=2)
![v2](https://user-images.githubusercontent.com/113147843/201497045-99a998f5-6c90-490b-b185-3b71f14e37a6.JPG)

V3: LED ON (P=2) LED OFF (P=1) Print Status (P=3)
![v3](https://user-images.githubusercontent.com/113147843/201497049-5bb53fa1-577f-4412-b88b-9bffd710ed58.JPG)

V4: LED ON (P=2) LED OFF (P=3) Print Status (P=1)
![v4](https://user-images.githubusercontent.com/113147843/201497054-99ff3057-969e-48b5-8c17-96c715c61c17.JPG)

V5: LED ON (P=3) LED OFF (P=2) Print Status (P=1)
![v5](https://user-images.githubusercontent.com/113147843/201497062-7b002d8b-4182-42ee-b1c5-dc1a5c937f14.JPG)

V6: LED ON (P=3) LED OFF (P=1) Print Status (P=2)
![v6](https://user-images.githubusercontent.com/113147843/201497064-6abd31d3-32e7-4530-a045-15229da404ed.JPG)

