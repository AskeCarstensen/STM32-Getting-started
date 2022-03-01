# Chapter 6. Analog-to-digital-conversion
In this chapter you will learn about analog-to-digital-conversion (ADC):

- What (ADC) is
- How to enable ADC 
- How to use ADC to read a measurement

## What ADC is 
For a microcontroller to use inputs from sensors we need ADCs to translate the real world analog signals to digital values the microcontroller can use.
The conversion is done by comparing the measured voltage with a reference

'''c
#include <string.h>
#include <stdio.h>
'''

'''c
/* Private variables ---------------------------------------------------------*/
ADC_HandleTypeDef hadc1;

UART_HandleTypeDef huart2;
'''

'''c
 /* USER CODE BEGIN 1 */
	uint16_t raw;
	char msg[10];

  /* USER CODE END 1 */
'''

'''c
/* USER CODE BEGIN WHILE */
  while (1)
  {

	  //Get ADC Value
	  HAL_ADC_Start(&hadc1);
	  HAL_ADC_PollForConversion(&hadc1,HAL_MAX_DELAY);
	  raw = HAL_ADC_GetValue(&hadc1);

	  //Print
	  sprintf(msg, "%hu\r\n",raw);
	  HAL_UART_Transmit(&huart2,(uint8_t*)msg,strlen(msg),HAL_MAX_DELAY);
	  HAL_Delay(1);
	  /* USER CODE END WHILE */
'''
