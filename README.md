# Stepper Async 5 (Library for Arduino)

This is a library that modifies the Arduino 'Stepper' library to drive a step motor asynchronously.

Detailed explanation (Korean) : [[Arduino] StepperAsync5 - 비동기 스탭 모터 라이브러리](https://blog.danggun.net/7268)

<br />
The existing 'Stepper' library operates synchronously, so other operations cannot be performed while the stepper motor is operating. This library corrects these disadvantages and allows other operations while the stepper motor is running.

[![설명영상](https://img.youtube.com/vi/fQSO-O-tE_c/0.jpg)](https://youtu.be/fQSO-O-tE_c?t=0s)

## Index
  - [Overview](#overview) 
  - [Getting Started](#getting-started)
  - [Running the tests](#running-the-tests)
  - [Document](#document)
  - [Update history](#update-history)
  - [Contributing](#contributing)
  - [Authors](#authors)
  - [License](#license)


## Overview

- 'Stepper' 라이브러리와 동일한 선언 구조
- 'Stepper' 라이브러리와 동일한 사용 방법
- 메인 'loop'를 멈추지 않고 동작하여 비동기로 동작
- 여러 개의 스텝모터나 다른 동작을 동시에 할 수 있음


## Getting Started

- Download the file from [Releases](https://github.com/dang-gun/Arduino_StepperAsync5/releases)  or
- Create 'StepperAsync5.h' and 'StepperAsync5.cpp' and copy the source.
- (Arduino IDE 2.x 이상) 'Arduino IDE'에서 'Sketch > Include Library > Manage Libraries...'를 선택하여 'Library Manager'를 열어 'Stepper Async 5'를 설치해 줍니다.

Follow the instructions below to install.

### Prerequisites

Tested on Arduino 1.8.19

### Installing

('Library Manager'로 설치하였으면 이 과정은 필요 없습니다.)

Create 'StepperAsync5' folder in 'libraries' folder of Arduino IDE

Insert 'StepperAsync5.h', 'StepperAsync5.cpp'.

![Arduino_ButtonClickCheck_001](https://github.com/dang-gun/Arduino_ButtonClickCheck/assets/22692763/7f5401db-c170-4dd0-a4ab-208830573e62)

Launch the Arduino IDE and add the following code.


```
#include <StepperAsync5.h>
```


## Running the tests

Put the code below in your sketch to test it.

```
#include <StepperAsync5.h>

StepperAsync5 stepper(200, 12, 11, 10, 9);
StepperAsync5 stepper2(200, 7, 6, 5, 4);

void setup() 
{
  Serial.begin(9600);
  stepper.setSpeed(30);
  stepper2.setSpeed(60);
}

void loop() 
{
  if (Serial.available())
  {
    int steps = Serial.parseInt();

    if(steps != 0)
    {
      stepper.setStep(steps);
      stepper2.setStep(steps);
      //stepper.setStep(200);
      //stepper2.setStep(200);
  
      Serial.print("steps : ");
      Serial.println(steps); 
    }
    
  }
  
  stepper.moveStep();
  stepper2.moveStep();

}
```

![ButtonClickCheck_001_001](https://github.com/dang-gun/Arduino_ButtonClickCheck/assets/22692763/7b9c1dce-d523-4f1e-81da-683c7d5de399)  

![ButtonClickCheck_001_003](https://github.com/dang-gun/Arduino_ButtonClickCheck/assets/22692763/6ed0a0a9-4a79-429b-91c5-dd5e76fbfb1b)

## Document

Name|Description
---|---|
ButtonClickCheck(int nButtonUpLevel)|A library for button judgment<br />@param nButtonUpLevel The judgment value when the button is not pressed. LOW or HIGH
ButtonClickCheck(uint8_t uintPin, int nButtonUpLevel)|Library for judging buttons (specifying which pins to use)<br />@param uintPin pre-assign pins.<br />@param nButtonUpLevel Judgment value when the button is not pressed. LOW or HIGH
&nbsp;|&nbsp; 
int ClickCheck()|Read the value of the stored pin number to determine the click information.<br />@return 1=Up, 2=Down, 3=First Down, 4=First Up<br /><br />1=Up : The button is not pressed  <br />2=Down: The button is pressed  <br />3=First Down: The state where the button changed from Up to Down (output only once when changed)  <br />4=First Up: The state where the button changed from Down to Up (output only once when changed)
int ClickCheck(int nDigitalRead)|Read the delivered value to determine the click information.<br />@param nDigitalRead Input digital value (passed value)<br />@return 1=Up, 2=Down, 3=First Down, 4=First Up<br /><br />1=Up : The button is not pressed  <br />2=Down: The button is pressed  <br />3=First Down: The state where the button changed from Up to Down (output only once when changed)  <br />4=First Up: The state where the button changed from Down to Up (output only once when changed)
BtnPush2Set(bool bBtnPush2Value)|Set the existing state value 'bBtnPush2' to a desired value.<br />@param bBtnPush2Value Data to store in the existing state value. on=true, off=false

## Update history

#### 2023-06-04 : 
- Renamed 'StepperMulti5' to 'StepperAsync5'


## Contributing

'Fork' the project to create a 'new branch' and then 'pull request'.

## Authors
  - [dang-gun](https://github.com/dang-gun)

A list of non-updating contributors can be found at [contributors](https://github.com/dang-gun/Arduino_StepperAsync5/contributors).


## License
[GNU LESSER GENERAL PUBLIC LICENSE](https://github.com/dang-gun/Arduino_StepperAsync5/blob/main/LICENSE)
<br />
<br />


== 'Stepper' library ==
Copyright (c) Arduino LLC. All right reserved.<br />
Copyright (c) Sebastian Gassner. All right reserved.<br />
Copyright (c) Noah Shibley. All right reserved.<br />

This library is free software; you can redistribute it and/or
modify it under the terms of the GNU Lesser General Public
License as published by the Free Software Foundation; either
version 2.1 of the License, or (at your option) any later version.

This library is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU
Lesser General Public License for more details.

You should have received a copy of the GNU Lesser General Public
License along with this library; if not, write to the Free Software
Foundation, Inc., 51 Franklin St, Fifth Floor, Boston, MA 02110-1301 USA
