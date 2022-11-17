```C
#define TAKDO A1
#define WATERPUMP_1 6
#define WATERPUMP_2 7

unsigned long time_previous, time_current;

void setup() {
  Serial.begin(9600); //시리얼 통신 서렁
  pinMode(TAKDO,INPUT); //탁도센서 A1핀 입력
  pinMode(WATERPUMP_1,OUTPUT); //워터펌프1 OUTPUT
  pinMode(WATERPUMP_2,OUTPUT); //워터펌프2 OUTPUT

}

void loop() {
  //탁도 데이터
  int takdo_data = analogRead(TAKDO);
  takdo_data = takdo_data * 2;
  Serial.println(takdo_data);
  
  //탁도가 기준을 넘어갔을 경우
  if(takdo_data < 1600){

    //워터펌프 가동
    digitalWrite(WATERPUMP_1,HIGH);
    digitalWrite(WATERPUMP_2,LOW);
  } else {
    //워터펌프 멈춤
    digitalWrite(WATERPUMP_1,LOW);
    digitalWrite(WATERPUMP_2,LOW);
  }
}
```