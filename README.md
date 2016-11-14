#ใบงานที่ 9
##การเขียนโปรแกรมกราฟฟิกส์ด้วย GDI+ (1)
##1.	กล่าวนำ

ใบงานนี้ มีวัตถุประสงค์ เพื่อให้นักศึกษา ได้รู้จักกับ GDI+ ซึ่งจะช่วยให้นักษาสามารถ

* อธิบายระบบพิกัดใน  GDI+ ได้
* สามารถใช้คำสั่งพื้นฐานของ GDI+ ในการวาดกราฟฟิกส์อย่างง่ายได้

##2.	เนื้อหา
###2.1.	เกี่ยวกับ GDI+
GDI+ (Graphics Device Interface Plus) เป็นกราฟฟิกส์ไลบรารี่ ซึ่ง Microsoft จัดเตรียมไว้ให้นักพัฒนาโปรแกรมได้ใช้ทำงานด้านกราฟฟิกส์ โดยที่ GDI+ จะมีลักษณะเป็น OOP เต็มตัว 

ก่อนที่จะมี GDI+ ไมโครซอฟท์มีไลบรารี่ชื่อ GDI ซึ่งอยู่ในไฟล์ gdi32.dll ติดตั้งมาบน Windows ทุกตัวจนกระทั่งมาถึงยุค Windows XP ทางไมโครซอฟท์ก็ได้ปรับปรุง GDI ให้มีความสามารถมากขึ้น โดยให้ชื่อว่า GDI+ และยังคงใช้ต่อมาจนถึงวินโดวส์รุ่นปัจจุบัน

###2.2.	ความสามารถของ GDI+ 
ความสามารถของ GDI+ จะมีอยู่ 3 ส่วนหลักๆ คือ
* **Vector graphics** เป็นการสร้างกราฟฟิกส์ 2 มิติ ด้วยรูปทรงเรขาคณิตพื้นฐาน เช่น เส้นตรง(Line) เส้นโค้ง (Curve)  สี่เหลี่ยม(Rectangle) วงรี (Ellipse) เป็นต้น 
* ***Imaging*** นอกจากความสามารถในการวาดภาพด้วยรูปทรงเรขาคณิตแล้ว GDI+ ยังมีความสามารถในด้านการ แสดงผล, Load/Save ไฟล์ภาพชนิดต่างๆ ในรูปของ bitmap (bitmap ในที่นี้หมายถึงไฟล์ภาพทุกชนิด ที่แสดงเป็น pixel และไม่สามารถอธิบายด้วยรูปทรงเรขาคณิตอย่างง่ายๆ ได้ เช่น ภาพถ่าย ภาพสแกน เป็นต้น)  
* ***Typology*** เป็นการจัดการเกี่ยวกับฟอนต์ ซึ่งมีความสามารถในการแสดงผลแบบ anti aliasing ทำให้ขอบของตัวอักษรดูเรียบขึ้นมากกว่าการเขียนโปรแกรมด้วย GDI 

###2.3.	ระบบพิกัดใน GDI+
ใน GDI+ จะมีระบบพิกัดที่ใช้งานอยู่เป็นจำนวน 3 ระบบ คือ World coordinate, Page coordinate และ Device coordinate

* **World coordinate** จะทำงานกับระบบหน่วยที่ใช้ในชีวิตประจำวัน เช่น หน่วยมิลลิเมตร หรือ หน่วยนิ้ว เป็นต้น
* **Page coordinate** จะทำงานกับระบบ coordinate บนหน้ากระดาษ และจะสามารถพิมพ์ออกทางเครื่องพิมพ์ตามขนาดที่กำหนดบน page coordinate
* **Device coordinate** จะทำงานกับ pixel บนจอหรือบนเครื่องพิมพ์

###2.4.	การทดลองย่อย 1   เริ่มต้นกับ C# และ GDI+
* เรียกโปรแกรม Visual Studio
 * สร้าง Project ใหม่ เป็นชนิด C# โดยมีชื่อ project คือ GDIPlus_1
* เมื่อ Wizard สร้าง Project เสร็จแล้ว จะนำเรามาที่หน้าต่าง Form1.cs[Design] ให้คลิกที่ปุ่ม Events ของ Properties pane ตาม (1) และ Double click ที่ Paint ตาม (2)

<p align="center">
<img src="https://github.com/Desktop-Programming-Lab-2559/LAB-09/blob/master/imgs/lab9-1.png">
</p> 
* เพื่อให้โปรแกรมของเราสามารถใช้งาน GDI+ ในการวาดภาพ 2D ได้ ให้ทำการเพิ่ม ```  using System.Drawing.Drawing2D; ``` ลงในบรรทัดที่ 9 ดังรูป 
<p align="center">
<img src="https://github.com/Desktop-Programming-Lab-2559/LAB-09/blob/master/imgs/lab9-2.png">
</p> 

