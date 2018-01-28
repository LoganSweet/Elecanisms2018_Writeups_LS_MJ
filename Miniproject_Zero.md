# Elecanisms Miniproject 0: Blinking LED and Coin Collector
**Maggie Jakus and Logan Sweet**
Due: Tuesday, January 30

### Introduction ###
The purpose of this lab was to familiarize ourselves with the tools we need to program the PIC24 microcontroller. In addition to installing the needed tools, we also created a simple C program to change the behavior of the onboard LEDs. 


### Tools ###
To make use of the PIC24 microcontroller, we need some digital tools to interface with the microcontroller and load our C programs. 


### Hardware ###
We used a button to provide a signal to the digital pin on the microcontroller. Our button had one side connected to the onboard Vdd pin, and the other side connected to a 10k Ohm pulldown resistor to ground. We connected digital pin 0 to the button on the second button pin, between the button and the pulldown resistor. This means that when the button is not pressed D0 sees ground, and when it is pressed D0 seed Vdd. 


### C Code ###
We started with the example code provided to the class, and edited it so that LED 1 was activated by the signal from digital pin 0. Although we are familiar with the operation of both the blinkpoll and blinkint programs, blinkpoll was easier to understand since it did not use the interrupt handler. Since we more fully understood it, we chose to use 



```C
#include "elecanisms.h"

int16_t main(void) {
    init_elecanisms();

    T1CON = 0x0030;         // set Timer1 period to 0.5s
    PR1 = 0x7A11;

    TMR1 = 0;               // set Timer1 count to 0
    IFS0bits.T1IF = 0;      // lower Timer1 interrupt flag
    T1CONbits.TON = 1;      // turn on Timer1

    LED2 = ON;

    while (1) {
        if (IFS0bits.T1IF == 1) {
            IFS0bits.T1IF = 0;      // lower Timer1 interrupt flag
            LED2 = !LED2;           // toggle LED2
        }
        LED1 = (SW2 == 0) ? ON : OFF;   // turn LED1 on if SW2 is pressed 
        LED3 = (SW3 == 0) ? ON : OFF;   // turn LED3 on if SW3 is pressed
    }
}
```





**thing here** more text goes here 

here is how you make a list
 - Item 1 
 - Item 2 
 - Item 3 

## Another Heading ##

**Things that go here ** type of submission
 - text
 - more text
 - This might tab over below, unclear
   - Another thing will go here 
   - woo
   - Oh yeah look at our writeup



