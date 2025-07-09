# โค้ดรวมสำหรับการทดลองทั้งหมด (Lab 02.02)
```cpp
void setup() {
  // เริ่มต้นการสื่อสารผ่าน Serial Monitor
  Serial.begin(115200);
  delay(1000); // รอสักครู่เพื่อให้ Serial Monitor พร้อม

  // --- 1. การคำนวณด้วยชนิดข้อมูลต่างกัน (Type Promotion) ---
  Serial.println("--- 1. ทดสอบการคำนวณระหว่างชนิดข้อมูล ---");
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


  // --- 2. การแปลงชนิดข้อมูล (Explicit Type Casting) ---
  Serial.println("\n--- 2. ทดสอบการแปลงชนิดข้อมูล (Type Casting) ---");
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
}

void loop() {
  // ไม่ต้องทำอะไรใน loop
}
```
