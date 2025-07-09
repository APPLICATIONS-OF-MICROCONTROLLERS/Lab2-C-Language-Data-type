# โค้ดรวมสำหรับการทดลองทั้งหมด (Lab 02.03)

```cpp
void setup() {
  // เริ่มต้นการสื่อสารผ่าน Serial Monitor
  Serial.begin(115200);
  delay(1000); // รอสักครู่เพื่อให้ Serial Monitor พร้อม

  // --- 1. ทดสอบชนิดข้อมูล int (ESP32) ---
  Serial.println("--- 1. ทดสอบชนิดข้อมูล int (ESP32) ---");
  Serial.print("ขนาดของ int: ");
  Serial.print(sizeof(int));
  Serial.println(" bytes");
  int myInteger = 100;
  Serial.print("ค่าเริ่มต้นของ myInteger: ");
  Serial.println(myInteger);
  myInteger = 2147483647;
  Serial.print("myInteger = 2147483647 ผลลัพธ์: ");
  Serial.println(myInteger);
  myInteger = 2147483647 + 1;
  Serial.print("myInteger = 2147483647 + 1 ผลลัพธ์: ");
  Serial.println(myInteger);
  myInteger = -2147483648;
  Serial.print("myInteger = -2147483648 ผลลัพธ์: ");
  Serial.println(myInteger);
  myInteger = -2147483648 - 1;
  Serial.print("myInteger = -2147483648 - 1 ผลลัพธ์: ");
  Serial.println(myInteger);

  // --- 2. ทดสอบชนิดข้อมูล float และ double (ESP32) ---
  Serial.println("\n--- 2. ทดสอบชนิดข้อมูล float และ double (ESP32) ---");
  Serial.print("ขนาดของ float: ");
  Serial.print(sizeof(float));
  Serial.println(" bytes");
  Serial.print("ขนาดของ double: ");
  Serial.print(sizeof(double));
  Serial.println(" bytes");
  float myFloat = 3.14159265;
  Serial.print("ค่า myFloat (float): ");
  Serial.println(myFloat, 8);
  double myDouble = 3.141592653589793;
  Serial.print("ค่า myDouble (double): ");
  Serial.println(myDouble, 15);

  // --- 3. ทดสอบชนิดข้อมูล char ---
  Serial.println("\n--- 3. ทดสอบชนิดข้อมูล char ---");
  Serial.print("ขนาดของ char: ");
  Serial.print(sizeof(char));
  Serial.println(" bytes");
  char myChar = 'Z';
  Serial.print("myChar = 'Z' ผลลัพธ์: ");
  Serial.println(myChar);
  Serial.print("myChar ในรูป ASCII: ");
  Serial.println((int)myChar);
  myChar = 122;
  Serial.print("myChar = 122 ผลลัพธ์: ");
  Serial.println(myChar);

  // --- 4. ทดสอบชนิดข้อมูล bool ---
  Serial.println("\n--- 4. ทดสอบชนิดข้อมูล bool ---");
  Serial.print("ขนาดของ bool: ");
  Serial.print(sizeof(bool));
  Serial.println(" bytes");
  bool myBool = true;
  Serial.print("myBool = true ผลลัพธ์: ");
  Serial.println(myBool);
  myBool = false;
  Serial.print("myBool = false ผลลัพธ์: ");
  Serial.println(myBool);

  // --- 5. ทดสอบชนิดข้อมูล long, long long, unsigned (ESP32) ---
  Serial.println("\n--- 5. ทดสอบชนิดข้อมูล long, long long, unsigned (ESP32) ---");
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
  long myLong = 4000000000L;
  Serial.print("myLong (4,000,000,000): ");
  Serial.println(myLong);
  long long myLongLong = 9000000000000000000LL;
  Serial.print("myLongLong (9,000,000,000,000,000,000): ");
  Serial.println(myLongLong);
  unsigned int myUnsignedInt = 4000000000U;
  Serial.print("myUnsignedInt (4,000,000,000): ");
  Serial.println(myUnsignedInt);
  unsigned long myUnsignedLong = 4000000000UL;
  Serial.print("myUnsignedLong (4,000,000,000): ");
  Serial.println(myUnsignedLong);
  unsigned long long myUnsignedLongLong = 18000000000000000000ULL;
  Serial.print("myUnsignedLongLong (1.8e19): ");
  Serial.println(myUnsignedLongLong);

  // --- 6. ทดสอบชนิดข้อมูล byte ---
  Serial.println("\n--- 6. ทดสอบชนิดข้อมูล byte ---");
  Serial.print("ขนาดของ byte: ");
  Serial.print(sizeof(byte));
  Serial.println(" bytes");
  byte myByte = 250;
  Serial.print("myByte = 250 ผลลัพธ์: ");
  Serial.println(myByte);
  myByte = 256;
  Serial.print("myByte = 256 ผลลัพธ์: ");
  Serial.println(myByte);

  // --- 7. ทดสอบการคำนวณระหว่างชนิดข้อมูล ---
  Serial.println("\n--- 7. ทดสอบการคำนวณระหว่างชนิดข้อมูล ---");
  int numA = 10;
  float numB = 3.0;
  double numC = 3.0;
  float resultFloat = numA / numB;
  Serial.print("10 / 3.0 (ผลลัพธ์ float): ");
  Serial.println(resultFloat, 2);
  double resultDouble = numA / numC;
  Serial.print("10 / 3.0 (ผลลัพธ์ double): ");
  Serial.println(resultDouble, 10);
  int resultInt = numA / (int)numB;
  Serial.print("10 / (int)3.0 (ผลลัพธ์ int): ");
  Serial.println(resultInt);

  // --- 8. ทดสอบการแปลงชนิดข้อมูล (Type Casting) ---
  Serial.println("\n--- 8. ทดสอบการแปลงชนิดข้อมูล (Type Casting) ---");
  float temperatureCelsius = 25.789;
  Serial.print("อุณหภูมิ Celsius (float): ");
  Serial.println(temperatureCelsius);
  int temperatureInteger = (int)temperatureCelsius;
  Serial.print("อุณหภูมิ Celsius (แปลงเป็น int): ");
  Serial.println(temperatureInteger);
  char letter = 'P';
  int asciiValue = (int)letter;
  Serial.print("อักขระ 'P' มีค่า ASCII: ");
  Serial.println(asciiValue);
  int count = 7;
  int total = 20;
  float average = (float)count / total;
  Serial.print("ค่าเฉลี่ย (7/20): ");
  Serial.println(average);
}

void loop() {
  // ไม่ต้องทำอะไรใน loop
}
```