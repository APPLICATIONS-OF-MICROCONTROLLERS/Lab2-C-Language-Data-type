# ใบงานที่ 02.03 การเรียนรู้ชนิดข้อมูลในภาษา C บน ESP32 (Wokwi Simulation)

__วัตถุประสงค์__

1. ทำความเข้าใจและสามารถระบุชนิดข้อมูลพื้นฐานในภาษา C (เช่น int, float, char, bool, long, long long, unsigned int, byte, double)

2. เข้าใจแนวคิดเรื่องขอบเขตของข้อมูล (Data Range) สำหรับ ESP32 และผลกระทบจากการเกินขอบเขต (overflow/underflow)

3. เรียนรู้การใช้โอเปอเรเตอร์ sizeof() เพื่อตรวจสอบขนาดของชนิดข้อมูล

4. สามารถประกาศตัวแปรและกำหนดค่าเริ่มต้นให้กับตัวแปรได้อย่างถูกต้อง

### เกี่ยวกับ sizeof() โอเปอเรเตอร์

`sizeof()` เป็นโอเปอเรเตอร์ในภาษา C/C++ ที่ใช้สำหรับหาขนาดของชนิดข้อมูลหรือตัวแปรในหน่วยไบต์ (bytes) มันมีประโยชน์มากในการทำความเข้าใจว่าแต่ละชนิดข้อมูลใช้หน่วยความจำไปเท่าใด ซึ่งอาจแตกต่างกันไปในแต่ละแพลตฟอร์มหรือสถาปัตยกรรมของไมโครคอนโทรลเลอร์ เช่น ขนาดของ int บน Arduino Uno (8-bit) อาจไม่เท่ากับบน ESP32 (32-bit)

### รูปแบบการใช้งาน

sizeof(ชนิดข้อมูล) เช่น sizeof(int)

sizeof(ชื่อตัวแปร) เช่น 

``` c
int myVar; 
sizeof(myVar);
```

ผลลัพธ์ที่ได้จาก `sizeof()` จะเป็นจำนวนเต็มที่บอกถึงจำนวนไบต์ที่ข้อมูลนั้นใช้ในการจัดเก็บ

### 1. ทดลองกับ int (จำนวนเต็ม) และ sizeof():


__วัตถุประสงค์__ 

ทำความเข้าใจการเก็บค่าจำนวนเต็ม ขอบเขต และขนาดของ int บน ESP32

- โค้ดที่ต้องเพิ่มใน `setup()` โดยลบโค้ดเดิมออก ยกเว้นบรรทัด `Serial.begin(115200);`


``` cpp
Serial.println("--- ทดสอบชนิดข้อมูล int (ESP32) ---");
Serial.print("ขนาดของ int: ");
Serial.print(sizeof(int));
Serial.println(" bytes");

int myInteger = 100;
Serial.print("ค่าเริ่มต้นของ myInteger: ");
Serial.println(myInteger);

// ลองกำหนดค่าให้เกินขอบเขตสูงสุดของ int (ประมาณ 2,147,483,647 สำหรับ 32-bit int)
myInteger = 2147483647; // ค่าสูงสุด
Serial.print("myInteger = 2147483647 ผลลัพธ์: ");
Serial.println(myInteger);

myInteger = 2147483647 + 1; // ลองเกินค่าสูงสุด
Serial.print("myInteger = 2147483647 + 1 ผลลัพธ์: ");
Serial.println(myInteger); // สังเกตผลลัพธ์ที่อาจเกิด Overflow

// ลองกำหนดค่าให้ต่ำกว่าขอบเขตต่ำสุดของ int (ประมาณ -2,147,483,648 สำหรับ 32-bit int)
myInteger = -2147483648; // ค่าต่ำสุด
Serial.print("myInteger = -2147483648 ผลลัพธ์: ");
Serial.println(myInteger);

myInteger = -2147483648 - 1; // ลองต่ำกว่าค่าต่ำสุด
Serial.print("myInteger = -2147483648 - 1 ผลลัพธ์: ");
Serial.println(myInteger); // สังเกตผลลัพธ์ที่อาจเกิด Underflow
```

