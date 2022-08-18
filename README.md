# T-Display-S3
应该是 这个开发板刚出不久，TFT_eSPI库暂时还没有对于的配置文件，官方实例是把 官方repositories 中的修改过的 TFT_eSPI库替换 官方库。

官方：https://github.com/Xinyuan-LilyGO/T-Display-S3

在 TFT_eSPI 依赖库中，必要的配置
1. User_Setup.h 中
第 38 行 取消注释  
`#define TFT_PARALLEL_8_BIT`  
第 45 行 注释掉  
`#define ILI9341_DRIVER       // Generic driver for common displays`
第 55 行 取消注释  
`#define ST7789_DRIVER`
第 77 行 取消注释  
`#define TFT_RGB_ORDER TFT_BGR`
第 86 行 取消注释, 修改像素为172
`#define TFT_WIDTH  172 // ST7789 172 x 320`
第 91 行 取消注释, 修改像素为320
`#define TFT_HEIGHT 320 // ST7789 240 x 320`  
第 168, 169, 170 行 注释掉  
``
// #define TFT_CS   PIN_D8  // Chip select control pin D8
// #define TFT_DC   PIN_D3  // Data Command control pin
// #define TFT_RST  PIN_D4  // Reset pin (could connect to NodeMCU RST, see next line)
``  
第 234 行 取消注释  
`#define TFT_BL   38  // LED back-light (required for M5Stack)`  
第 247-264 行 取消注释， 并修改对应引脚
``
// Tell the library to use 8 bit parallel mode (otherwise SPI is assumed)
#define TFT_PARALLEL_8_BIT
// The ESP32 and TFT the pins used for testing are:
#define TFT_CS   6  // Chip select control pin (library pulls permanently low
#define TFT_DC   7  // Data Command control pin - must use a pin in the range 0-31
#define TFT_RST  5  // Reset pin, toggles on startup
#define TFT_WR   8  // Write strobe control pin - must use a pin in the range 0-31
#define TFT_RD   -1  // Read strobe control pin
#define TFT_D0   39  // Must use pins in the range 0-31 for the data bus
#define TFT_D1   40  // so a single register write sets/clears all bits.
#define TFT_D2   41  // Pins can be randomly assigned, this does not affect
#define TFT_D3   42  // TFT screen update performance.
#define TFT_D4   45
#define TFT_D5   46
#define TFT_D6   47
#define TFT_D7   48
``  

第 338 ~ 345 行 修改频率为5000000  
``
// #define SPI_FREQUENCY   1000000
#define SPI_FREQUENCY   5000000
// #define SPI_FREQUENCY  10000000
// #define SPI_FREQUENCY  20000000
// #define SPI_FREQUENCY  27000000
// #define SPI_FREQUENCY  40000000
// #define SPI_FREQUENCY  55000000 // STM32 SPI1 only (SPI2 maximum is 27MHz)
// #define SPI_FREQUENCY  80000000
``

2. 在 User_Setup_Select.h 中
第 52 行 取消注释  
`#include <User_Setups/Setup24_ST7789.h>            // Setup file for DSTIKE/ESP32/ESP8266 configured for ST7789 240 x 240`  
3. 在 User_Setups/Setup24_ST7789.h ，经对比，大部分修改，更好的做法应该是新建一个配置文件。
