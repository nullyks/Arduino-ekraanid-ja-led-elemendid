### Arduino UNO kood

Bitmapi loomisel kasutatud seda tööriista: http://www.majer.ch/lcd/adf_bitmap.php

~~~cpp
#include <Wire.h>
#include <Adafruit_GFX.h>
#include <Adafruit_SSD1306.h>

#define SCREEN_WIDTH 128 // Ekraani laius pikslites
#define SCREEN_HEIGHT 32 // Ekraani kõrgus pikslites
#define OLED_RESET    -1 // Ei kasuta eraldi reseti pinni
#define SCREEN_ADDRESS 0x3C // OLED ekraani I2C aadress

Adafruit_SSD1306 display(SCREEN_WIDTH, SCREEN_HEIGHT, &Wire, OLED_RESET);

const unsigned char heart_bitmap[] PROGMEM = {
  0x0C, 0x30,
  0x1E, 0x78,
  0x3F, 0xFC,
  0x7F, 0xFE,
  0x7F, 0xFE,
  0x3F, 0xFC,
  0x1F, 0xF8,
  0x0F, 0xF0,
  0x07, 0xE0,
  0x03, 0xC0,
  0x01, 0x80,
};

void setup() {
  if(!display.begin(SSD1306_SWITCHCAPVCC, SCREEN_ADDRESS)) {
    for(;;); //kui ei saa suheldud ekraaniga, siis lõputu tsükkel
  }
  display.clearDisplay();
  display.drawBitmap(10, 10, heart_bitmap, 16, 11, SSD1306_WHITE);
  display.setTextSize(1);
  display.setTextColor(SSD1306_WHITE);
  display.setCursor(30, 12);
  display.print("Syda"); // "Ü" asemel "y", kuna OLED ei pruugi toetada täpitähti
  display.display();
}

void loop() {
}
~~~