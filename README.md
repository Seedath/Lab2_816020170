# _3006 Lab 2_

## Sleeping
Sleeping was implemented by using the "make menuconfig" command and then going into Components Config -> FreeRTOS and then enable sleep which updated the respective sdkconfig files. For sleep to be enabled vApplicationIdleHook() is used and must be defined along with including <esp_sleep.h> in the main C file and CONFIG_ENABLE_FREERTOS_SLEEP must be defined and set to one in the sdkconfig.h file.

From the runtime stats we and comparing it to the stats from question2a, we see that the results for the % time were the same. Thus, from these results, it is not apparent that Sleep affects the system performance. This, however, is useful as it can be used to save power of the device and system if necessary and will not decrease or alter the performance of the system. 
