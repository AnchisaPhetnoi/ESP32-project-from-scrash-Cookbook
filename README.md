# ESP32-project-from-scrash -Cookbook

ตัวอย่างที่นำมาใช้คือ การสร้าง project ของ ESP32 นำมาจาก Project ST67-Lab02-ESP-project-from-scrash 

ส่วนของการแก้ไข

### ขั้นตอนการทำ project

1.1 สร้าง folder สำหรับ project

1.1.1 เรียกเมนู file กด Open Folder

![image](https://github.com/user-attachments/assets/f0658806-064e-40e1-8eb9-7ad114fd5ae5)



1.1.2 browse ไปที่ folder ที่จะเก็บโปรเจค แล้วสร้าง folder ใหม่ ในที่นี้ชื่อ ESP32_Blank

![image](https://github.com/user-attachments/assets/ec6f8dfa-00cf-4fd0-8f21-552375a84655)

1.1.3 สร้างไฟล์ใหม่ ตั้งชื่อ Makefile และเพิ่มเนื้อหาดังนี้

![image](https://github.com/user-attachments/assets/036650dc-368c-4ec1-8d50-04bbddc9cc65)

เนื้อหาใน Makefile

``` cpp
#
# This is a project Makefile. It is assumed the directory this Makefile resides in is a
# project subdirectory.
#

PROJECT_NAME := app-template

include $(IDF_PATH)/make/project.mk
```

1.1.4 สร้างไฟล์ใหม่ ตั้งชื่อ CMakeLists.txt และเพิ่มเนื้อหาดังนี้

![image](https://github.com/user-attachments/assets/c137058a-5843-4afa-8d71-d2ec0c124659)


``` cpp
# The following lines of boilerplate have to be in your project's
# CMakeLists in this exact order for cmake to work correctly
cmake_minimum_required(VERSION 3.5)

include($ENV{IDF_PATH}/tools/cmake/project.cmake)
project(app-template)
```

1.1.5 เพิ่มไฟล์ CMakeLists.txt ในโฟลเดอร์ main

![image](https://github.com/user-attachments/assets/30ff0e67-041c-401f-89ff-e3c85e9d9bd7)


``` cpp
# Edit following two lines to set component requirements (see docs)
set(COMPONENT_REQUIRES driver)
set(COMPONENT_PRIV_REQUIRES )

set(COMPONENT_SRCS 
"LED.c"
"main.c"
)
set(COMPONENT_ADD_INCLUDEDIRS "")

register_component()
```

1.1.6 เพิ่มไฟล์ main.c

![image](https://github.com/user-attachments/assets/6e8f3999-e34d-46b5-b435-e3d41fc35355)

![image](https://github.com/user-attachments/assets/70772c2a-7e1a-416f-8511-e58b16de2155)

``` cpp
#include <stdio.h>
#include "freertos/FreeRTOS.h"
#include "freertos/task.h"
#include "driver/gpio.h"

#include "driver/gpio.h"

#include "driver/adc.h"

void app_main(void)
{
    gpio_set_direction(5, GPIO_MODE_OUTPUT);  // LED 1
    gpio_set_direction(GPIO_NUM_17, GPIO_MODE_INPUT); // Button 2
    int button2 = 0;
    int ledState = 0;

    while (1) {
        button2 = gpio_get_level(GPIO_NUM_17);
        
        if (button2 == 1)
        {
            ledState = !ledState; // สลับสถานะ LED
            gpio_set_level(5, ledState); // ตั้งค่า LED ตามสถานะ
            printf("LED State = %d\n", ledState);
            vTaskDelay(1000 / portTICK_PERIOD_MS); // หยุดรอ 1 วินาทีเพื่อหลีกเลี่ยงการกดซ้ำ
        }

        vTaskDelay(100 / portTICK_PERIOD_MS);
    }
}
```

![image](https://github.com/user-attachments/assets/8ca91324-d2ed-48b4-8c61-85e94a380882)


ผลลัพน์ที่แสดงคือ LED จะหยุดรอ และติดรอ 1 วินาที ก่อนที่จะกดปุ่มซ้ำ ต่างกับโค้ดเดิมตรงที่ โค้ดนั้น จะต้องกดปุ่มทีละครั้ง ถึงจะทำให้ LED เปิด กับ ปิด ตามการกดปุ่ม แต่ โค้ดนี้ ใช้เวลาในการ รอให้ LED ติดและดับ และค่อยกดปุ่ม จะเห็นตัวเลขที่แสดงขึ้นมา 


วิดิโอประกอบ

https://youtu.be/_H4wOot7Upg?si=y5Jtv4ceblGhFTTK


1.1.7 เพิ่มไฟล์ main.c

![image](https://github.com/user-attachments/assets/02a7c262-ec78-463b-a4c3-7152e6eff8e0)



``` cpp
#include <stdio.h>
#include "freertos/FreeRTOS.h"
#include "freertos/task.h"
#include "driver/gpio.h"

#include "driver/gpio.h"

#include "driver/adc.h"

void app_main(void)
{
    gpio_set_direction(5, GPIO_MODE_OUTPUT);  // LED 1
    gpio_set_direction(GPIO_NUM_17, GPIO_MODE_INPUT); // Button 2
    int button2 = 0;
    int pressCount = 0;

    while (1) {
        button2 = gpio_get_level(GPIO_NUM_17);
        
        if (button2 == 1)
        {
            gpio_set_level(5, 1); // LED ON
            pressCount++; // เพิ่มนับจำนวนการกด
            printf("Button pressed %d times\n", pressCount);
            vTaskDelay(1000 / portTICK_PERIOD_MS); // หยุดรอ 1 วินาทีเพื่อหลีกเลี่ยงการนับซ้ำ
        }
        else
        {
            gpio_set_level(5, 0); // LED OFF
        }

        vTaskDelay(100 / portTICK_PERIOD_MS);
    }
}

``` 

![image](https://github.com/user-attachments/assets/c834c66b-aabe-4064-b060-e10f880a608a)


![image](https://github.com/user-attachments/assets/b0760f7d-f536-43f0-8826-70310223de52)


Build และทดสอบบนบอร์ด ESP32


ผลลัพน์คือ


รูปประกอบ


สรุปผล:



ลิงค์ Project ที่ทำบน VS code : https://github.com/AnchisaPhetnoi/ESP32_Blank_.git















