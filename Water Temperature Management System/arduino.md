```c
#define TEMP_LM35 A0
#include <Servo.h>

Servo servo; //Servo 클래스로 servo 객체 생성

float C;

int angle = 0;
int default_temp = 30;

int heater_angle = 50 - 20 /360;
//float angle_rate = servo_angle  /heater_angle;
float angle_rate = 0.5;

void setup() {
  Serial.begin(9600);
  servo.attach(3); //서브모터 3번 핀 연결
}

void loop() {

  //heater
 
  
  // heater angle : servo angle
  
  default_set(default_temp);

  while(true){
  float V = fmap(analogRead(A0),0,1023,0,5); //map함수 원리를 이용한 다이렉트 Voltage계산
  
  //전압 -> 온도 공식 (섭씨)
  C = ( V - 0.5) * 100;
   
  Serial.print("tmp : ");
  Serial.println(C);
  
  servo.write(C * angle_rate);

  delay(10000);
  }
}

void default_set(int defualt_temp){
    int min = 20;
    int max = 50;
    //int i = 0;
    int flag = default_temp * angle_rate;
	servo.write(flag);
}

float fmap(long x, long in_min, long in_max, float out_min, float out_max)
{
  return (x - in_min) * (out_max - out_min) /(float) (in_max - in_min) + out_min;
}
```