# Chapter 5. USART!

In this chapter you will learn about:

- How to Configure Usart.

- Setup Putty for serial communication.

- How to transmit over serial from the nucelo board.
https://controllerstech.com/uart-transmit-in-stm32/
    - Transmit using POLL method
    - Transmit using interrupt
    - Transmit using DMA

- How to receive from serial on the nucelo baord.
https://controllerstech.com/uart-receive-in-stm32/
    - Receive with POLL method
    - Receive with interrupt
    - Receive with DMA

## Configure Usart on the nucleo
When we created the project, usart was setup with standard settings. The auto generated code can be found in main.c and is shown below.

```c
/**
  * @brief USART2 Initialization Function
  * @param None
  * @retval None
  */
static void MX_USART2_UART_Init(void)
{

  /* USER CODE BEGIN USART2_Init 0 */

  /* USER CODE END USART2_Init 0 */

  /* USER CODE BEGIN USART2_Init 1 */

  /* USER CODE END USART2_Init 1 */
  huart2.Instance = USART2;
  huart2.Init.BaudRate = 115200;
  huart2.Init.WordLength = UART_WORDLENGTH_8B;
  huart2.Init.StopBits = UART_STOPBITS_1;
  huart2.Init.Parity = UART_PARITY_NONE;
  huart2.Init.Mode = UART_MODE_TX_RX;
  huart2.Init.HwFlowCtl = UART_HWCONTROL_NONE;
  huart2.Init.OverSampling = UART_OVERSAMPLING_16;
  if (HAL_UART_Init(&huart2) != HAL_OK)
  {
    Error_Handler();
  }
  /* USER CODE BEGIN USART2_Init 2 */

  /* USER CODE END USART2_Init 2 */

}

```

In the given code snippet we can see: 
(Skal skrive om, mangler info)
- we are using USART2
- baudrate is set to 115200
- 8 bit
- parity is none
- tx rx
- flow ctl none
- oversampling is to 16

This is the standard settings for alot of devices, but if you need to change these paramertes. You need to go the the "Pinout & configuration" tab again. Then go to, connectivity -> USART2 -> Parameter settings. Here one can modify the diffrent parameters. After changing them, press "ctrl + s" and then new configeration will be gernerated. 


<p align="center">
    <img src = "usartconfig.png"width="350">
</p>

From here the 




## Setup putty to send commands.

First we need to setup putty to be able to send serial commands to our nucleo board. Set com port, baud rate and etc., like you did in chapter 1. Click on Terminal in the option menu to the right. Here we need to enable "implicit CR in every LF", local echo to "Force on". (see image)

<p align="center">
    <img src = "setupPutty.png"width="350">
</p>


## Transmit using POLL method

Poll method is the most simple way of transferring data. The down side of poll is, while transmitting the data it will block all other operation. The good thing about poll is, its good for transferring large amount of data simple and good if the programs jobs are only transferring over usart. 

The setup for poll is simple and was the one we used in chapter 1. The code snippet below shows a basic setup.

-  First we include string.h

``` c
/* Private includes ----------------------------------------------------------*/
/* USER CODE BEGIN Includes */
#include "string.h"
```

- Define a buffer

```c
int main(void)
{
  /* USER CODE BEGIN 1 */
	uint8_t buf[25];
```

- Then Copy a string to our buffer and transmit it.

```C
  /* Infinite loop */
  /* USER CODE BEGIN WHILE */
  while (1)
  {
	  strcpy((char*)buf, "Hello world\r\n");
	  HAL_UART_Transmit(&huart2, buf, strlen((char*)buf), HAL_MAX_DELAY);
	  HAL_Delay(1000);
```

In the code above we give HAL_UART_Transmit "HAL_MAX_DELAY" as a argument. This is the timeout timespan for the task. This is needed for any blocking process. HAL_MAX_DELAY timespan is multipel days and is only used if you dont care how long you are blocking. When you using poll you need to consider the timespan needed for your task, if the timespan is too short the task will terminated and the remaing data won't be sendt. 

Then to resolve this problem we can use interupt or DMA for transmitting the data.

## Transmit using Interrupt

The first step for setting up the usart interrupt is to enable it in NVIC Settings, go to Pinout & Configuration -> Connectivity -> USART2( or whatever port you are using) -> NVIC Settings. (See image below) Then press "ctrl + s" and generate the new code.

<p align="center">
    <img src = "setupInterrupt.png"width="350">
</p>

Then to transmit in interrupt mode call "HAL_UART_Transmit_IT". In the example below, a led is toggle every second, just as we did it in chapter 1., but this time we dont want to add the delay from transmitting 

```c
  /* Infinite loop */
  /* USER CODE BEGIN WHILE */
  while (1)
  {
	  strcpy((char*)buf, "Hello world\r\n");
	  HAL_UART_Transmit_IT(&huart2, buf, strlen((char*)buf));
	  HAL_Delay(1000);

```

One can then call 




