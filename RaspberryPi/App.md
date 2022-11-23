```
#Main.py
# APP

start_time = None

while True:
    
    end_time = time.time()
    
    if start_time != None:
        if round(end_time - start_time,3) >= 30 * 60:
            temperature_managemnet()
    # 초기설정 여부    
    default_flag =None
    
    input_value = input("원하는 동작을 입력해주세요")
    #0: default 온도 설정 및 수온 조절 1: 워터펌프 2: 먹이 3:@
    
    if input_value == 0:
        default_flag = 1
        input_default_temp = input("초기 온도를 설정해주세요")
        default_temperature(int(input_default_temp)) # API 요청
        start_time = time.time()
    
    elif input_value == 1:
        filtering_management() # API 요청
        
    elif input_value == 2:
        
        feeding_management()  # API 요청
        


```
