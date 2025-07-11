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
<img width="401" height="168" alt="image" src="https://github.com/user-attachments/assets/8562bad3-4a44-49fb-805e-977e23012339" />

__คำถาม__ 

1.1  int บน ESP32 ใช้กี่ไบต์?
sizeof(int) บน ESP32 = 4 bytes (32-bit)

1.2 จากผลลัพธ์ นักศึกษาสังเกตเห็นอะไรเมื่อค่าเกินขอบเขตของ int บน ESP32? 
ค่าสูงสุดของ int คือ 2,147,483,647 (0x7FFFFFFF) เมื่อลองกำหนด int ให้เกินค่านี้ เช่น 2147483647 + 1
→ เกิด overflow
→ ค่าจะวนกลับไปเป็นค่าติดลบ -2147483648

เช่นเดียวกัน หากกำหนดต่ำกว่าค่าต่ำสุด (-2147483648 - 1)
→ จะเกิด underflow
→ ค่าจะวนกลับไปเป็น 2147483647

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
<img width="403" height="144" alt="image" src="https://github.com/user-attachments/assets/aff11f3e-fd4a-4e6e-9b1d-413808b642a1" />


__คำถาม__
- float และ double บน ESP32 ใช้กี่ไบต์ตามลำดับ?
float	4 bytes (32-bit floating point)
double	8 bytes (64-bit floating point)✔️ (บน ESP32)

- นักศึกษาสังเกตเห็นความแตกต่างของความแม่นยำระหว่าง float และ double อย่างไร? สถานการณ์ใดที่คุณควรเลือกใช้ double แทน float?
float เหมาะกับงานที่ไม่ต้องการความแม่นยำสูง
double เหมาะกับ: การคำนวณทางคณิตศาสตร์ที่ละเอียด งานวิศวกรรม ตำแหน่ง GPS

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
- <img width="256" height="138" alt="image" src="https://github.com/user-attachments/assets/20727093-bff0-4728-be3d-fff348be7db7" />

__คำถาม__

- char ใช้กี่ไบต์? ค่าตัวเลข (ASCII value) มีความสัมพันธ์กับอักขระอย่างไร?
sizeof(char) = 1 byte
อักษรจะถูกแทนด้วยเลข ASCII เช่น:
'A' = 65
'P' = 80
'z' = 122
การแปลง (int)char จะได้ ค่า ASCII การกำหนดค่า ASCII เช่น char x = 122; → ได้ 'z'

### 4. ทดลองกับ bool (ตรรกะ) และ sizeof():

__วัตถุประสงค์__

- ทำความเข้าใจการเก็บค่าความจริง (true หรือ false) และขนาด
ค่าใน bool	true (1), false (0)
ขนาดใน ESP32	1 byte
ค่าที่เป็น true	ตัวเลขใด ๆ ที่ไม่ใช่ 0
ค่าที่เป็น false	เฉพาะ 0 เท่านั้น
การพิมพ์ bool	ใช้ Serial.println() จะเห็นเป็น 1 หรือ 0

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
<img width="222" height="103" alt="image" src="https://github.com/user-attachments/assets/87977276-6c45-4e2d-aad9-e27e78f7692b" />


__คำถาม__

- bool ใช้กี่ไบต์? true และ false ถูกแสดงผลเป็นค่าใดบน Serial Monitor?
sizeof(bool) = 1 byte
ค่าที่แสดงผลบน Serial Monitor
true → 1
false → 0

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
<img width="513" height="291" alt="image" src="https://github.com/user-attachments/assets/c2df3997-c3e0-4dba-80a4-eb36254733fe" />

__คำถาม__

- ชนิดข้อมูลจำนวนเต็มแต่ละชนิด (long, long long, unsigned int, unsigned long, unsigned long long) ใช้กี่ไบต์บน ESP32?
long	4	32	±2.14 พันล้าน
long long	8	64	±9.2×10¹⁸
unsigned int	4	32	0 ถึง 4.29×10⁹
unsigned long	4	32	0 ถึง 4.29×10⁹
unsigned long long	8	64	0 ถึง 1.84×10¹⁹

- บน ESP32, long มีขอบเขตเท่ากับ int หรือไม่? ชนิดข้อมูลใดที่คุณจะใช้หากต้องการเก็บค่าจำนวนเต็มบวกที่ใหญ่ที่สุด?
เท่ากัน บน ESP32: int = long = 32-bit ใช้: **unsigned long long** (64-bit)
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
<img width="240" height="122" alt="image" src="https://github.com/user-attachments/assets/9319b1d0-6aa9-41a3-aa9f-787c1c37df5b" />

