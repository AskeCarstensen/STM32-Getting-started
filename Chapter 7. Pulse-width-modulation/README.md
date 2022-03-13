# Chapter 7. Pulse-width-modulation
In this chapter you will learn about pulse-width-modulation (PWM):

- What PWM is
- How to setup PWM in CUBEMX
- How to use PWM to dim an LED

## Introduction: Pulse-witdh- modulation



## Setup: Setup timer for PWM



<p align="center">
    <img src = "setup_pwm_timer.png", width="800">
</p>


## Exercise: Dimming a led

In this exerise we are gonna use pwm for dimming an LED. 

```c
  /* Initialize all configured peripherals */
  MX_GPIO_Init();
  MX_USART2_UART_Init();
  MX_TIM1_Init();
  /* USER CODE BEGIN 2 */
  TIM1->CCR1 = 60; // set duty cycle of 60 %
  HAL_TIM_PWM_Start(&htim1, TIM_CHANNEL_1); // init pwm
```




<p align="center">
    <img src = "pwm_led_bb.png", width="800">
</p>
