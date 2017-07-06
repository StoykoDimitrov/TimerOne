TimerOne Library for Arduino, ATTiny85, etc.
==============================================   
  
Stoyko Dimitrov's modified TimerOne library based on the Paul Stoffregen's TimerOne library. 
-----------------------------------------------

*This version provides 1 main benefit:*  

* **Support for ATTiny85** (except for the PWM functionality)
    
<hr />
  
Notes regarding ATTiny85 when using this library:
-----------------------------------------------  

1. This library can be used directly without any modifications to your existing code in case you are porting your code from Arduino to ATTiny85 except if you use the PWM functionality. The PWM functionality is still not implemented for ATTiny85.  
2. Make sure that no other library is using Timer1 when using the current TimerOne library with ATTiny85.  
3. Bear in mind that the maximum time period achievable with Timer1 on ATTiny85 is ~ half a second. Of course I am saying "maximum" here in the context of the TimerOne library. Otherwise if you need to achieve longer time period you can simply execute a custom sub-method in your custom method that is called on each interrupt. For example you can execute your custom sub-method every 4-th time when your custom method is called on each interrupt and that way you will expand the time 4 times (if you have set the timer to 500000 microseconds period through this approach you will achieve 4 x 0.5 seconds = 2 seconds).
4. millis() and micros() functions will be working with this library since they use Timer0 in the latest ATTinyCore's. Nevertheless if for some reason you need to use an older core for Attiny85 that uses Timer1 for millis() and micros() then you will have to change the value of TIMER_TO_USE_FOR_MILLIS variable of your core(it is located in "core_build_options.h" in older cores).
5. There is an example with ATTiny85 in the folder /examples.

Usage
-----------------------------------------------
Detailed description of the main methods and how they can be used can be found in the following link:
http://playground.arduino.cc/Code/Timer1

Download
-----------------------------------------------  
To download - click on the button "Clone or download" and then click the "Download ZIP" at the right side, extract the archive and rename the uncompressed folder TimerOne. Check that the TimerOne folder contains TimerOne.cpp and TimerOne.h  
Alternatively, you can download the latest release (1.2) from the releases section of this repository - https://github.com/StoykoDimitrov/TimerOne/releases/  
Here is the direct link for download of the current latest release:  
https://github.com/StoykoDimitrov/TimerOne/archive/1.2.zip  

Install
-----------------------------------------------  
To install the library - place the TimerOne library folder to your [Arduino IDE sketch folder]/libraries/ folder. You may need to create the libraries subfolder if its your first library. Restart the IDE. For more information you can also check the following link:  
https://www.arduino.cc/en/Guide/Libraries#toc5  
  
Original code  
-----------------------------------------------

https://github.com/PaulStoffregen/TimerOne  
http://playground.arduino.cc/Code/Timer1  

ATTiny85's unique Timer1 technical details:
-----------------------------------------------
ATTiny85's Timer1 is unique compared to any other Atmel microcontroller. It has features like achieving 64 MHz PWM via PLL, high resolution of Timer1 (although Timer1 is only 8 bit the high resolution is achieved through many prescalers available for this Timer). It is also interesting to note that Timer0 and Timer1 share the same register for timer interrupts - TIMSK therefore you can not just set this register to 0 when you detach an interrupt as it is being done in the detachInterrupt() method for Arduino but instead you have to only unset the exact bit responsible for the current timer (Timer1 in this case).

Open Source License
-----------------------------------------------
  
TimerOne is free software. You can redistribute it and/or modify it under
the terms of Creative Commons Attribution 3.0 United States License.
To view a copy of this license, visit  
  
http://creativecommons.org/licenses/by/3.0/us/
  
Stoyko Dimitrov forked this version from a copy of TimerOne by Paul Stoffregen
which was licensed "Creative Commons Attribution 3.0" and has maintained
the original "CC BY 3.0 US" license terms.  
  
Other, separately developed updates to TimerOne have been released by other
authors under the GNU GPLv2 license.  Multiple copies of this library, bearing
the same name but distributed under different license terms, is unfortunately
confusing.  This copy, with nearly all the code redesigned as inline functions,
is provided under the "CC BY 3.0 US" license terms.  
  
