# Chapter 3. Interupts

In this chapter you will learn about:

- How to setup a interrupt handler.

- Toggle an led with a external interrupt tigger. 

- Set hierarchy of a interrupt handler. 

## Exercise 1: Setup a interrrupt handler.

First we need to setup GPIOB pin 10 as a interrupt. To setup the interrupt you need to go to the "pinout & configuration", then find PB10 on the MCU and select "GPIO_EXTI10". 

<p align="center">
    <img src = "SET_INTERRUPT_B10.PNG" width="500">
</p>

Then code for the interrupt on GPIOB pin 10 will be generated. The interrupt handler function will be generated in the "stm32f4xx_it.c". You can find it at the same place as "main.c". In this file you should have a function as shown below.

```c
/**
  * @brief This function handles EXTI line[15:10] interrupts.
  */
void EXTI15_10_IRQHandler(void)
{
  /* USER CODE BEGIN EXTI15_10_IRQn 0 */
  
  /* USER CODE END EXTI15_10_IRQn 0 */
  HAL_GPIO_EXTI_IRQHandler(GPIO_PIN_10);
  HAL_GPIO_EXTI_IRQHandler(B1_Pin);
  /* USER CODE BEGIN EXTI15_10_IRQn 1 */

  /* USER CODE END EXTI15_10_IRQn 1 */
}
```

This mehtod will run every time GPIOB pin 10 goes high. From here we can make a led toggle or whatever one can imagine. But it is also important to remeber that the function will run, when any interrupt pin between 15-10 goes high.

## Exercise 2: Make a led toggle. 

First we are gonna repeart from Chapter 2, first setup GPIOB bin 5 as a GPIO output. Then setup GPIOB pin 10 with a pull down resistor. 

Then add HAL_GPIO_TogglePin to the code example. This will make the led toggle between states, for every interrupt.

```c
/**
  * @brief This function handles EXTI line[15:10] interrupts.
  */
void EXTI15_10_IRQHandler(void)
{
  /* USER CODE BEGIN EXTI15_10_IRQn 0 */
  HAL_GPIO_TogglePin(GPIOB, GPIO_PIN_5);
  /* USER CODE END EXTI15_10_IRQn 0 */
  HAL_GPIO_EXTI_IRQHandler(GPIO_PIN_10);
  HAL_GPIO_EXTI_IRQHandler(B1_Pin);
  /* USER CODE BEGIN EXTI15_10_IRQn 1 */

  /* USER CODE END EXTI15_10_IRQn 1 */
}
```

Take out your breadboard, copy the schemeatic below and run the code.

<p align="center">
    <img src = "interupt_bb.PNG" width="500">
</p>



## Extra: Interupt hierarchy

If you are building a bigger system, with multiple interrupts. It is important to set the hierarchy of the interrupts. You have to decide which are most system and time critical. To modify it, go to "Pinout & Configuration" then open System core and NVIC. Here one can set a priority where "0" is top prority.

<p align="center">
    <img src = "set_interrupt.PNG" width="500">
</p>

