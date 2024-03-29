# pyneospider

네오스파이더를 Python을 통하여 제어하면서 학습할 수 있는 라이브러리입니다.

## INSTALL

Python 3버전(>=3.6)을 기준으로 작성되었으며, 설치해야하는 패키지는 다음과 같습니다.

```bash
$ pip install pyserial
$ pip install pyneospider
```

## NeoSpider

`pyneospider` 라이브러리 안에 `NeoSpider` 클래스가 있습니다.

해당 클래스를 인스턴스화 하여 사용하시면 됩니다.

교구의 대한 내용은 아래의 링크를 참조하시면 됩니다.

[http://neo3ds.com/goods/goods_view.php?goodsNo=1000000071](http://neo3ds.com/goods/goods_view.php?goodsNo=1000000071)

## NeoSpider 메서드 소개

### [public method]: 📤출력

#### 1. connect

Comport와 연결할 수 있는 메서드입니다.

> @params
>
> comport: 컴포트 작성 파라미터
>
> baudrate: 보드레이트 설정 파라미터
>
> ex) connect('COM3')

```python
from pyneospider import NeoSpider # 라이브러리 import

ns = NeoSpider() # 인스턴스화

ns.connect('COM3') # COM3번과 연결 -> Comport 번호는 사용자마다 상이함
```

#### 2. close

Comport 연결 해제 메서드입니다.

> ex) close()

```python
from pyneospider import NeoSpider

ns = NeoSpider()

ns.connect('COM3')

ns.close() # Comport 연결 해제
```

#### 3. move

##### 3-1. move

네오스파이더 이동 구동할 수 있는 메서드입니다.

> @params
>
> direct: 방향을 정하는 파라미터
>
> 0 -> 정지
>
> 1 -> 앞으로
>
> 2 -> 왼쪽으로
>
> 3 -> 오른쪽으로
>
> 4 -> 뒤로
>
> ex) move(1)

```python
from pyneospider import NeoSpider
import time # 시간 라이브러리 import

ns = NeoSpider()

ns.connect('COM3')

ns.move(1) # 앞으로 이동
time.sleep(3) # 3초 지연
ns.move(0) # 정지

ns.close()
```

##### 3-2. move_secs

네오스파이더 이동 구동할 수 있는 메서드입니다.

> @params
>
> direct: 방향을 정하는 파라미터
>
> 0 -> 정지
>
> 1 -> 앞으로
>
> 2 -> 왼쪽으로
>
> 3 -> 오른쪽으로
>
> 4 -> 뒤로
>
> secs: 움직일 시간
>
> ex) move_secs(1)

```python
from pyneospider import NeoSpider
import time # 시간 라이브러리 import

ns = NeoSpider()

ns.connect('COM3')

ns.move_secs(3) # 앞으로 3초간 이동

ns.close()
```

#### 4. stop

네오스파이더 구동 정지 메서드입니다.

> ex) stop()

```python
from pyneospider import NeoSpider
import time

ns = NeoSpider()

ns.connect('COM3')

ns.move(1)
time.sleep(3)
ns.stop() # 정지

ns.close()
```

#### 5. tone

네오스파이더 **SOUND모듈** 제어 메서드입니다.

> @params
>
> octave: 옥타브 (0~7)
>
> note: 음계 ('도', '도#', '레', '레#', ..., '시')
>
> duration: 시간/s
>
> ex) tone(3, '도', 0.3)

```python
from pyneospider import NeoSpider
import time

ns = NeoSpider()

ns.connect('COM3')

ns.tone(3, '도', 0.3)
time.sleep(0.2)
ns.tone(3, '도', 0.3)
time.sleep(0.2)

ns.close()
```

#### 6. num_rgb_led

네오스파이더 모듈에 있는 RGB LED를 각각 제어할 수 있는 메서드입니다.

> @params
>
> num: 모듈 위치 (0~7)
>
> r: 빨강색 세기 정도 (0~255)
>
> g: 초록색 세기 정도 (0~255)
>
> b: 파란색 세기 정도 (0~255)
>
> ex) num_rgb_led(2, 70, 100, 130)

```python
from pyneospider import NeoSpider
import time

ns = NeoSpider()

ns.connect('COM3')

ns.num_rgb_led(0, 50, 0, 0)
ns.num_rgb_led(2, 0, 50, 0)
ns.num_rgb_led(4, 0, 0, 50)
ns.num_rgb_led(6, 50, 0, 50)

time.sleep(3) # 연결 해제되기 전에 확인하기 위한 지연

ns.close()
```

#### 7. all_rgb_led

네오스파이더 모듈에 있는 RGB LED 모두를 제어할 수 있는 메서드입니다.

> @params
>
> r: 빨강색 세기 정도 (0~255)
>
> g: 초록색 세기 정도 (0~255)
>
> b: 파란색 세기 정도 (0~255)
>
> ex) all_rgb_led(50, 100, 150)

