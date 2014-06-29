#include <Adafruit_NeoPixel.h>

#define PIN 6
int stripLen = 16;
int sensorPin = A0;
int sensorVal;
int pixelPos;
int pixelOn;
int pixelOff;
int pixelMap;
int brightnessMap;

void setup() {
  Serial.begin(9600);
  strip.begin();
  strip.show(); // Initialize all pixels to 'off'
}

void loop() {
  sensorVal = analogRead(sensorPin); //   incoming values are 10-bit: 0 - 1023
  pixelPos = sensorVal/64; //             downsample to 4-bit values: 0 - 15 (number of pixels) 
  pixelMap = pixelPos*64; //              reverse upsample 4-bit values to 8-bit block-resolution

  brightnessMap = sensorVal - pixelMap; //map((sensorVal - pixelMap), 0, 63, 0, 255); // remap 0 - 63 to 0 - 255 (more precise than * 4)
  //Serial.println(brightnessMap);
  refresh(pixelPos, brightnessMap);
  //delay (10);

}

void refresh(int currentPos, int brightness){
  for (int j = 0; j < currentPos+1; j++){
    int greenMap = map(brightness, 0, 255, 0, 155);
    strip.setPixelColor(pixelPos, 0, brightness, brightness);
    strip.show();
  }  
  for (int i = stripLen; i > currentPos; i--){  
    strip.setPixelColor(i, 0, 0, 0); 
    strip.show();
  }
}


