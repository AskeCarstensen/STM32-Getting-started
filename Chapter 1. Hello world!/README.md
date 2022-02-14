# Chapter 1. Hello world!


<p align="center">
    <img src = "STM32CubeLogo.png">
</p>
This chapter will walk you through setting up STM32CubeIDE for the first time and running HelloWorld on your board. This project uses the NUCLEO-F411RE board but this guide should be applicable to other STM as well.
Subchapters:

- Install STM32CubeIDE 
- Create a STM32 Project
- Toggle the on board LED every second.
- Toggle a external LED on a breadboard every second.
- Write “Hello There!” to putty over serial connection.


## Info: Install STM32CubeIDE
Download IDE from: https://www.st.com/en/development-tools/stm32cubeide.html

The STEM32CubeIDE contains presets for many stm32 boards as well as an easy to use interface to setup registers to peripherals and clock setup.

## Info: Create STM32 Project
To create your first STM32Project open the STM32CubeIDE and press "Start New STM32 Project":
<p align="center">
    <img src = "IDEHomepage.png"width="800">
</p>

In the window target select choose "Board selector" and type in your board name here shown with the NUCLE-F411RE development board:
 <p align="center">
    <img src = "IDEBoardSelect.png"width="800">
</p>
In the next window the project is defined by naming it, choosing the language, if it is an executable or library file and if STM32 is the target. Fill in the details and press next:
<p align="center">
    <img src = "IDEProjectSetup.png"width="350">
</p>
If this is the first time using a board the IDE will download the relevant board files and this might take a few minutes:
<p align="center">
    <img src = "BoardDownload.png"width="350">
</p>

Now the project is setup and the next step is to configure pins, write code and upload to the STM32.


## Exercise 1: Toggle the on board LED Every second

In the first exercise we are gonna toggle the on board LED. The first step is to find out which GPIO port and pin the led is located at. To find the pin configration open the project file and go to "Pinout & Configuration". In our case it is GPIOA pin5.
<p align="center">
    <img src = "PinConfig.png"width="800">
</p>

Then go to main.c. Here it is important that you only write code inside the comments with "USER CODE BEGINS" else it will be deleted every time you change the configuration.
<p align="center">
    <img src = "Mainc.png"width="800">
</p>

To toggle the LED pin we are gonna use the HAL libray made by STM. HAL is a hardware abstraction layer, that will allow us to use the same methods over a series of microcontrollers. As shown below, we start with the method "HAL_PGIO_TogglePin and then tell it we want to toggle GPIOA, pin 5. Followed by a HAL_Delay of one second.
```c
  /* Infinite loop */
  /* USER CODE BEGIN WHILE */
  while (1)
  {
	  HAL_GPIO_TogglePin(GPIOA, GPIO_PIN_5);
	  HAL_Delay(1000);

    /* USER CODE END WHILE */

    /* USER CODE BEGIN 3 */
  }
  /* USER CODE END 3 */
}
```

## Exercise 2: Toggle an external LED on a breadboard every second

In this exercise an off-board LED will be toggled using the following setup:

<p align="center">
    <img src = "BlinkLed_bb.png">
</p>

Then we need to assign a GPIO pin as a output, see image below.

<p align="center">
    <img src = "PinConfigAddPin.png"width="800">
</p>

Then we repeart the same method as the one we used in the last exercise.

```c
  /* Infinite loop */
  /* USER CODE BEGIN WHILE */
  while (1)
  {
	  HAL_GPIO_TogglePin(GPIOA, GPIO_PIN_5);
      HAL_GPIO_TogglePin(GPIOA, GPIO_PIN_10);
	  HAL_Delay(1000);

    /* USER CODE END WHILE */

    /* USER CODE BEGIN 3 */
  }
  /* USER CODE END 3 */
}
```

## Exercise 3: Write "Hello There!" to putty over serial connection.

Then 

<p align="center">
    <img src = "Putty.png"width="350">
</p>
<p align="center">
    <img src = "DeviceManager.png"width="350">
</p>





