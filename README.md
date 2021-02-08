# 2021badge
Badge code for 2021
We are developing for the Raspberry Pi arch.


**Hardware:**


This is the hardware we are using to develop the badge, and thus what is known to work with our code:

Raspberry Pi Zero W (for example: https://www.adafruit.com/product/3708)

PiTFT Plus Assembled 320x240 2.8" TFT + Resistive Touchscreen (https://www.adafruit.com/product/2298)

DS3231 High Precision RTC Real Time Clock (https://www.amazon.com/gp/product/B01N1LZSK3/ref=ppx_yo_dt_b_asin_title_o06_s01?ie=UTF8&psc=1)

The real-time clock will have to be wired in, it can't directly plug into the header on the display due to the pin out.  We'll include instructions on the wiring along with the case design (which will have a place for the RTC to live) once the case design has been finalized.

**OS:**

Raspbian lite

**Language:**

Go for right now
