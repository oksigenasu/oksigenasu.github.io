---
layout: post
title:  "Hands on LoLin32 lite and SSD1306 OLED Display"
description: Finally its arrived!.
date:   2020-04-03 22:34:34 +000
categories: ESP32 OLED SSD1306 Hardware Arduino 
comments: true
---

## Finally its arrived! 

and without further ado, lets open them.

![cloned LoLin32 with red charging led](/assets/img/chargerled.jpeg)

Since lolin32 was retired, i knew the board that i got was a clone.  The downside from a clone is that sometimes its charging IC was bad and need replacement.  You can spot it when the charging led is blinking even though there were no battery attached. The prochedure to replace the IC can be followed  in [this youtube video](https://www.youtube.com/watch?v=a9f9vHjQSfQ).

![Tiny OLED](/assets/img/oled-lolin-soldered.jpeg)

The other thing that arrived is a 0.91" I2C OLED display.  Using SSD1306 driver, this display can be accessed using two-wire I2C.  I was quite dissapointed by the size (i know, i dont read what i bought), but surprisingly the display was clear and have a good contrast since every pixel has its own light.  Maybe next time, i should buy a bigger size.


## Wiring them together

At first i was about to connect them together using enameled copper wire.  But since i can't find my mother's wire wrapping pliers, i temporarely solder them using supplied pinheader.  And since i can't bend the pinhead, i need to get creative and connect the display to GPIO pins and drive them later to supply the power.
This is my setup:

|OLED   ||lolin32    |
|:-----:|-----|:---------:|
|SDA    |----->|GPIO18     |
|SCK    |----->|GPIO23     |
|VCC    |----->|GPIO19     |
|GND    |----->|GPIO22     |



![Wiring OLED and LoLin32 (creatively)](/assets/img/oled-lolin-wiring.jpg)

With this setup, i need to declare custom I2C pin and manually drive the GPIOs to supply vcc and gnd. 

## Testing with Arduino IDE

I use Arduino IDE and Adafruit SSD1306 Library to test this setup.  Since i already have ESP32 Platforms in Arduino IDE, i just need to select "WEMOS LOLIN 32" in my board manager to set this up. Another parameter to set is "Upload Speed:460800".  You can go lower speed if the upload failed.
Lets try the example from the library.  For this OLED display i used the "ssd1306_128x32_i2c" example.  For this setup i change the default i2c pin using `Wire.begin(sda,scl)` and also turn the GPIO to drive the OLED.  I add these code at the beginning of the `setup()` function.

```cpp
  Wire.begin(18,23);  //tell the wire lib to use custom pins

  pinMode(19, OUTPUT);  //this pin will be our VCC
  pinMode(22, OUTPUT);  //this pin will be our GND
  digitalWrite(19, HIGH);   //turn this pin to VCC
  digitalWrite(22,LOW);     //turn this pin to GND to drive the OLED
```
after uploading and running, the OLED display show the example demo with blazing speed!

## Make custom image

to make custom image, i use this [online converter](https://javl.github.io/image2cpp/) to convert and generate the code for the library.
![its so bright](/assets/img/oled-its-bright.jpeg)

next, i will try to make a WiFi NTP Clock with custom display animation.
until next time!
