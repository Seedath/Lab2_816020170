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

From these results, we see that V4 and V5 with LED ON and LED having priorities of either 2 or 3 both result in similar absolute time and % time. Both these show an almost equal sharing of the ON and OFF state for the LED with ith being ON slightly more than it is OFF. Looking at the output we also see that the tasks moved from Task 1 to Task 2 then Task 3. Therefore, in V4, there was priority inversion since Task 1 ran before Task 2 even though Task 2 had the higher priority. Additionally, since in both these instances, there was an equal share of the time, we see than priority inheritance occurred since these tasks were not allowed to block each other but in fact result in priority inversion for a short amount of time to allow for the sharing of the mutex.

V1 and V2 had similar runtime stats and showed LED OFF having the majority of the % time with 73% and LED ON only having 2%. In both these cases LED ON had a lower priority than LED OFF and without the mutex, LED ON would not run. However, due to priority inheritance, LED ON ran for a short time and minimized the priority inversion by temporarily raising the priority of LED ON to allow it to access the mutex for this short time. From the output files, we see that for V1 and V2, LED OFF runs twice before an instance of LED ON is run due to the priority levels but LED ON is still allowed to run in the program due to priority inheritance.

V3 and V6 share a similar situation to V1 and V2 except LED OFF is the lower priority and LED ON has the higher priority. Again, priority inheritance occurs to allow the lower priority task (LED OFF) to be temporarily raised to the priority of the higher priority task (LED ON) so that it can minimize priority inversion and access the mutex for a short time.

For all these cases, the Print Status executes for relatively the same amount of absolute and % time since it does not need the mutex and it therefore only executes based on its assigned priority.
