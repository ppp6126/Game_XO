# Game_XO
##โจทย์
* 1. ให้เขียนเกม XO ด้วย Web App โดยให้เกมสามารถกำหนด ขนาดตารางของ XO นอกจาก 3x3 เป็นขนาดใด ๆ ก็ได้
* 2. มีระบบฐานข้อมูลเก็บ history play ของเกมเพื่อดู replay ได้
* 3. ส่งโค้ดกลับมาผ่าน github public link พร้อม readme วิธีการ setup, run โปรแกรม, วิธีออกแบบโปรแกรมและ algorithm ที่ใช้
## วิธีการ setup, run
* 1-ในส่วนของ server ให้เปิดไฟล์ src/mian/java/com/example/game (บางกรณีเปิดถึงแค่ java ก็  จะเจอแล้ว)แล้วให้คลิกขวาที่ GameApplication.java แล้วหใเลือกคลิกตรงที่ Run Java เพื่อทำการรันเซิฟเวอร์ 
* 2-ในส่วนของ display ให้กดแถบบาร์ Terminal แล้วเลือก new Terminal เพื่อเปิด Terminal ขึ้นมา    แล้วทำการพิมพ์คำสั่ง npm start เพื่อให้ระบบรันแล้วหน้าเว็บจะเปิดขึ้นมา
## วิธีออกแบบโปรแกรมและ algorithm
* เริ่มต้นระบบจะใช้ ฟังก์ชั่น componentWillMount() เพื่อวนลูปเพิ่มจำนวนตัวเลขใน select เพื่อนำมาแสดงผลในการเลือกขนาดตาราง ทำการเลือกขนาดของตารางเสร็จระบบจพใช้ 
* ฟังก์ชั่น selectTable(value) เพื่อนำจำนวนตัวเลขที่ได้จากการเลือกนำไป วนลูปเพื่อทำการเช็ตค่าตารางตามขนาดที่เราได้ทำการเลือกไว้ 
* หลังจากนั้นระบบจะทำการใช้ฟังก์ชั่น render() เพื่อวนลูปนำตารางตามขนาดที่เราต้องการออกมาและมีปุ่มกดเลือกตามต่ำแหน่งที่ต้องการ และมีการเช็ค ชนะ ในแต่ละครั้งในการกด 
* โดยกดหนึ่งครั้งระบบจะเข้าฟังก์ชั่น handleClick(value) โดยจะมีการส่งต่ำแหน่งที่เราทำการกดเข้าไปในฟังก์ชั่นด้วย เพื่อทำการเช็คว่ากดต่ำแหน่งไหน เป็นผู้เล่น X,Oแล้วระบบจะทำการส่งค่าต่ำแหน่ง ขนาดตาราง  ผู้เล่นX,Oและตาราง 
* เข้าไปในฟังก์ชั่น calculateWinnerxo() และฟังก์ชั่นจะทำการนำค่าขนาดตารรางไปวนลูปเพื่อนำตารางออกมา และทำการวนลูปอีกครั้งหนึ่งเพื่อนำต่ำแหน่งที่เราทำการกดเลือกว่าต่ำแหน่งตรงกับต่ำแหน่งไหนของตารางแล้วก็นำค่าผู้เล่นX,O * ใส่เเทนเข้าไปในต่ำแหน่งนั้น แล้วก็ส่งค่าตารางกลับไป 
* ในฟังก์ชั่น handleClick() แล้วทำการเก็บต่ำแหน่งที่เลือกและค่าผู้เล่นX,Oเก็บพร้อมกันเป็นค่า Arrayแล้วนำตารางที่ได้จากฟังก์ชั่น calculateWinnerxo()มาเซ็ตทับเข้าไปในตารางที่เรานำไปแสดง แล้ว
* จะเข้าฟังก์ชั่น checkwinner() ในฟังก์ชั่นนี้ จะมีการนำค่าขนาดตาราง มาวนลูปเพื่อหาค่าหรือแถวแนวทเเยงที่ชนะ แล้วนำข้อมูลที่ได้มาใส่ใน Array แล้วนำมาวนลูปเพื่อนำArrayที่มีข้อมูลแถวแนวทแยงที่ชนะมาเช็คว่าค่าต่ำแหน่งในตารางตรงกับต่ำแหน่งที่ชนะหรือไม่ถ้ายังไม่ตรงก็ให้กดเล่นต่อไป ถ้าตรงก็จะขึ้น winner ตามด้วยผู้ชนะแล้ว
* ระบบก็ทำเรียกใช้ฟังก์ชั่น maxid() เพื่อหารหัสเกมส์ล่าสุดแล้วนำมา+1 แล้วก็เซ็ตค่ารหัสเกมส์ 
* ต่อมาจะเข้าสู่ฟังก์ชั่น  savehistory() เพื่อการเก็บข้อมูลลงในฐานข้อมูลโดยจะเก็บ  Array ที่มีค่าXOและต่ำแหน่งที่กด ขนาดของตาราง รหัสเกมส์ เมื่อบันทึกข้อมูลเกมส์สำเร็จ
* ระบบจะทำการเรียกใช้ฟังก์ชั่นreset(value)โดยจะส่งค่าขนาดของตารางเข้าไปเพื่อรีเซ็ตค่าตาราง ให้เป็นขนาดตารางที่เราได้ทำการเล่นไป และยังมีรายการเกมส์ที่เคยเล่นไปแล้วสามารถกดดูรีเพลย์ได้ ตามรหัสเกมส์ 
* แล้วจะทำการส่งรหัสเกมส์ไปหน้า LoadGame เพื่อทำการรีเพลย์ โดยจะมีการใช้ฟังก์ชั่น componentWillMount() เพื่อทำการดึงรหัสเกมส์ออกมาแล้วทำการเรียก 
* ฟังก์ชั่น fetchgameid(value) โดยจะส่งค่ารหัสเกมส์เข้าไปเพื่อนำไป ดึงข้อมูลของเกมส์นั้นๆ ในฐานข้อมูลออกมาใช้ และ
* จะใช้ฟังก์ชั่น selectTable() เพื่อสร้างตารางขึ้นมาตามขนาดของตารางในเกมส์ที่เราเลือกมาดูรีเพลย์ 
* ต่อมาระบบจะทำการใช้ฟังก์ชั่น render() เพื่อสร้างตาราง และมีปุ่มกด รีเพลย์ 
* ระบบจะทำการเรยกใชฟังก์ชั่น autoclick()เพื่อวนลูปในการนำต่ำแหน่งและค่าXOเพื่อส่งเข้าฟังก์ชั่น handleClick() ระบบก็จะทำงานเหมือนตอนที่เรากดเล่นเกมส์ครับ 
* ฟังก์ชั่น handleClick() ทำงานเสร็จระบบก็จะทำการเรียกใช้ ฟังก์ชั่น fetchgameid(),selectTable() อีกครั้งเพื่อรีเซ็ตค่าตารางใหม่ครับ และยังมีปุ่มกด playgame เพื่อไปหน้าเล่นเกมส์ครับ
