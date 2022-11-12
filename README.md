# _3006 Lab 2_

## Branching

 * The main branch only contains information about the repo and serves as the information oage
 * Each question number is on a different branch since they build of each other
 * If a question number has multiple parts, they will also be on a new and separate branch in the project
 
## P1: How do the following files affect the FreeRTOS

### /project/sdkconfig

This file is application specific file. It sets the hardware configuration and customize the SDK for your specific board. Each project containts this file and it contains the settings and configuration for flashing the mircoprocessor. Thus, if the contents of this file is changed without caution, it can have cause an error in the flashing and serial monitoring process and impact the functionality of the device. For example, if a function is not defined properly then its functionality would not be available to the device.

### /project/build/include/sdkconfig.h

This is also an application specific file. It defines what you want the sdk can be set up to do and also what features of the kernel you want to be turned on or off. The file's #DEFINE's are set up when the project is successfully build and is generated according to the project's sdkconfig file. The sdkconfig file will therefore update the information in this header file and errors in that file would also affect this file. Additionally, if you have a memory or space issue, you can turn features off here to reduce the additional tasks that will be launched for those specific functions and will reduce the size of the final binary. 

### /sdk/components/freertos/port/esp8266/include/freertos/FreeRTOSConfig.h

This is a port specific file. It configures FreeRTOS for the ESP SDK. If you turn off a function here the function would not be available on the SDK. Thus, defining the statements allows for the use of the functions but increases the size of the binary. 
