
# Setup your machine 

ให้ทำตามครบทุกขั้นตอนเพื่อให้แน่ใจว่า ระบบและซอฟต์แวร์สามารถทำงานได้อย่างไม่มีปัญหา **และควรทำล่วงหน้าก่อนวันอบรมสักอย่างน้อย 4-5 วัน เพราะถ้าพบว่าเครื่องของตัวเองถูก block หรือจำกัดสิทธิ์ จะได้ทำเรื่องกับฝ่าย Security หรือ Admin เพื่อดำเนินการให้สามารถติดตั้งและใช้งานได้ตามปกติ**

## ⚠️ ข้อควรระวัง เรื่องการใช้เครื่องคอมขององค์กร มาใช้ในการอบรม

- **แนะนำว่าสำหรับองค์กรที่มีการ block การทำงานผ่านอินเตอร์เน็ต เช่นการ block port หรือ certificate ให้เตรียม Account สำหรับเชื่อมต่ออินเตอร์เน็ตวงนอกให้ผู้เข้าอบรมได้เลย**
- การอบรมจะมีการรันคำสั่งผ่าน โปรแกรม Command Prompt หรือ Terminal และมีโปรเซสที่ทำการสร้างและแก้ไขไฟล์ที่อยู่บนระบบปฏิบัติการ (เช่น NodeJS process) ให้แน่ใจว่าระบบปฏิบัติการไม่ได้มีการบล๊อคการทำงาน และสามารถทำงานได้อย่างไม่มีปัญหา
- ระหว่างการอบรม จะมีการเชื่อมต่ออินเตอร์เน็ต และมีการดาวน์โหลดโค้ด รวมถึงติดตั้ง, setup, และ install โปรแกรมเพิ่มเติม **ควรให้แน่ใจว่าคอมพิวเตอร์ทีี่ใช้ไม่มีการปิดกั้นการทำงานดังกล่าว**

> ⚠️⚠️⚠️ หากทางผู้ดูแลระบบไม่ได้มีการอำนวยความสะดวกในการผ่อนปรนตามสถานการณ์ด้านบน ทางผู้เข้าอบรมอาจจะไม่สามารถใช้คอมพิวเตอร์นั้นเรียนรู้ หรือทำ workshop บางส่วนได้ จึงขอแจ้งมาเพื่อทราบครับ

## 1. สำหรับ Computer ที่ใช้ในการทำงาน

ทำการดาวน์โหลดตัวติดตั้ง และดำเนินการติดตั้งให้เรียบร้อย

1. JDK SDK 17 รุ่น LTS
   1. [Windows](https://www.oracle.com/java/technologies/downloads/#jdk17-windows)
   2. [MacOS](https://www.oracle.com/java/technologies/downloads/#jdk17-mac)
   
   > เสร็จแล้วทดสอบรันคำสั่ง `javac --version` ใน Terminal/Command Prompt ควรจะแสดงเวอร์ชั่นของ JDK ที่ติดตั้งแล้ว 

2. Git Client ([Download](http://git-scm.com/download/) | [คลิปแนะนำการติดตั้ง](https://www.youtube.com/watch?v=fPOoIZbDKmE))
3. Visual Studio Code ([Download](https://code.visualstudio.com/))
   - เสร็จแล้วติดตั้งส่วนเสริม 
     1. [Nextflow Java Testing Extension Pack](https://marketplace.visualstudio.com/items?itemName=teerasej.nextflow-java-testing-pack) 
4. Web Browser สามารถเลือกระหว่าง 2 อย่างนี้ 
   1. Google Chrome ([Download](https://www.google.com/chrome/))
   2. Microsoft Edge ([Download](https://www.microsoft.com/en-us/edge/download))
5. Maven 
   1. MacOS 
      1. ติดตั้ง [HomeBrew](https://brew.sh/) 
      2. รันคำสั่ง `brew install maven` ใน Terminal
   2. Windows (ติดตั้งผ่าน Chocolatey)
      1. ติดตั้ง [Chotolatey](https://chocolatey.org/install#individual)
      2. รันคำสั่ง `choco install maven` ใน Command Prompt

## 2. สมัคร Account ที่ควรมี

[สมัคร Github Account](https://github.com/signup) ให้เรียบร้อย
