# -Camp51.9-

아두이노 코드
예제 Adafruit_NeoMatrix  ->  matrixtest 참조

#include <Adafruit_GFX.h>
#include <Adafruit_NeoMatrix.h>
#include <Adafruit_NeoPixel.h>
#ifndef PSTR
#define PSTR
#endif

#define PIN 6

Adafruit_NeoMatrix matrix = Adafruit_NeoMatrix(24, 8, PIN,           // 네오픽셀 n X n 입력
  NEO_MATRIX_TOP     + NEO_MATRIX_RIGHT +
  NEO_MATRIX_COLUMNS + NEO_MATRIX_PROGRESSIVE,
  NEO_GRB            + NEO_KHZ800);

const uint16_t colors[] = {
  matrix.Color(255, 0, 0), matrix.Color(0, 255, 0), matrix.Color(0, 0, 255) };

void setup() {
  matrix.begin();
  matrix.setTextWrap(false);
  matrix.setBrightness(40);
  matrix.setTextColor(colors[0]);
}

int x    = matrix.width();
int pass = 0;

void loop() {
  matrix.fillScreen(0);
  matrix.setCursor(x, 0);
  matrix.print(F("Welcome to Camp 51.9"));    //원하는 글자 입력
  if(--x < -130) {                            // 네오픽셀 글자 노출시간
    x = matrix.width();
    if(++pass >= 3) pass = 0;
    matrix.setTextColor(colors[pass]);
  }
  matrix.show();
  delay(50);                                  //글자 빠르기
}
