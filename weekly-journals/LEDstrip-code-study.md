﻿  
## **LED Arduino Sketch / Code Study**
  
```  
#include <FastLED.h>  
```  
FastLED library is used for controlling addressable LED strips  
```  
#define LED_PIN 5  
#define NUM_LEDS  150  
#define BRIGHTNESS  64  
#define LED_TYPE  WS2811  
#define COLOR_ORDER GRB  
CRGB leds[NUM_LEDS];  
  
```  
Parameters for LED setup.  
* `LED_PIN`: Arduino pin connected to the data input of the LED strip  
* `NUM_LEDS`: total number of LEDs in the strip  
* `BRIGHTNESS`: overall brightness of the LEDs  
* `LED_TYPE`: type of LED chip  
* `COLOR_ORDER`:  color order of the LEDS (for this it's green-red-blue)  
* `CRGB leds`: declares an array called 'leds' of type `CRGB`(color Red Green Blue), with the size of `NUM_LEDS`. this basically stores the color information for each LED in the strip  
  
```  
#define UPDATES_PER_SECOND 100  
int start_idx; int end_idx;  
```  
- indicates # of updates you wanna perform per second for the LED animation  
- declares two integer variables start/end, to keep track of the starting and ending indices of the LED segment light  
  
```  
void setup() {  
Serial.begin(9600);  
delay( 3000 ); // power-up safety delay  
FastLED.addLeds<LED_TYPE, LED_PIN, COLOR_ORDER>(leds, NUM_LEDS).setCorrection( TypicalLEDStrip );  
FastLED.setBrightness(  BRIGHTNESS );  
start_idx = 0;  
end_idx = 10;  
for(int i = 0; i < NUM_LEDS; i++){  
leds[i] = CRGB(0,0,0);  
}  
FastLED.show();  
  
}  
  
```  
Setup() Function;  
- Serial communication is initialized.  
-  3-second delay for power-up safety.  
- FastLED library is configured with the specified parameters.  
- Initial values for `start_idx` and `end_idx` are set.  
- The `leds` array is initialized with all LEDs turned off (black).  
- The initial state of the LEDs is displayed using `FastLED.show()`.  
  
  
```  
void loop()  
{  
count_5seconds();  
FastLED.show();  
FastLED.delay(1000 / UPDATES_PER_SECOND);  
count_15seconds();  
FastLED.show();  
FastLED.delay(1000 / UPDATES_PER_SECOND);  
  
}  
```  
loop() Function;  
- `count_5seconds()` and `count_15seconds()` functions are called, which will fill a segment of LEDs with red color for 5 and 15 seconds, respectively.  
- `FastLED.show()` is used to update the LEDs.  
- `FastLED.delay(1000 / UPDATES_PER_SECOND)` introduces a delay to control the speed of the animation.  
  
  
```  
void count_5seconds(){  
delay(5000);  
FillLED();  
start_idx += 10;  
end_idx += 10;  
if(end_idx >= NUM_LEDS){  
exit(0);  
}  
}  
```  
`count_5seconds()` function:  
  
- `delay(5000)`: There's a 5-second delay  
-  `FillLED()` : to set a segment of LEDs to red.  
- `start_idx` and `end_idx` are incremented by 10.  
- If `end_idx` becomes greater than or equal to `NUM_LEDS`, the program exits  
```  
void count_15seconds(){  
delay(15000);  
FillLED();  
start_idx += 10;  
end_idx += 10;  
if(end_idx >= NUM_LEDS){  
exit(0);  
}  
}  
```  
Count Functions:  
-  `count_5seconds()` and `count_15seconds()` functions delay for the specified duration, fill a segment of LEDs with red color using the `FillLED()` function, and then update the start and end indices.  
- If the end index exceeds or equals the total number of LEDs, the program exits.  
  
```  
void FillLED(){  
for(int i = 0; i < end_idx; i++){  
leds[i] = CRGB(255,0,0);  
}  
}  
```  
`FillLED()` function fills the LEDs in the range [0, end_idx) with red color (RGB: 255, 0, 0).


