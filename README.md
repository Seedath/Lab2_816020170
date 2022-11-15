# _3006 Lab 2_

## Sleeping
Sleeping was implemented by using the "make menuconfig" command and then going into Components Config -> FreeRTOS and then enable sleep which updated the respective sdkconfig files. For sleep to be enabled vApplicationIdleHook() is used and must be defined along with including <esp_sleep.h> in the main C file and CONFIG_ENABLE_FREERTOS_SLEEP must be defined and set to one in the sdkconfig.h file.

From the runtime stats we and comparing it to the stats from question2a, we see that the results for the % time were the same. Thus, from these results, it is not apparent that Sleep affects the system performance in terms of the resource utilization. Additionally, looking at the output file, we see that there was also no priority inversion due to this addition. Again in this situation, the jitter could not be analyzed to determine its effect on system performance. 

The sleep function was also used instead of the active wait to determine if this also had an effect on the system performance but it yielded the same results in terms of resource utilization and no priority inversion occurred. However, this can be useful in terms of reducing the energy consuption aspect of performance as this replacement allows the process to lighly sleep and use less power than if it was actively waiting. This can reduce the over power usage of the system and improve its performance.
