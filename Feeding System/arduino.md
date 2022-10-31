```C
#include <SoftwareSerial.h>

#include "SimpleTimer.h"
#include <Servo.h>
#define motorEnablePin 9
#define TWELVE_HOURS 43200000

Servo servo_9;

SimpleTimer timer;

void feedme()
{
  for (int i=1023; i<1015; i--){
    analogWrite(motorEnablePin,i);
    delay(100);
}
  analogWrite(motorEnablePin,0);
}//한바퀴 돌리는거

void initFeeding() { 
feedme();
delay(300);
feedme();
delay(300);
feedme();
delay(300);
}


void setup()
{
  servo_9.attach(9, 500, 2500);
  initFeeding();
  timer.setInterval(TWELVE_HOURS, feedMe);//12시간에 한번씩 feedme 함수 실행
}
void loop()
{
  timer.run()//timer 실행
}
```