* ให้เพิ่มบรรทัดต่อไปนี้ลงในฟังก์ชัน ```private void Form1_Paint(object sender, PaintEventArgs e)```
 * สร้าง Object ของกราฟิกส์ โดยคำสั่ง  ```Graphics g = e.Graphics;``` ซึ่ง Object ชื่อ e ถูกส่งผ่านมาทาง argument ของฟังก์ชัน
 * เพิ่มออบเจกต์ของปากกา สีน้ำเงินขนาด 2 พิกเซล ด้วยคำสั่ง ```Pen = new Pen(Color.Blue, 2);```
 * วาดสี่เหลี่ยมด้วยคำสั่ง ```g.DrawRectangle(bluepen, 10, 10, 100, 100);```
 * คืนหน่วยความจำให้ระบบโดยการลบออบเจ็กต์ปากกาสีน้ำเงิน โดยคำสั่ง ```bluepen.Dispose();```

<p align="center">
<img src="https://github.com/Desktop-Programming-Lab-2559/LAB-09/blob/master/imgs/lab9-3.png">
</p> 
 
 * ทดลอง Build และ Run โปรแกรม
 * บันทึกผลที่ได้
 ![](https://scontent.fbkk1-3.fna.fbcdn.net/v/t34.0-12/15049906_1138598806260369_728966848_n.png?oh=28fcfbfd5c55b4aa8cbe5b49a9156f38&oe=582BA92F)
 
 <hr>
 

###2.5.	การทดลองย่อย 2  การใช้สี
####2.5.1.	การใช้สีโดยการผสมค่าสี
* เพิ่ม Code ต่อไปนี้ลงในฟังก์ชัน ```private void Form1_Paint(object sender, PaintEventArgs e)``` แล้วทดลอง Run โปรแกรม

<p align="center">
<img src="https://github.com/Desktop-Programming-Lab-2559/LAB-09/blob/master/imgs/lab9-4.png">
</p> 
 ###ทดลองรันโปรแกรมได้ดังนี้
 ![](https://scontent.fbkk1-3.fna.fbcdn.net/v/t34.0-12/15057924_1138602882926628_548341633_n.png?oh=7cf827d3bccddb015fd670dcc26f6b59&oe=582BD682)
 <hr>
 
####2.5.2.	โดยการใช้ methode FromName 
* เพิ่ม Code ต่อไปนี้ลงในฟังก์ชัน private void Form1_Paint(object sender, PaintEventArgs e) แล้วทดลอง Run โปรแกรม
 <p align="center">
<img src="https://github.com/Desktop-Programming-Lab-2559/LAB-09/blob/master/imgs/lab9-5.png">
</p> 
 ###ทดลองรันโปรแกรมได้ดังนี้
 ![](https://scontent.fbkk1-3.fna.fbcdn.net/v/t34.0-12/15058618_1138608166259433_614027133_n.png?oh=8261efb2f3c8de812395687fa09d368b&oe=582BA862)

####2.5.3. การทดลองย่อย 3  -- การใช้ปากกา
* การทดลองเปลี่ยนขนาดและสีของปากกา โดยใช้ properties Width และ Color
<p align="center">
<img src="https://github.com/Desktop-Programming-Lab-2559/LAB-09/blob/master/imgs/lab9-6.png">
</p> 
 ###ทดลองรันโปรแกรมได้ดังนี้
 ![](https://scontent.fbkk1-3.fna.fbcdn.net/v/t34.0-12/15045824_1138612046259045_1700990058_n.png?oh=fb8e2e7701643887acae651550083ba7&oe=582CC339)
 <hr>

* เปลี่ยนชนิดของปากกาเป็นเส้นประ
<p align="center">
<img src="https://github.com/Desktop-Programming-Lab-2559/LAB-09/blob/master/imgs/lab9-7.png">
</p> 
###ทดลองรันโปรแกรมได้ดังนี้
 ![](https://scontent.fbkk1-3.fna.fbcdn.net/v/t34.0-12/15057771_1138614232925493_63437757_n.png?oh=f569d2bb3d4732d9e195634e6b1bfa53&oe=582CE0FD)
 <hr>
 

* ใช้ Pen ร่วมกับ Brush  
 <p align="center">
<img src="https://github.com/Desktop-Programming-Lab-2559/LAB-09/blob/master/imgs/lab9-8.png">
</p> 

* ใช้ Pen ร่วมกับ HatchBrush  เพื่อสร้างลายเส้นแบบต่างๆ
 <p align="center">
<img src="https://github.com/Desktop-Programming-Lab-2559/LAB-09/blob/master/imgs/lab9-9.png">
</p> 
 

##คำถาม/แบบฝึกหัดท้ายการทดลอง
* ให้เปลี่ยน Color และ HatchStyle เป็นแบบต่างๆ เพื่อดูความเปลี่ยนแปลง 
 * เลือกรูปแบจาก [MSDN: HatchStyle Enumeration](https://msdn.microsoft.com/en-us/library/system.drawing.drawing2d.hatchstyle(v=vs.110).aspx) แล้ววาดภาพมาส่งอย่างน้อย 6 รูปแบบ 
