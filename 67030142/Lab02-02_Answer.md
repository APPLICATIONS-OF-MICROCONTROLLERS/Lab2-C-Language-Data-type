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

คำถาม

1.1 ทำไม 10 / 3.0 (เมื่อตัวหารเป็น float หรือ double) ถึงได้ผลลัพธ์เป็นทศนิยม แต่เมื่อตัวหารถูกแปลงเป็น int แล้วผลลัพธ์เป็นจำนวนเต็ม?
-  ถ้ามีข้อมูลทศนิยม (float, double) อย่างน้อย 1 ตัว ผลลัพธ์จะเป็นทศนิยม แต่ถ้าหาตัวเต็มล้วน ผลลัพธ์ก็จะเป็นจำนวนเต็ม (ตัดทศนิยมออก)

ในการเขียนโปรแกรม ต้องทำ Type Casting ในสถานการณ์ใดบ้าง
-  ทำ Type Casting เมื่อชนิดข้อมูลต่างกันและต้องการแปลงเพื่อให้การคำนวณหรือการเก็บข้อมูลถูกต้องตามต้องการ
