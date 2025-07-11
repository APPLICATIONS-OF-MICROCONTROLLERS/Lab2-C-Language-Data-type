# ใบงานที่ 02.02 การคำนวณและแปลงชนิดข้อมูลเบื้องต้น


### 1. การคำนวณด้วยชนิดข้อมูลต่างกัน (Type Promotion)

__วัตถุประสงค์__ 

ทำความเข้าใจว่าการคำนวณระหว่างชนิดข้อมูลต่างกันมีผลลัพธ์อย่างไร

- โค้ดที่ต้องเพิ่มใน `setup()` โดยลบโค้ดเดิมออก ยกเว้นบรรทัด `Serial.begin(115200);`


``` c
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
<img width="309" height="108" alt="image" src="https://github.com/user-attachments/assets/4746b6f8-7afa-434e-b90f-4542564ab659" />

__คำถาม__ 

1.1  ทำไม 10 / 3.0 (เมื่อตัวหารเป็น float หรือ double) ถึงได้ผลลัพธ์เป็นทศนิยม แต่เมื่อตัวหารถูกแปลงเป็น int แล้วผลลัพธ์เป็นจำนวนเต็ม?
เมื่อมี float หรือ double เข้ามาในนิพจน์ → การคำนวณจะ "ยกระดับ" เป็น ทศนิยม (floating point operation)จะได้ค่าทศนิยมแน่นอน กรณี: 10 / (int)3.0 
3.0 ถูกแปลงเป็น int → กลายเป็น 3 
10 / 3 เป็นการ หารระหว่างจำนวนเต็ม (int) ลลัพธ์ของการหารระหว่าง int คือ int 

### 2. การแปลงชนิดข้อมูล (Explicit Type Casting)

__วัตถุประสงค์__ 

ฝึกการแปลงชนิดข้อมูลด้วยตัวเอง

- โค้ดที่ต้องเพิ่มใน `setup()` โดยลบโค้ดเดิมออก ยกเว้นบรรทัด `Serial.begin(115200);`


``` c
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
<img width="342" height="141" alt="image" src="https://github.com/user-attachments/assets/20e320db-7af0-4401-b9e2-ad94c128aa64" />


__คำถาม__

- ในการเขียนโปรแกรม ต้องทำ Type Casting ในสถานการณ์ใดบ้าง
สถานการณ์ที่ควรใช้ Type Casting
1. เพื่อควบคุมผลลัพธ์ของการคำนวณ
เมื่อมีการหารและต้องการให้ได้ผลลัพธ์เป็น ทศนิยม แทนที่จะถูกตัดทศนิยมออก
2. เมื่อแปลงค่าเพื่อแสดงผลหรือใช้งาน
เช่น แปลง char เป็น int เพื่อดูค่า ASCII
3. เมื่อต้องการตัดทศนิยมออก
การแปลง float หรือ double เป็น int จะทำให้ ทศนิยมถูกตัดทิ้ง (ไม่ปัดขึ้น)
4. เมื่อต้องการยกระดับชนิดข้อมูลให้แม่นยำขึ้น
ในบางกรณีจำเป็นต้องแปลงค่าที่เป็น int ให้เป็น float, double, long, หรือ unsigned long long เพื่อหลีกเลี่ยงการ overflow
5. เมื่อแปลงค่าระหว่างชนิดข้อมูลที่เกี่ยวข้องกับหน่วยหรือรูปแบบ
เช่น: แปลง byte → int เพื่อให้คำนวณหรือแสดงค่าที่ชัดเจนขึ้น
แปลง unsigned เป็น signed หรือกลับกัน