- ดำเนินการจำลองตามวิธีที่ได้ทดลองมาแล้ว
![image](https://github.com/user-attachments/assets/f9560aa5-0cca-411f-b5b4-5a9fb55a10ed)

__คำถาม__ 

1.1  int บน ESP32 ใช้กี่ไบต์?
- 32 bit = 2147483647 byte
1.2 จากผลลัพธ์ นักศึกษาสังเกตเห็นอะไรเมื่อค่าเกินขอบเขตของ int บน ESP32? 
- จำนวนเต็มบวกจะกลายเป็นจำนวนเต็มลบ

### 2. ทดลองกับ float และ double (ทศนิยม) และ sizeof()

__วัตถุประสงค์__ 

ทำความเข้าใจการเก็บค่าทศนิยม ความแม่นยำ และขนาดของ float และ double บน ESP32

__หมายเหตุ__

 บน ESP32, float คือ 4 ไบต์ (Single Precision) และ double คือ 8 ไบต์ (Double Precision) ซึ่งมีความแม่นยำสูงกว่า


- โค้ดที่ต้องเพิ่มใน `setup()` โดยลบโค้ดเดิมออก ยกเว้นบรรทัด `Serial.begin(115200);`


``` c
Serial.println("\n--- ทดสอบชนิดข้อมูล float และ double (ESP32) ---");
Serial.print("ขนาดของ float: ");
Serial.print(sizeof(float));
Serial.println(" bytes");
Serial.print("ขนาดของ double: ");
Serial.print(sizeof(double));
Serial.println(" bytes");

float myFloat = 3.14159265; // ค่า Pi
Serial.print("ค่า myFloat (float): ");
Serial.println(myFloat, 8); // แสดงผลทศนิยม 8 ตำแหน่ง

double myDouble = 3.141592653589793; // ค่า Pi ที่แม่นยำกว่า
Serial.print("ค่า myDouble (double): ");
Serial.println(myDouble, 15); // แสดงผลทศนิยม 15 ตำแหน่ง
```

- ดำเนินการจำลองตามวิธีที่ได้ทดลองมาแล้ว
![image](https://github.com/user-attachments/assets/0e03b700-7f4c-411f-8de5-6d31785a57f6)


__คำถาม__


2.1 float และ double บน ESP32 ใช้กี่ไบต์ตามลำดับ?
- float ใช้ 4 ไบต์
- double ใช้ 8 ไบต์

2.2 นักศึกษาสังเกตเห็นความแตกต่างของความแม่นยำระหว่าง float และ double อย่างไร? สถานการณ์ใดที่คุณควรเลือกใช้ double แทน float?
- double จะมีความละเอียดของทศนิยมมากกว่า floatถ้าต้องการความละเอียดสูงให้ใช้ double เเต่ถ้าไม่ต้องละเอียดมากสามารถใช้ float
- 
### 3. ทดลองกับ char (อักขระ) และ sizeof()

__วัตถุประสงค์__

- ทำความเข้าใจการเก็บอักขระ ขนาด และการแปลงเป็นค่า ASCII

- โค้ดที่ต้องเพิ่มใน `setup()` โดยลบโค้ดเดิมออก ยกเว้นบรรทัด `Serial.begin(115200);`

``` c
Serial.println("\n--- ทดสอบชนิดข้อมูล char ---");
Serial.print("ขนาดของ char: ");
Serial.print(sizeof(char));
Serial.println(" bytes");

char myChar = 'Z';
Serial.print("myChar = 'Z' ผลลัพธ์: ");
Serial.println(myChar);
Serial.print("myChar ในรูป ASCII: ");
Serial.println((int)myChar); // แปลง char เป็น int เพื่อดูค่า ASCII

myChar = 122; // 122 คือค่า ASCII ของ 'z'
Serial.print("myChar = 122 ผลลัพธ์: ");
Serial.println(myChar);
```

- ดำเนินการจำลองตามวิธีที่ได้ทดลองมาแล้ว
![image](https://github.com/user-attachments/assets/67500ffc-6997-4d61-bc43-ea20e232ae50)

  
__คำถาม__

3.1char ใช้กี่ไบต์? ค่าตัวเลข (ASCII value) มีความสัมพันธ์กับอักขระอย่างไร?
- char ใช้ 1 ไบต์
- char จะเก็บค่าเป็นตัวเลขที่เป็นรหัส ASCII (หรือรหัส Character Encoding อื่นๆ) ซึ่งแต่ละตัวเลขจะถูกจับคู่กับอักขระหนึ่งตัว
### 4. ทดลองกับ bool (ตรรกะ) และ sizeof():

__วัตถุประสงค์__

- ทำความเข้าใจการเก็บค่าความจริง (true หรือ false) และขนาด

- โค้ดที่ต้องเพิ่มใน `setup()` โดยลบโค้ดเดิมออก ยกเว้นบรรทัด `Serial.begin(115200);`

``` C++
Serial.println("\n--- ทดสอบชนิดข้อมูล bool ---");
Serial.print("ขนาดของ bool: ");
Serial.print(sizeof(bool));
Serial.println(" bytes");

bool myBool = true;
Serial.print("myBool = true ผลลัพธ์: ");
Serial.println(myBool); // true จะถูกแสดงเป็น 1

myBool = false;
Serial.print("myBool = false ผลลัพธ์: ");
Serial.println(myBool); // false จะถูกแสดงเป็น 0
```

- ดำเนินการจำลองตามวิธีที่ได้ทดลองมาแล้ว
![image](https://github.com/user-attachments/assets/a0bd869b-6e66-4583-98bd-852a0ef62204)


__คำถาม__

4.1 bool ใช้กี่ไบต์? true และ false ถูกแสดงผลเป็นค่าใดบน Serial Monitor?
- นิดข้อมูล bool ใช้ 1 ไบต์
- True = 1 , False = 0

### 5. ทดลองกับ long, long long, unsigned int, unsigned long, unsigned long long (จำนวนเต็มขนาดใหญ่/ไม่มีเครื่องหมาย) และ sizeof():

__วัตถุประสงค์__ ทำความเข้าใจการใช้ชนิดข้อมูลสำหรับจำนวนเต็มที่มีขนาดใหญ่ขึ้นและแบบไม่มีเครื่องหมายบน ESP32 รวมถึงขนาด

- โค้ดที่ต้องเพิ่มใน `setup()` โดยลบโค้ดเดิมออก ยกเว้นบรรทัด `Serial.begin(115200);`

``` C++
Serial.println("\n--- ทดสอบชนิดข้อมูล long, long long, unsigned (ESP32) ---");
Serial.print("ขนาดของ long: ");
Serial.print(sizeof(long));
Serial.println(" bytes");
Serial.print("ขนาดของ long long: ");
Serial.print(sizeof(long long));
Serial.println(" bytes");
Serial.print("ขนาดของ unsigned int: ");
Serial.print(sizeof(unsigned int));
Serial.println(" bytes");
Serial.print("ขนาดของ unsigned long: ");
Serial.print(sizeof(unsigned long));
Serial.println(" bytes");
Serial.print("ขนาดของ unsigned long long: ");
Serial.print(sizeof(unsigned long long));
Serial.println(" bytes");

long myLong = 4000000000L; // long บน ESP32 คือ 32-bit (เท่า int)
Serial.print("myLong (4,000,000,000): ");
Serial.println(myLong); // จะเกิด overflow เพราะเกิน 2.1 พันล้าน

long long myLongLong = 9000000000000000000LL; // long long คือ 64-bit
Serial.print("myLongLong (9,000,000,000,000,000,000): ");
Serial.println(myLongLong);

unsigned int myUnsignedInt = 4000000000U; // unsigned int คือ 32-bit
Serial.print("myUnsignedInt (4,000,000,000): ");
Serial.println(myUnsignedInt);

unsigned long myUnsignedLong = 4000000000UL; // unsigned long คือ 32-bit
Serial.print("myUnsignedLong (4,000,000,000): ");
Serial.println(myUnsignedLong);

unsigned long long myUnsignedLongLong = 18000000000000000000ULL; // unsigned long long คือ 64-bit
Serial.print("myUnsignedLongLong (1.8e19): ");
Serial.println(myUnsignedLongLong);
```

- ดำเนินการจำลองตามวิธีที่ได้ทดลองมาแล้ว
![image](https://github.com/user-attachments/assets/5bbf1007-5b6d-4bee-90c1-6a2cd7ad39af)

__คำถาม__

5.1 ชนิดข้อมูลจำนวนเต็มแต่ละชนิด (long, long long, unsigned int, unsigned long, unsigned long long) ใช้กี่ไบต์บน ESP32?
-long: 4 ไบต์ (32 บิต)
- long long: 8 ไบต์ (64 บิต)
- unsigned int: 4 ไบต์ (32 บิต)
- unsigned long: 4 ไบต์ (32 บิต)
- unsigned long long: 8 ไบต์ (64 บิต)

5.2 บน ESP32, long มีขอบเขตเท่ากับ int หรือไม่? ชนิดข้อมูลใดที่คุณจะใช้หากต้องการเก็บค่าจำนวนเต็มบวกที่ใหญ่ที่สุด?
- long มีขอบเขตเท่ากับ int
- ชนิดข้อมูลสำหรับค่าจำนวนเต็มบวกที่ใหญ่ที่สุด: unsigned long long (64 บิต)

### 6. ทดลองกับ byte (ข้อมูล 8 บิต) และ sizeof():

__วัตถุประสงค์__

ทำความเข้าใจการเก็บค่าจำนวนเต็มขนาดเล็ก (0-255) และขนาด

- โค้ดที่ต้องเพิ่มใน `setup()` โดยลบโค้ดเดิมออก ยกเว้นบรรทัด `Serial.begin(115200);`


``` C++
Serial.println("\n--- ทดสอบชนิดข้อมูล byte ---");
Serial.print("ขนาดของ byte: ");
Serial.print(sizeof(byte));
Serial.println(" bytes");

byte myByte = 250;
Serial.print("myByte = 250 ผลลัพธ์: ");
Serial.println(myByte);

myByte = 256; // ค่าเกินขอบเขต (0-255)
Serial.print("myByte = 256 ผลลัพธ์: ");
Serial.println(myByte); // สังเกตผลลัพธ์
```
- ดำเนินการจำลองตามวิธีที่ได้ทดลองมาแล้ว
![image](https://github.com/user-attachments/assets/96afbf7c-f6d4-47f6-8131-e19f9bfbfdda)

__คำถาม__

6.byte ใช้กี่ไบต์? เมื่อ myByte ถูกกำหนดให้เป็น 256 ผลลัพธ์ที่ได้คืออะไร และเพราะเหตุใด?
- 1 ไบต์ เท่ากับ 8 บิต ซึ่งหมายความว่า byte สามารถเก็บค่าได้ทั้งหมด 2^8 = 256
## ส่วนที่ 2: การคำนวณและแปลงชนิดข้อมูลเบื้องต้น

### 7. การคำนวณด้วยชนิดข้อมูลต่างกัน (Type Promotion)

__วัตถุประสงค์__

- ทำความเข้าใจว่าการคำนวณระหว่างชนิดข้อมูลต่างกันมีผลลัพธ์อย่างไร

- โค้ดที่ต้องเพิ่มใน `setup()` โดยลบโค้ดเดิมออก ยกเว้นบรรทัด `Serial.begin(115200);`

``` C++
Serial.println("\n--- ทดสอบการคำนวณระหว่างชนิดข้อมูล ---");
int numA = 10;
float numB = 3.0;
double numC = 3.0;

float resultFloat = numA / numB; // int หาร float ผลลัพธ์จะเป็น float
Serial.print("10 / 3.0 (ผลลัพธ์ float): ");
Serial.println(resultFloat, 2);

double resultDouble = numA / numC; // int หาร double ผลลัพธ์จะเป็น double
Serial.print("10 / 3.0 (ผลลัพธ์ double): ");
Serial.println(resultDouble, 10);

int resultInt = numA / (int)numB; // int หาร int ผลลัพธ์จะเป็น int (ทศนิยมถูกตัดทิ้ง)
Serial.print("10 / (int)3.0 (ผลลัพธ์ int): ");
Serial.println(resultInt);
```

- ดำเนินการจำลองตามวิธีที่ได้ทดลองมาแล้ว
![image](https://github.com/user-attachments/assets/0981fda6-9655-4fd6-9fbe-dbe1ad2eb24f)

__คำถาม__ 

7.ทำไม 10 / 3.0 (เมื่อตัวหารเป็น float หรือ double) ถึงได้ผลลัพธ์เป็นทศนิยม แต่เมื่อตัวหารถูกแปลงเป็น int แล้วผลลัพธ์เป็นจำนวนเต็ม?
- -ขึ้นอยู่กับ "ชนิดข้อมูล" ของตัวถูกดำเนินการ

### 8. การแปลงชนิดข้อมูล (Explicit Type Casting):

__วัตถุประสงค์__ 

-ฝึกการแปลงชนิดข้อมูลด้วยตัวเอง

- โค้ดที่ต้องเพิ่มใน `setup()` โดยลบโค้ดเดิมออก ยกเว้นบรรทัด `Serial.begin(115200);`

``` C++
Serial.println("\n--- ทดสอบการแปลงชนิดข้อมูล (Type Casting) ---");
float temperatureCelsius = 25.789;
Serial.print("อุณหภูมิ Celsius (float): ");
Serial.println(temperatureCelsius);

int temperatureInteger = (int)temperatureCelsius; // แปลง float เป็น int
Serial.print("อุณหภูมิ Celsius (แปลงเป็น int): ");
Serial.println(temperatureInteger);

// ตัวอย่างการใช้ char เป็นตัวเลข
char letter = 'P';
int asciiValue = (int)letter;
Serial.print("อักขระ 'P' มีค่า ASCII: ");
Serial.println(asciiValue);

// ตัวอย่างการแปลง int เป็น float
int count = 7;
int total = 20;
float average = (float)count / total; // ต้องแปลงอย่างน้อยหนึ่งตัวให้เป็น float ก่อนหาร
Serial.print("ค่าเฉลี่ย (7/20): ");
Serial.println(average);
```
- ดำเนินการจำลองตามวิธีที่ได้ทดลองมาแล้ว
![Uploading image.png…]()

__คำถาม__ 

8.นักศึกษาจะใช้การทำ Type Casting ในสถานการณ์ใดบ้างในการเขียนโปรแกรม?
- ต้องการควบคุมชนิดข้อมูลในการทำงาน เช่น เมื่อต้องการแปลงค่าจากชนิดข้อมูลที่มีความละเอียดสูงกว่า ไปสู่ชนิดข้อมูลที่มีความละเอียดต่ำกว่า


