```C
#include <Stepper.h>

#define TEMP_PIN A0

// 2048:한바퀴(360도), 1024:반바퀴(180도)...
const int stepsPerRevolution = 2048; 

// 모터 드라이브에 연결된 핀 IN4, IN2, IN3, IN1
Stepper myStepper(stepsPerRevolution,11,9,10,8);

int rotation = 0;
int post_temp = 30;

void default_setting(){

  int min_temp = 20;
  int max_temp = 34;
  int default_temp = 25;
  //1도가 움직일때 0.6
  // open issue: 소수점 몇째짜리까지 되는지 모름
  rotation = stepsPerRevolution / (max_temp - min_temp);
  myStepper.step(rotation * default_temp);
  Serial.print("초기값");
  Serial.println(rotation * default_temp);
  delay(5000);
}

void setup(){
  
  //시리얼 모니터
  Serial.begin(9600);

  // 온도 센서 설정
  pinMode(TEMP_PIN, INPUT);
  
  //step motor 속도 설정

  // 서보모터 0도 초기화
  Serial.print("초기화+++++");
  delay(2000);
  default_setting();
  //default 값 설정
}

void loop(){

  int voltage = analogRead(TEMP_PIN);
  float temp = voltage * 5.0 * 100 / 1024;
  Serial.println(temp);

  float compare_temp = temp - post_temp;
  
  if(compare_temp > 0){
    myStepper.step(rotation * compare_temp);
  }else{
    myStepper.step(-rotation * compare_temp);
  }
  
  Serial.print("온도차 ::");
  Serial.print(compare_temp);
  Serial.print(" 움직인 각도:: " );
  Serial.println(rotation * compare_temp);
  post_temp = temp;
  delay(3000);

}
```