__คำถาม__

byte ใช้กี่ไบต์? เมื่อ myByte ถูกกำหนดให้เป็น 256 ผลลัพธ์ที่ได้คืออะไร และเพราะเหตุใด?
sizeof(byte) = 1 byte ขอบเขต: 0–255 (8 บิต)
ผลลัพธ์: 0 เพราะ 256 mod 256 = 0 (เกิด overflow) byte รองรับค่าถึงแค่ 255 → วนกลับไปเริ่มที่ 0

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

__คำถาม__ 

ทำไม 10 / 3.0 (เมื่อตัวหารเป็น float หรือ double) ถึงได้ผลลัพธ์เป็นทศนิยม แต่เมื่อตัวหารถูกแปลงเป็น int แล้วผลลัพธ์เป็นจำนวนเต็ม?
ถ้าอย่างน้อยหนึ่งตัวในนิพจน์เป็น float หรือ double
→ การหารจะเป็น "แบบทศนิยม" (floating-point division)
 ถ้าทั้งสองตัวเป็น int
→ การหารจะเป็น "แบบจำนวนเต็ม" (integer division)
→ ทศนิยมจะถูก ตัดทิ้ง (ไม่ใช่ปัดขึ้น)
2. สาเหตุที่ 10 / 3.0 ให้ผลลัพธ์ทศนิยม
10 เป็น int
3.0 เป็น float หรือ double
C/C++ จะ แปลงอัตโนมัติ ตัว int ให้เป็น float ด้วย
→ เพื่อให้ชนิดข้อมูลเหมือนกัน
→ คำสั่งจะกลายเป็น 10.0 / 3.0
→ ได้ผลลัพธ์เป็น 3.333...
3. ส่วน 10 / (int)3.0 ทำให้ผลลัพธ์เป็นจำนวนเต็ม
(int)3.0 แปลง 3.0 ให้เป็น int → ได้ 3
ตอนนี้เรากำลังทำ int / int
ผลลัพธ์เป็น int → ทศนิยมถูกตัดทิ้ง → ผลลัพธ์คือ 3
สรุปสั้น ๆ:
เมื่อมี float หรือ double อยู่ในการหาร → ระบบจะ ยกระดับ การคำนวณเป็น ทศนิยม
แต่ถ้าเป็น int / int → จะ ตัดทศนิยมทิ้ง แล้วให้ผลลัพธ์เป็นจำนวนเต็ม
หากอยากให้หารได้ทศนิยมเสมอ ควรแปลงตัวใดตัวหนึ่งให้เป็น float หรือ double ก่อน

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
<img width="364" height="133" alt="image" src="https://github.com/user-attachments/assets/6669a665-b06a-48f3-848a-20cf86861c21" />

__คำถาม__ 

นักศึกษาจะใช้การทำ Type Casting ในสถานการณ์ใดบ้างในการเขียนโปรแกรม?
 สถานการณ์ที่ควรใช้ Type Casting
1. เพื่อควบคุมผลลัพธ์ของการคำนวณ
เพื่อให้ได้ผลลัพธ์แบบทศนิยมหรือหลีกเลี่ยงการตัดทศนิยมออก
2. เมื่อต้องแปลงค่าที่ใช้แสดงผล หรือทำงานกับอุปกรณ์
เช่น การแสดงค่า ASCII จากตัวอักษร
3. ตัดค่าทศนิยมออกเพื่อให้ได้ค่าจำนวนเต็ม
เช่น การแปลง float เป็น int เพื่อใช้งานในฟังก์ชันที่ต้องการค่าจำนวนเต็ม
4. เพื่อหลีกเลี่ยงการเกิด Overflow ในการคำนวณ
เมื่อคูณค่าจำนวนเต็มที่มีโอกาสเกินขอบเขตของ int
5. เมื่อส่งค่าไปยังฟังก์ชันที่รองรับเฉพาะชนิดข้อมูลบางประเภท
เช่น ในบาง Library ต้องการ float แทน int
6. เมื่อต้องการเปลี่ยนชนิดของค่าผลลัพธ์หลังการคำนวณ
เช่น การแปลงค่าระหว่าง signed และ unsigned
7. เมื่อทำงานกับบิตระดับต่ำ หรือ pointer
ในงานขั้นสูง เช่น การแปลงชนิดของ pointer หรือ address (สำหรับ Arduino ระดับสูงหรือ Embedded)
