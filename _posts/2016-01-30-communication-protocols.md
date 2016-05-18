---
layout: post
title: An Alphabet Soup of Communication Protocols
---

*By Radhika Ghosal*

Before you start reading, this is just to serve as an introduction to the
TinkerEve we'll be hosting on Wednesday on communication protocols (obviously),
like SPI, I2C, and a few more if time permits.

So, what is this beast called a 'communication protocol'? Your USB drive, Ethernet cable,
SD card, all use some communication protocol or the other to talk to your computer.

Ever interfaced an LCD display with an Arduino? Well, the code for that on the
Arduino IDE looks something like:

{% highlight C++ %}
// include the library code:
#include <LiquidCrystal.h>

// initialize the library with the numbers of the interface pins
LiquidCrystal lcd(12, 11, 5, 4, 3, 2);

void setup() {
    // set up the LCD's number of columns and rows:
    lcd.begin(16, 2);
    // Print a message to the LCD.
    lcd.print("hello, world!");
}

void loop() {
}
{% endhighlight %}

That's rather cute. But in reality, the Arduino IDE does most of the heavy lifting
for us and abstracts out the internal working of the LCD display. In fact, the actual
code for writing to an LCD display in AVR C looks more like:

{% highlight C %}
// This is just a snippet of the entire program for writing to an LCD
#include <avr/io.h>
#include <util/delay.h>

void SendCommand(unsigned char command)
{
    CheckIfBusy();
    PORTB = command;
    PORTD &= ~((1<<2)|(1<<2)); //turn off RS (command mode) and RW (write mode)
    BlinkLight();
    DDRB = 0;
}

void SendCharacter(unsigned char character)
{
    CheckIfBusy();
    PORTB = character;
    PORTD &= ~(1<<7); //turn off RW (write mode)
    PORTD |= (1<<2); //turn on RS (character display mode)
    BlinkLight();
    DDRB = 0;
}
{% endhighlight %}

If you're in the first year, and your Introduction to Engineering Design project
involves pretty screens or lots of fancy sensors, we advise you to attend the session.
We look forward to seeing you at our TinkerEve on Wednesday, 5:30PM, at C02.
