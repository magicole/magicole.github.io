---
layout: single
title: STM32F0 Cheat Sheet
excerpt: Common configurations for the STM32F0 MCU
categories: microcontrollers
---

Below are some common things done while using STM32 MCUs. This should be used as a quick reference.

* toc
{:toc}

## GPIO Setup

### Input

```c
//This example will use PA0 as an input
//enable the GPIO bank on the AHB, all GPIO banks are on the AHB
RCC->AHBENR |= RCC_AHBENR_GPIOAEN;  //enable GPIOA
//configure GPIO pin as input
GPIOA->MODER &= ~((1 << 0) | (1 << 1)); //set PA0 to input
//set the input speed
GPIOA->OSPEEDR &= ~(1 << 0); //set PA0 to low speed
//set pull-up or pull-down resistor
GPIOA->PUPDR |= (1 << 1); // set PA0 to use Pull-down resistor
GPIOA->PUPDR &= ~(1 << 0);
//read input state
intGPIOA->IDR & (1 << 0);
```

### Output

```c
//This example will use PC6 as an output
//enable GPIO bank on the AHB, all GPIO channels are on the AHB
RCC->AHBENR |= RCC_AHBENR_GPIOCEN; //enable GPIOC
//set the pin mode to output
GPIOC->MODER |= (1 << 12); //set pin PC6 to output
GPIOC->MODER &= ~(1 << 13);
//set push-pull or open-drain output type
GPIOC->OTYPER &= ~(1 << 6); //set push pull output type for PC6
//set pin speed
GPIOC->OSPEEDR &= ~(1 << 12); //set low speed output on pin PC6
//set pull-up or pull-down resistor
GPIOC->PUPDR &= ~((1 << 12) | (1 << 13)); //set no Pull-up or Pull-down for PC6
//set output state
GPIOC->ODR |= (1 << 9); //set PC9 (green) to high
```

## Interrupt setup

Interrupt handler names are stored in startup_stm32f072xb.s

Interrupt IRQn numbers are stored in stm32f072xb.h

### Timers

```c
//Timer interrupt configuration code goes here
```

### External

```c
//external interrupt configuration code goes here
```

## PWM

```c
//PWM configuration code goes here
```

## Communication

### Serial/TTL RS232

```c
//This example will use USART3 on PC10 (Tx) and PC 11 (Rx)
//Enable the GPIO pins and USART on their respective busses
RCC->AHBENR |= RCC_AHBENR_GPIOCEN; //enable GPIOC on the AHB
RCC->APB1ENR |= RCC_APB1ENR_USART3EN; //enable USART3 on the APB
//set the GPIO pins to use their alternate function
GPIOC->MODER |= (1 << 21); //set PC10 to Mode 0x10 Alternate Function
GPIOC->MODER &= ~(1 << 20);
GPIOC->MODER |= (1 << 23); //set PC11 to Mode 0x10 Alternate Function
GPIOC->MODER &= ~(1 << 22);
//set which alternate function to use
GPIOC->AFR[1] |= (1 << 8); //set PC10 to alternate function mode 1 USART3_TX
GPIOC->AFR[1] |= (1 << 12); //set PC11 to alternate function mode 1 USART3_RX
//configure the baudrate
int brr = HAL_RCC_GetHCLKFreq() / 115200;
USART3->BRR = brr;
//enable the components of the USART
USART3->CR1 |= (1 << 3); //enable TX
USART3->CR1 |= (1 << 2); //enable RX
USART3->CR1 |= (1); //enable the entire USART3
//write to the USART
while((USART3->ISR & (1 << 7)) == 0){} //wait until the Transmit Data Register Empty flag is set
USART3->TDR = 'a';
//read from the USART
while(!(USART3->ISR & (1 << 5))){} //wait until the RX Not Empty Register is set
char input = USART3->RDR;

//Optional interrupt configuration, do this before enabling the USART
//tell the USART to trigger an interrupt when Rx is not empty
USART3->CR1 |= (1 << 5); //enable RX Not Empty Interrupt
//tell the NVIC to enable the interrupt for USART3/USART4
NVIC_EnableIRQ(USART3_4_IRQn); //enable the USART3 interrupt in the NVIC

void USART3_4_IRQHandler(void){
    //handle incoming data here
    char data = USART3->RDR;
}
```

### I2C

```c
//I2C configuration code goes here
```

## Misc.

### Delay

```c
//number of ms to delay
HAL_Delay(200);
```