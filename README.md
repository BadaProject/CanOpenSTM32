# CANopenNode STM32

CANopenSTM32은 [CANOpenNode](https://github.com/CANopenNode/CANopenNode) stack 기반의 STM32 마이컴에서 실행되는 CANopen stack이다.

## demos 실행 방법

예제는 [STM32CubeIDE](https://www.st.com/en/development-tools/stm32cubeide.html) 도구로 개발되었다. (공식 ST 개발 studio)
STM32CubeIDE에서 직접 프로젝트를 열고, 관련 보드에서 예제를 실행할 수 있다.

## repo 디렉토리

- `.\CANopenNode` : stack 구현. 이 부분을 건드릴 일은 거의 없다. (i.e. Linux, PIC, STM32 and etc.)
- `.\CANopenNodeSTM32` : STM32 마이크로컨트롤러에서 하위 드라이버 구현. 변경없이 CAN 기반 driver와 FDCAN 기반 driver를 모두 지원한다. 자동으로 컨트롤러 타입을 감지하고, STM32 HAL 라이브러리를 활성화한다.
- `.\examples` : 다양한 보드에 대한 예제. STM32F4-Discovery, STM32G0C1 Evaluation board, STM32F076 Nucleo Board, STM32H735G-Development Kit.
- `.\Legacy` : 예전  CANOpenSTM32 구현. 특히 FDCAN 컨트롤러용이지만 안정적이였고 FreeRTOS 구현 포함

## 지원하는 boards와 MCUs
 

### [STM32H735G-DK](https://www.st.com/en/evaluation-tools/stm32h735g-dk.html).
STM32H7xx 시리는 3개 CAN transceivers를 가지고 있다.
기존 CAN network에 연결하기 위해서는 추가적인 하드웨어가 필요하지 않다.
빌트인 programmer와 virtual COM port를 가지고 있어서, 평가보드로 작업하는 것이 쉽고 빠르다.

> CanOpen demo works at `FDCAN1` port. Use connector *CN18*.

> FDCAN IP block is same for any STM32H7xx MCU family, hence migration to your custom board should be straight-forward.

* STM32H735G-DK 보드를 박스에서 꺼내기
* Bare metal과 FreeRTOS OS 예제
* `FDCAN1` (*CN18*) 하드웨어는 125kHz로 통신하는데 사용
* CANopen LED control 잘 동작함
* Debug messages는 VCP COM port에서 `115200` bauds로 동작
* 제품을 개발하는데 참조 코드로 사용할 수 있다.



### [STM32G0C1VE-EV](https://www.st.com/en/evaluation-tools/stm32g0c1e-ev.html)
STM32G0C1E-EV 평가 보드는 STM32G0C1VET6 마이크로컨트롤러를 사용하는 고급 개발 플랫폼이다. 2개 CAN FD 컨트롤러와 물리적 레이어가 내장되어 있다.
기존 CAN network에 연결하기 위해서는 추가적인 하드웨어가 필요하지 않다.
빌트인 programmer와 virtual COM port를 가지고 있어서, 평가보드로 작업하는 것이 쉽고 빠르다.
> CanOpen 데모는 `FDCAN1` port에서 동작한다. connector *CN12*를 사용한다.
> FDCAN IP block은 모든 STM32G0xx MCU family에서 동일하다. 따라서 사용자의 커스텀 보드로의 이식은 간단하다.


### [NUCLEO-F303ZE](https://www.st.com/en/evaluation-tools/nucleo-f303ze.html) / [NUCLEO-F072RB](https://www.st.com/en/evaluation-tools/nucleo-f072rb.html) + [MAX33040ESHLD](https://www.digikey.ie/en/products/detail/analog-devices-inc-maxim-integrated/MAX33040ESHLD/13558019)

Nucleo는 arduino 호환 헤더를 가지고 있다. 이를 이용해서 MAX33040ESHLD를 추가할 수 있다. 이 bundle은 CAN 통신과 CANopen을 구성하는데 최소한의 요구사항을 만족시킨다.

이 프로젝트는 CubeMX 설정에 의존하므로, 사용자는 CubeMX를 사용해서 호환되는 설정을 제공해야 한다. (bitrate, interrupt activation 등)


### [STM32F4DISCOVERY](https://www.st.com/en/evaluation-tools/stm32f4discovery.html) + Any CAN Bus Physical Layer Module

pin mapping 관련해서 STM32CubeMX 설정 파일을 확인해보자.


## Video Tutorial
CANOpenNode Stack 과 CANOpenNodeSTM32 stack에 대한 개념을 잡기 위해서 아래 비디오를 참조한다. 기본적인 개념부터 구현과 포팅까지 설명한다.

[![CANOpen Node STM32 From basics to coding](https://img.youtube.com/vi/R-r5qIOTjOo/0.jpg)](https://www.youtube.com/watch?v=R-r5qIOTjOo)

>[00:00](https://www.youtube.com/watch?v=R-r5qIOTjOo&t=0s) Introduction and Overview [1:13](https://www.youtube.com/watch?v=R-r5qIOTjOo&t=73s) Why CAN ? [4:51](https://www.youtube.com/watch?v=R-r5qIOTjOo&t=291s) CAN Bus [8:55](https://www.youtube.com/watch?v=R-r5qIOTjOo&t=535s) Why CANOpen ? [13:27](https://www.youtube.com/watch?v=R-r5qIOTjOo&t=807s) CANOpen architecture [20:00](https://www.youtube.com/watch?v=R-r5qIOTjOo&t=1200s) Object dictionary [21:38](https://www.youtube.com/watch?v=R-r5qIOTjOo&t=1298s) Important CANOpen concepts [23:29](https://www.youtube.com/watch?v=R-r5qIOTjOo&t=1409s) PDO [27:25](https://www.youtube.com/watch?v=R-r5qIOTjOo&t=1645s) SDO [32:23](https://www.youtube.com/watch?v=R-r5qIOTjOo&t=1943s) NMT [33:25](https://www.youtube.com/watch?v=R-r5qIOTjOo&t=2005s) CANOpenNode Open-Source Stack [39:26](https://www.youtube.com/watch?v=R-r5qIOTjOo&t=2366s) STM32 Practical implementation [40:29](https://www.youtube.com/watch?v=R-r5qIOTjOo&t=2429s) CANOpen Tutorial code preparation [43:09](https://www.youtube.com/watch?v=R-r5qIOTjOo&t=2589s) Importing examples to STM32CubeIDE and programming them [47:04](https://www.youtube.com/watch?v=R-r5qIOTjOo&t=2824s) Examples explanation [57:00](https://www.youtube.com/watch?v=R-r5qIOTjOo&t=3420s) Porting to custom STM32 board [1:18:20](https://www.youtube.com/watch?v=R-r5qIOTjOo&t=4700s) EDS Editor (Object dictionary editor) [1:25:54](https://www.youtube.com/watch?v=R-r5qIOTjOo&t=5154s) Creating a TPDO [1:39:55](https://www.youtube.com/watch?v=R-r5qIOTjOo&t=5995s) Accessing OD Variables [1:54:08](https://www.youtube.com/watch?v=R-r5qIOTjOo&t=6848s) Creating an RPDO [2:05:50](https://www.youtube.com/watch?v=R-r5qIOTjOo&t=7550s) Using the SDOs [2:52:52](https://www.youtube.com/watch?v=R-r5qIOTjOo&t=10372s) Node guarding [3:04:38](https://www.youtube.com/watch?v=R-r5qIOTjOo&t=11078s) Transmitting PDOs manually



## 다른 STM32 마이크로컨트롤러로의 포팅할때 체크리스트 :
- STM32CubeMXIDE에서 새로운 프로젝트를 생성
- Configure CAN/FDCAN to your desired bitrate and map it to relevant tx/rx pins - Make sure yo activate Auto Bus recovery (bxCAN) / protocol exception handling (FDCAN)
- Activate the RX and TX interrupt on the CAN peripheral
- Enable a timer for a 1ms overflow interrupt and activate interrupt for that timer
- Copy or clone `CANopenNode` and `CANopenNodeSTM32` into your project directory 
- Add `CANopenNode` and `CANopenNodeSTM32` to Source locations in `Project Properties -> C/C++ General -> Paths and Symbols -> Source Locations`
  - add an exclusion filter for `example/` folder for `CANopenNode` folder
- Add `CANOpenNode` and `CANopenNodeSTM32` to `Project Properties -> C/C++ General -> Paths and Symbols -> Includes` under `GNU C` items
- In your main.c, add `#include "CO_app_STM32.h"`
  ```c
    /* Private includes ----------------------------------------------------------*/
    /* USER CODE BEGIN Includes */
    #include "CO_app_STM32.h"
    /* USER CODE END Includes */
  ```
  - Make sure that you have the `HAL_TIM_PeriodElapsedCallback` function implmented with a call to `canopen_app_interrupt`.

```c
void HAL_TIM_PeriodElapsedCallback(TIM_HandleTypeDef *htim)
{
  /* USER CODE BEGIN Callback 0 */

  /* USER CODE END Callback 0 */
  if (htim->Instance == TIM1) {
    HAL_IncTick();
  }
  /* USER CODE BEGIN Callback 1 */
  // Handle CANOpen app interrupts
  if (htim == canopenNodeSTM32->timerHandle) {
      canopen_app_interrupt();
  }
  /* USER CODE END Callback 1 */
}

```

- 여러분의 application에 따라서 아래 접근법 중에 하나를 선택한다. :

  ### Baremetal application 에서
- main.c 내에서 아래 코드를 USER CODE BEGIN 2에 추가한다.
  ```c
    /* USER CODE BEGIN 2 */
    CANopenNodeSTM32 canOpenNodeSTM32;
    canOpenNodeSTM32.CANHandle = &hcan;
    canOpenNodeSTM32.HWInitFunction = MX_CAN_Init;
    canOpenNodeSTM32.timerHandle = &htim17;
    canOpenNodeSTM32.desiredNodeID = 29;
    canOpenNodeSTM32.baudrate = 125;
    canopen_app_init(&canOpenNodeSTM32);
    /* USER CODE END 2 */
  ```

- main.c 내에서 아래 코드를 USER CODE BEGIN WHILE에 추가한다.
  ```c
  /* USER CODE BEGIN WHILE */
  while (1)
  {
	  canopen_app_process();
    /* USER CODE END WHILE */

  ```

  ### In FreeRTOS Applications
- CANOpen용 task를 생성한다. 우리는 `canopen_task`라고 부르고, 높은 우선순위를 가진다. 그리고 이 task에서 다음 코드를 사용한다. :

```c

void canopen_task(void *argument)
{
  /* USER CODE BEGIN canopen_task */
  CANopenNodeSTM32 canOpenNodeSTM32;
  canOpenNodeSTM32.CANHandle = &hfdcan1;
  canOpenNodeSTM32.HWInitFunction = MX_FDCAN1_Init;
  canOpenNodeSTM32.timerHandle = &htim17;
  canOpenNodeSTM32.desiredNodeID = 21;
  canOpenNodeSTM32.baudrate = 125;
  canopen_app_init(&canOpenNodeSTM32);
  /* Infinite loop */
  for(;;)
  {
	  //Reflect CANopenStatus on LEDs
    HAL_GPIO_WritePin(LED1_GPIO_Port, LED1_Pin, !canOpenNodeSTM32.outStatusLEDGreen);
    HAL_GPIO_WritePin(LED2_GPIO_Port, LED2_Pin, !canOpenNodeSTM32.outStatusLEDRed);
    canopen_app_process();
    // Sleep for 1ms, you can decrease it if required, in the canopen_app_process we will double check to make sure 1ms passed
    vTaskDelay(pdMS_TO_TICKS(1));
  }
  /* USER CODE END canopen_task */
}

```
> RTOS 어플리케이션내에서 OD 변수, CAN send, EMCY 변수에 접근할때 아주 주의해야한다. critical section을 lock해서 race conditions이 발생하지 않도록 해야한다. `CO_LOCK_CAN_SEND`, `CO_LOCK_OD`, `CO_LOCK_EMCY` 를 살펴보자.

- 타겟보드에서 프로젝트를 실행시킨다. startup 시점에 bootup 메시지를 볼 수 있어야 한다.

### Known limitations : 

- 하나의 STM32 장치에서 multi CANopen을 테스트하지 않았다. 하지만 원래 CANOpenNode는 multi 모듈을 사용할 수 있도록 구현되어 있다. 사용자가 직접 개발할 수 있다.

### Clone or update

git repo clone 및 submodules 가져오기:

```
git clone https://github.com/CANopenNode/CANopenSTM32
cd CANopenSTM32
git submodule update --init --recursive
```

기존 프로젝트 업데이트하기 (submodules 포함):

```
cd CANopenSTM32
git pull
git submodule update --init --recursive
```

## License

This file is part of CANopenNode, an opensource CANopen Stack. Project home page is https://github.com/CANopenNode/CANopenNode. For more information on CANopen see http://www.can-cia.org/.

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0
