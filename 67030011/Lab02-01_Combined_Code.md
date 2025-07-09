# โค้ดรวมสำหรับการทดลองทั้งหมด (Lab 02.01)
```cpp
void setup() {
  // เริ่มต้นการสื่อสารผ่าน Serial Monitor
  Serial.begin(115200);
  delay(1000); // รอสักครู่เพื่อให้ Serial Monitor พร้อมทำงาน

  // --- การทดลองที่ 2: int ---
  Serial.println("--- 2. ทดสอบชนิดข้อมูล int (ESP32) ---");
  int myInteger = 100;
  Serial.print("ค่าเริ่มต้นของ myInteger: ");
  Serial.println(myInteger);
  myInteger = 2147483647; // ค่าสูงสุด
  Serial.print("myInteger = 2147483647 ผลลัพธ์: ");
  Serial.println(myInteger);
  myInteger = 2147483647 + 1; // ลองเกินค่าสูงสุด
  Serial.print("myInteger = 2147483647 + 1 ผลลัพธ์: ");
  Serial.println(myInteger); // Overflow
  myInteger = -2147483648; // ค่าต่ำสุด
  Serial.print("myInteger = -2147483648 ผลลัพธ์: ");
  Serial.println(myInteger);
  myInteger = -2147483648 - 1; // ลองต่ำกว่าค่าต่ำสุด
  Serial.print("myInteger = -2147483648 - 1 ผลลัพธ์: ");
  Serial.println(myInteger); // Underflow

  // --- การทดลองที่ 3: float และ double ---
  Serial.println("\n--- 3. ทดสอบชนิดข้อมูล float และ double (ESP32) ---");
  float myFloat = 3.14159265;
  Serial.print("ค่า myFloat (float): ");
  Serial.println(myFloat, 8);
  double myDouble = 3.141592653589793;
  Serial.print("ค่า myDouble (double): ");
  Serial.println(myDouble, 15);

  // --- การทดลองที่ 4: char ---
  Serial.println("\n--- 4. ทดสอบชนิดข้อมูล char ---");
  char myChar = 'Z';
  Serial.print("myChar = 'Z' ผลลัพธ์: ");
  Serial.println(myChar);
  Serial.print("myChar ในรูป ASCII: ");
  Serial.println((int)myChar);
  myChar = 122; // 122 คือค่า ASCII ของ 'z'
  Serial.print("myChar = 122 ผลลัพธ์: ");
  Serial.println(myChar);

  // --- การทดลองที่ 5: bool ---
  Serial.println("\n--- 5. ทดสอบชนิดข้อมูล bool ---");
  bool myBool = true;
  Serial.print("myBool = true ผลลัพธ์: ");
  Serial.println(myBool);
  myBool = false;
  Serial.print("myBool = false ผลลัพธ์: ");
  Serial.println(myBool);

  // --- การทดลองที่ 6: long, long long, unsigned ---
  Serial.println("\n--- 6. ทดสอบชนิดข้อมูล long, long long, unsigned (ESP32) ---");
  long myLong = 4000000000L; // long บน ESP32 คือ 32-bit (เท่า int)
  Serial.print("myLong (4,000,000,000): ");
  Serial.println(myLong); // จะเกิด overflow
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

  // --- การทดลองที่ 7: byte ---
  Serial.println("\n--- 7. ทดสอบชนิดข้อมูล byte ---");
  byte myByte = 250;
  Serial.print("myByte = 250 ผลลัพธ์: ");
  Serial.println(myByte);
  myByte = 256; // ค่าเกินขอบเขต (0-255)
  Serial.print("myByte = 256 ผลลัพธ์: ");
  Serial.println(myByte); // สังเกตผลลัพธ์
}

void loop() {
  // ไม่ต้องทำอะไรใน loop เพราะเราต้องการให้โค้ดรันแค่ครั้งเดียว
}
```
