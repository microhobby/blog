Here a list of my favorite 2020 technologies:

> ⚠️ Remembering that this list is based only and ONLY on my humble opinion 💩 and are more related to my area of expertise (embedded systems, embedded Linux)! These were technologies that I had the opportunity to work and test during 2020.

I will divide the "award" into classes and in each one I will point out my winner within that class and the one that I think is a "promise" or that we should keep an eye on because it is a technology highlighted in the market. So, let's to the "MicroHobby top tech 2020" winners!

### Programming Language

![top languages 2020](https://github.com/microhobby/blog/blob/master/img/retro-lang.png?raw=true)

- My Winner: **C#**
- Highlighted: **Python**

C# with .NET Core 3.1 or .NET 5 for Embedded Linux systems has very useful, either for headless or GUI applications. The language interoperability is fantastic, super easy and transparent to access native libraries. The platform is very robust and optimized to run on armv7 and armv8. We also have C# running for microcontrollers with `NanoFramework` and `Meadow OS`.

Python is the highlighted language. I personally don't like the language (my personal opinion!!!). But by the ecosystem and community, the platform has many facilities, libraries that make your work easy. I have been working with python with my current employer in one of the projects so, no way to escape, python is very popular and the trend is just to grow. Even though the language is not one of my favorites, it is good to keep an eye and improve the skills.

### Linux Distro

![top linux distro 2020](https://github.com/microhobby/blog/blob/master/img/retro-distro.png?raw=true)

- My Winner: **Ubuntu**
- Highlighted: **Alpine**

I usually change my mind about Linux distros. If I were to choose my favorite distro in the middle of the year I would choose without even thinking: DEBIAN! But now at the end of the year my choice goes to Ubuntu, for the great support with WSL community. In fact I have not seen much interest from the Debian community with WSL 😢. I even offered to help with the Debian Distro support for WSL 2, but I was kind of ignored (again making it clear that this is my opinion, maybe I misinterpreted it 🤷‍♂️). Well, with that said, and I have been using WSL 2 more and more in my day to day, so I will stay in Ubuntu that has an AMAZING support for the WSL community.

Alpine, my dear Alpine! Choose as highlight because it is not that distro that I will use as a desktop distro, and I think this is not even his premise. It is popular in the world of Docker containers because it is minimal, based on BusyBox, uses `musl` instead of `glibc`, etc. And because of that, it has been a great choice as a minimal ready Linux distro for embedded systems.

### Code Editor

![top ide 2020](https://github.com/microhobby/blog/blob/master/img/retro-ide.png?raw=true)

- My Winner: **VS Code**
- Highlighted: **Codespaces**

VS Code rocks 😎. "Ohhh but he's not an IDE, he's just a code editor" 🙄. VS Code has trillions of extensions, you can build your own IDE for whatever you want to do! Furthermore the API for writing extensions is the easiest and most beautiful thing I have ever seen. And I speak properly, I develop extensions for both VS Code and VS 2019 and the VS 2019 extensions API is a horror movie with a bad script compared to the VS Code API. TRUST ME!

In a nutshell, Codespaces is the VS Code that runs in the cloud on your browser, so no more. NEXT!

### Microcontrolled Board

![top microcontrolled boards 2020](https://github.com/microhobby/blog/blob/master/img/retro-microcontrolled.png?raw=true)

- My Winner: **Wilderness Labs Meadow F7**
- Highlighted: **SparkFun MicroMods**

Wilderness Labs has been doing a very interesting job with Meadow F7. It runs a Mono Framework port that makes it possible to run .NET Standard on microcontrollers, so I can reuse libraries written in C# that follow this standard, use NuGet packages and so on. The Meadow Foundation has an great and easy API for hardware access in a `dotnet` style and also already has implementations for some of most popular devices and modules used in the maker world. But it is good to note that it is still in beta, the network stack for WiFi use is still in development, it works, but is not optimized. But anyway running .NET on a board with only 32MB RAM and @216MHz is still very impressive. It will be a great option for use the .NET and C# skills on IoT projects.

The highlight goes to SparkFun MicroMods. Soon there will be a review of it here. The idea of a MoM (Microcontroller on Module) is very good, it's not new, but using an M.2 connector for this is very interesting. Another interesting thing is that the SparkFun MicroMods pin pattern is open, so the hope is that this pattern will become popular and become an industry standard. So I hope we will have several MoMs out there that are pin compatible with multiple base boards.

### Microprocessed Board

![top microprocessed boards](https://github.com/microhobby/blog/blob/master/img/retro-microprocessed.png?raw=true)

- My Winner: **Apalis iMX8QM**
- Highlighted: **Raspberry Pi 4**

I didn't make this list last year, but surely the microprocessor board winner would also be the Apalis iMX8QM. The board is just an ignorance, two GPUs, heterogeneous processing, 6 ARM cores, 2x A72 and 4x A53, 4 ARM M4F cores and more. RUNS EVERYTHING! The Toradex software support is also very good, there is a Linux distro for the Toradex hardware the Torizon to run containerized applications. But I am suspicious to say since I work at Toradex ... 🤐

The highlight goes to the Raspberry Pi 4. As every Raspberry Pi Foundation launch it is already very popular. Raspberry boards are the best choice for those who want to start in the world of Embedded Linux, and the new generation of boards has a very powerful hardware.

### Framework UI

![top GUI framework 2020](https://github.com/microhobby/blog/blob/master/img/retro-gui.png?raw=true)

- My Winner: **UNO Platform**
- Highlighted: **Total Cross**

This year I also tested and worked with several GUI frameworks, focused on Embedded Linux. UNO Platform itself is not new, but support for Linux was announced this last year. And even if it was announced as a preview it was had already a very good support. Being able to use XAML and C# to work with the Embedded Linux GUI is AMAZING. Use the framework is very easy, runs with X11 or Wayland and it is not necessary to compile anything else to run in the `armv7` or `armv8` architectures, everything comes in the NuGet packages, very straightforward.  Also have a amazing community and documentation. I would say that the Uno Platform was one of the main findings of my 2020 year. In love 😍

The highlight goes to Total Cross. I had the opportunity to test and work with the framework this year. First that the framework is developed by Brazilians, then it already earns points 😝 (I'm Brazilian so ...). It has its own virtual machine for a Java subset, generates very small footprint deployment files (great for systems with low memory storage) and also runs well without the need for a GPU. There are still some issues of interoperability with native libraries, but this feedback has already been received by the Total Cross team and they are working on it (there is already something in preview). So keep an eye on Total Cross because it promises.

### Best Tech of 2020

![top tech 2020](https://github.com/microhobby/blog/blob/master/img/retro-toptech.png?raw=true)

- My Winner: **WSL 2**
- Highlighted: **Blazor**

And last but not least, the best technologies in a more general classification that I used this year. My favorite one was Windows Subsystem for Linux 2. Having Linux running together with Windows is beautiful. It is a VM under the hood but as it was structured it makes everything very transparent and the interoperability is very good. Seeing Microsoft support, and great support, contributing to open source communities and using it on Windows is priceless. The possibilities and opportunities are endless.

The highlight goes to the awesome Blazor. In the beginning it ran a Mono Framework `WASM` (Web Assembly) port, and it is really cool to have .NET running right in your browser with `WASM`. The development experience is really interesting, writing C# as if it were JavaScript, especially for those who want to venture into the world of the web and come from Microsoft's desktop technologies. But for some problems you will still run into JavaScript code anyway. Blazor also has the server side option, the experience is the same as `WASM` but the code runs on the server and it exchange the data via signalR with the browser to make the reactive changes in the browser. I came to evaluate this mode for Embedded Linux and had good results. It is a "hype" technology that Microsoft is investing a lot, so, you have to keep an eye on Blazor.

## Final Considerations

That's it folks! Remembering that:

> ⚠️ THIS LIST IS BASED ON MY HUMBLE OPINION 💩! These are not absolute truths and I can change my mind without prior notice! 🤣

2020 we stayed at home and tested/studied/worked hard, it was crazy 🤪

