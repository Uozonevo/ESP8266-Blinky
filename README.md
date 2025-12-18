# ESP8266 Blinky Project

<!--![ESP8266 Image](ESP8266img.jpg)-->
<p>
<img align="left" hspace=20 src="ESP8266img.jpg"/> 
This is a test project to show that the ESP8266 board I acquired works as intended. To complete this project, I went through a number trials attempting to flash the LED on the RTC. <br>

On the left is an image of the board I will be using to show where the on-board LED is located, and the assorted I/O ports <br>

Also displayed is the USB to TTL driver: **Important to Note for later** 
</p>

## Progression 📈
To start this project, I looked at the data sheet for the ESP8266 nodeMCUv2 and reviewed where the LED was. I connected the board to my computer and opened up VSCode to see if it would show any serial ports. 

**Steps and Description**: 
1. Download ESP-IDF: I downloaded the ESP-IDF extension through VSCode for projects relating to ESP boards but realized this extension only applies to newer ESP32 boards. 
> [!NOTE]
> Decided to keep as I also acquired an ESP32 board for future projects

2. Download PlatformIO: After reading up on which IDE extension to use for my current board, I downloaded the PlatformIO extension in VSCode to set up my project
3. I selected the example blinky project from the PIO HOME and configured my environment to include the current board.
4. When I compiled the project, I received a compilation error stating that the included libraries were not recognized
> [!NOTE]
> For future references, I will compile from the PlatformIO activity bar for ease of access
5. I was able to bypass the compilation error and successfully build my project, until I ran into another error...
    Yes...My USB driver was not compatible for my device. So to make sure I got the right one, I went to my device manager and viewed the version number for my device which was **CP210x USB to UART Bridge Controller Driver**, a universal Windows Drvier.
> [!TIP]
> Make sure your USB driver is recognizable and up-to-date

6. After successfully installing the driver, my serial port was recognized as COM3, from here I could now build and upload my project onto the board.

## Manipulating and Testing the Code
From this point, the project was working great, but I wanted to understand how the rate at which the on-board LED was blinking

```C
gpio16_output_conf();
    while(true) {
    	gpio16_output_set(0);
        vTaskDelay(2000/portTICK_RATE_MS);
        gpio16_output_set(1);
        vTaskDelay(2000/portTICK_RATE_MS);
    }
```
Within this code snippet I manipulated the portTICK_RATE_MS from 1000 to 2000 to slow down the rate of blinking to 2 seconds in my forever loop.

 

<!--
> [!TIP]
> Optional information to help a user be more successful.

> [!IMPORTANT]  
> Crucial information necessary for users to succeed.

> [!WARNING]  
> Critical content demanding immediate user attention due to potential risks.

> [!CAUTION]
> Negative potential consequences of an action.
-->
