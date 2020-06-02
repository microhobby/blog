
The Netduino platform has been among us since 2010. And now in 2020, 10 years later, [it has been discontinued](https://www.wildernesslabs.co/netduino). 

![Netduino 3 Wi-Fi](https://github.com/microhobby/blog/blob/master/img/netduino3-wifi.png?raw=true)

As you can see in the photo it has the same form factor and design as the Arduino, pin-compatible with the Arduino Shields by the way. Here in Brazil, where I live, he was never very popular. But I met some people who came to have and use it.

One of Netduino's differentials was its 32-bit microcontroller and a software ecosystem that allowed it to run C# code on top of the .NET Micro Framework using Visual Studio and its debugging tools.

Netduino was a start for other tools and platforms that focus on using C# and .NET for microcontrollers that emerged.

## Netduino Hardware

I will talk about the hardware that I have here. But the project had many other models, see here a complete list: [https://github.com/WildernessLabs/Netduino_Hardware](https://github.com/WildernessLabs/Netduino_Hardware)

Let's talk about the Netduino 2 specs:

- 32-bit ARM Cortex M3 @ 120 MHz (STM32F205RFT6)
- 22 GPIOs (SPI, I2C, 2 UARTS, 4 PWM and 6 ADC)
- 192 KB Flash
- 60 KB SRAM
- Input 7.5 - 9.0 VDC
- Micro USB Input
- 5V and 3.3V (regulated)
- Digital I/O 3.3V (5V tolerant)
- ROHS
- Operating Temperature 0 to 70 ºC

## Netduino Firmware Stack

This is the software stack used by the .NET Micro Framework:

![Netduino Software Stack](https://raw.githubusercontent.com/microhobby/blog/master/img/netduinoSoftwareStack.png?token=AAUC42IYVJCDUZHHYCZ3ONS62R6HM)

- User Code or the Application
	- Is the C# code compiled to the CIL (Common Intermediate Language);
-  .NET Micro Framework
	- Subset of common .NET Llibraries;
- TinyCRL OS
	- CLR (Common Language Runtime) will execute the CIL natively;
	- PAL (Platform Abstraction Layer) additional abstraction, memory blocks, timers and I/O;
	- HAL (Hardware Abstraction Layer) direct access to hardware and common peripherals;

## Netduino Software Ecosystem

The idea of using C# in microcontrollers with Netduino would come in conjunction with all the experience that .NET platform developers are used to. So you had an awesome Visual Studio extension to develop your applications. This extension makes development very transparent with commands for deploy, upload the application to the target board, and step by step debugging.

![Netduino Button interrup Break Point](https://github.com/microhobby/blog/blob/master/img/netduino-interrupt-inaction.gif?raw=true)

# It's Time to Say Goodbye 😢

The coolest thing about the platform was its software ecosystem. It was really easy to develop your application using C#, your knowledge of .NET Framework, Visual Studio, and the powerful debug tools to play in the world of embedded microcontrolled systems.

It was a pity that the project has been discontinued. But it was time, since 2017 that it had not been receiving much maintenance. For example, the support of the visual studio extension was stopped in Visual Studio 2015 and never won a new version. The .NET Micro Framework Github repository was archived and etc ...

Initially, the project had been created under the name of Secret Labs. At the end of 2016, it was acquired by [Wilderness Labs](https://www.wildernesslabs.co/) who kept the project "breathing" until 05/2020. And they have plans for a successor the [Meadow Platform](https://www.wildernesslabs.co/developers),  that is still in its [beta stages](http://developer.wildernesslabs.co/Meadow/). (I will talk more about the meadow as soon as my sample hardwar arrives here in Brazil)

Also another alternative is the [nanoFramework](https://github.com/nanoframework), which was a community response to the lack of maintenance on the .NET Micro Framework project. I will explore nanoFramework better in another article.

But all good things come to an end, so **Rest In Peace Netduino**