```python
from pyneospider import NeoSpider
import time

ns = NeoSpider()

ns.connect('COM3')

ns.all_rgb_led(0, 0, 100)
time.sleep(3)

ns.close()
```

#### 8. all_rgb_led_off

네오스파이더 모듈에 있는 RGB LED 모두 OFF 메서드입니다.

> ex) all_rgb_led_off()

```python
from pyneospider import NeoSpider
import time

ns = NeoSpider()

ns.connect('COM3')

ns.all_rgb_led(0, 0, 100)
time.sleep(3)
ns.all_rgb_led_off()
time.sleep(2)

ns.close()
```

#### 9. output_motor

네오스파이더 **OUTPUT** 외부모터제어모듈 제어 메서드입니다.

:warning:D5번에 값을 주면 D6번에 값을 0으로 주어야 합니다. 반대로도 동일합니다.

> @params
>
> d5: digital 5 pin 제어 (0~255)
>
> d6: digital 6 pin 제어 (0~255)
>
> ex) output_motor(150, 0)

```python
from pyneospider import NeoSpider
import time

ns = NeoSpider()

ns.connect('COM3')

ns.output_motor(0, 150)
time.sleep(3)

ns.close()
```

#### 10. head_angle

네오스파이더 고개를 제어하는 메서드입니다.

> @params
>
> angle: 고개 각도 (50~130)
>
> ex) head_angle(60)

```python
from pyneospider import NeoSpider
import time

ns = NeoSpider()

ns.connect('COM3')

ns.head_angle(60)
time.sleep(3)

ns.close()
```

### [public method]: 📥입력

입력에는 값을 한번 받아야 하는 경우도 있지만, 보편적으로 지속적으로 받아야 하기에 while문과 함께 쓰이는 경우가 많습니다.

:warning:아직 라이브러리의 안정성 문제로 인하여 입력 값들이 지연되는 경우가 있습니다. `print` 출력을 통하여 값을 확인을 꼭 해주세요.

#### 1. get_gas_sensor

가스 모듈의 값을 가져옵니다. (0~1023)

```python
from pyneospider import NeoSpider
import time

ns = NeoSpider()

ns.connect('COM3')

try: # 강제 종료를 위한 try~except 예외 처리
	while True: # 무한 루프 while문
        gas_value = ns.get_gas_sensor() #가스 센서값 변수에 담기
        print(gas_value) # 가스 센서값 확인

except KeyboardInterrupt: # `ctrl + c` 강제 종료시 처리할 부분
    print('강제 종료')
    ns.close()
except Exception as e: # 에러 발생시 처리할 부분
    print("에러: {}".format(e))
    ns.close()

ns.close()
```

함수 호출 부분을 제외하고는 아래 부분부터는 코드를 생략하겠습니다.

:warning:정확한 값을 가져오기 위해서는 해당 모듈이 네오스파이더에 꽂아 있어야합니다.

#### 2. get_cds_sensor

조도 센서 모듈의 값을 가져옵니다. (빛의 밝기 정도 -> 어두우면 값이 높고 밝으면 낮음, 0~1023)

#### 3. get_temp_sensor

온도 센서 모듈의 값을 가져옵니다. (변환된 온도값)

:warning:온도 센서에서 오래 켜두면 PCB의 과열로 인하여 온도가 조금씩 높아지는 현상이 발생하기도 합니다.

#### 4. get_vibe_sensor

진동 센서 값을 가져옵니다. (0~1023)

#### 5. get_input_sensor

외부 INPUT 모듈 값을 가져옵니다. (0~1023)

:warning:INPUT 모듈은 GAS 모듈과 동일한 핀을 사용하고 있습니다. 2개를 동시에 사용하면 올바르지 못한 값을 가져올 수 있습니다.

#### 6. get_left_infrared

왼쪽 적외선 센서의 감지를 했는지 결과를 리턴합니다. (감지시 True / 미감지시 False)

#### 7. get_right_infrared

오른쪽 적외선 센서가 감지를 했는지 결과를 리턴합니다. (감지시 True / 미감지시 False)

#### 8. get_ultrasonic

초음파 센서가 감지한 거리값을 가져옵니다. (단위 cm / 소수점 2자리까지 허용)

#### 9. get_motion

모션 센서가 감지 했는지 결과를 리턴합니다. (감지시 True / 미감지시 False)

### [private method]🔒

#### 1. \_\_check_sum

데이터를 검증하기 위한 메서드입니다.

> @params
>
> check_list: 검증할 2차원 리스트
>
> @return sum_value & 255

#### 2. \_\_write_data

시리얼로 데이터를 보내기 위한 메서드입니다.

#### 3. \_\_init_data

데이터 초기화 메서드입니다.

#### 4. \_\_read_data

데이터 수신 메서드입니다.

#### 5. \_\_read_thread

데이터 수신 메서드를 상시적으로 확인하기 위해서 있는 Thread:Daemon 메서드입니다.
