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


Build และทดสอบบนบอร์ด ESP32


ผลลัพน์คือ


วิดิโอประกอบ


สรุปผล:



ลิงค์ Project ที่ทำบน VS code :















