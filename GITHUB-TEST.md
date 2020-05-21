In this article, we will show how you can use serial UART GPS using .NET Core and [Visual Studio Code Extension for Torizon](https://developer.toradex.com/knowledge-base/visual-studio-code-development-extension-pythonnet-core).

The goal is to show an application using [ASP.NET Core Blazor Server](https://docs.microsoft.com/aspnet/core/blazor/get-started?view=aspnetcore-3.1&tabs=visual-studio-code) template, showing the data returned from a serial UART GPS on a Google Maps visualization.

![Blazor Application on Local Kiosk UI](https://docs.toradex.com/107682-img_20200519_235158039.jpg?w=500)

# Prerequisites #

- [TorizonCore](https://developer.toradex.com/software/torizon) installed on a Toradex module.
- Have completed the [.NET Core Development and Debug on TorizonCore Using Visual Studio Code](https://developer.toradex.com/knowledge-base/net-core-development-and-debug-on-torizoncore-using-visual-studio-code) lessons.
- Have completed the [.NET Core - Using Serial UART GPS](https://developer.toradex.com/knowledge-base/net-core-using-serial-uart-gps)
- [Google Maps Platform API Key](https://developers.google.com/maps/documentation/javascript/get-api-key)
- (optional) HDMI Display or [Capacitive Touch Display 7" Parallel Touch Display](https://www.toradex.com/pt-br/accessories/capacitive-touch-display-7-inch-parallel) for Local UI

# Application Architecture #

In this example we will show a way to use ASP.NET Core Blazor application as a Local and Remote user interface solution. For that we will use a multi-container architecture:

- **Weston Container**:
	- Wayland compositor;

- **Kiosk Browser Container**:
	- Chromium browser for the local UI, that will open, in full screen kiosk mode, the ASP.NET Core Blazor application. Chromium is a graphic application that depends on Weston to run;

- **Application Container**
	- ASP.NET Core Blazor application that will manage the serial UART GPS connection and UI design;

![ASP.NET Core Blazor GPS Application architecture](https://docs.toradex.com/107678-blazordiagramcomplete.png?w=550)

With this multi-container architecture running we can access the application ASP.NET Core Blazor page, either remotely through the board IP address, on a computer or device connected to the same network, or interact with the application on a display connected to the board, that will show the Kiosk browser running.

# Connect to a Serial GPS #

For the example in this article we will follow the same steps for connecting the GPS from the section [Connect to a Serial GPS](https://developer.toradex.com/knowledge-base/net-core-using-serial-uart-gps#Connect_to_a_Serial_GPS) from [.NET Core - Using Serial UART GPS](https://developer.toradex.com/knowledge-base/net-core-using-serial-uart-gps) article.

# Instructions #

In this article we will focus on the creation of
ASP.NET Core Blazor application using Torizon Visual Studio Code extension.

## Create a New ASP.NET Core Project ##

On VS Code press `F1` and: 

- Select the command `Torizon/.NET: Create ASP.NET Application`
- Type the application name `blazorGoogleMaps`
- Select a folder to store the project files
- On the project templates list select `ASP.NET Blazor Application`
- Select the architecture `arm32` or `arm64` for the target Toradex Board
- Confirm, pressing enter, the default `torizon` user

![Create an ASP.NET Core Blazor Project](https://docs.toradex.com/107668-8jtu6vighp.gif)

## Add UART Device to the Project ##

To add an UART device to your ASP.NET Core Blazor Torizon project, first, open the Torizon Configuration View. To do that, press F1 in Visual Studio Code command bar and then type "Torizon: Focus on Configurations View"

![Show the Configurations View](https://docs.toradex.com/107389-103486-vscode-cmd-bar-configuration.jpeg)

On the device item, press the '+' button on the right.

![Add New Device to The Project](https://docs.toradex.com/107574-vscodeadddevice.png?w=500)

Type the selected tty device. As an example, we will add `/dev/apalis-tty4`.

⚠️ **WARNING: `/dev/apalis-tty4` is UART4 in the case of the Apalis family. See more information in the article [How to Use UART on TorizonCore](https://developer.toradex.com/knowledge-base/uart-torizoncore)** ⚠️

![Adding tty device](https://docs.toradex.com/107575-vscodeadddevtty.png?w=500)

Check if the device was added to your project.

![Project's Devices](https://docs.toradex.com/107576-vscodedevttyadded.png?w=500)

## Add Serial Access Permission ##

To have access to the serial devices we need to add the default `torizon` user to `dialout` group. Go to the Torizon Visual Studio Code Extension Configurations and add the `buildcommands`:

```
RUN usermod -a -G dialout torizon 
```

![Add torizon user to dialout group](https://docs.toradex.com/107655-6mo2wp0rmu.gif)

## Add Nuget Packages ##

To easily parse NMEA data from GPS module, we use the `SharpGIS.NmeaParser` library. To add it to the project open a new terminal using the Visual Studio Code and enter the following command:

```
dotnet add package SharpGIS.NmeaParser
```

![Adding NUGET Package](https://docs.toradex.com/107578-prg2proqkb.gif)

## Source Code ##

The example code used in this documentation comes from the sample [https://github.com/toradex/torizon-samples/gps/dotnet/blazor/](https://github.com/toradex/torizon-samples/gps/dotnet/blazor)

You can copy the contents of the files and folders, listed below, to your project created on the sections above, choosing the overwrite option. Or just open the `samples/gps/dotnet/blazor` folder in VS Code to use with Torizon Visual Studio Code Extension:

- [/Models](https://github.com/toradex/torizon-samples/gps/dotnet/blazor/Models)
- [/Pages](https://github.com/toradex/torizon-samples/gps/dotnet/blazor/Pages)
- [/Services](https://github.com/toradex/torizon-samples/gps/dotnet/blazor/Services)
- [/Shared](https://github.com/toradex/torizon-samples/gps/dotnet/blazor/Shared)
- [/wwwroot](https://github.com/toradex/torizon-samples/gps/dotnet/blazor/wwwroot)
- [_Imports.razor](https://github.com/toradex/torizon-samples/gps/dotnet/blazor/_Imports.razor)
- [App.razor](https://github.com/toradex/torizon-samples/gps/dotnet/blazor/App.razor)
- [Program.cs](https://github.com/toradex/torizon-samples/gps/dotnet/blazor/Program.cs)
- [Startup.cs](https://github.com/toradex/torizon-samples/gps/dotnet/blazor/Startup.cs)
- [/appconfig_0/docker-compose.arm32v7.yml](https://github.com/toradex/torizon-samples/gps/dotnet/blazor/appconfig_0/docker-compose.arm32v7.yml)
- [/appconfig_0/docker-compose.arm64v8.yml](https://github.com/toradex/torizon-samples/gps/dotnet/blazor/appconfig_0/docker-compose.arm64v8.yml)

### Google Maps Configuration ###

To use Google Maps you will need a Google Maps Platform API Key, follow the developers Google documentation to get an API Key: [https://developers.google.com/maps/documentation/javascript/get-api-key](https://developers.google.com/maps/documentation/javascript/get-api-key)

With a Google Maps Platform API Key created edit the file [Pages/_Host.cshtml](https://github.com/toradex/torizon-samples/gps/dotnet/blazor/Pages/_Host.cshtml#L35) on the line `35`:

```html
    <script src="https://maps.googleapis.com/maps/api/js?key=NULL&v=3"></script>
```

Modifying the `key=NULL` property by `key=<your API key>`


### Set `SerialPortDevice.PortName` ###

Modify the serial device path according to the serial device you are using. Edit the file [Services/GPS.cs](https://github.com/toradex/torizon-samples/gps/dotnet/blazor/Services/GPS.cs#L19) on the line `19`:

```csharp
            serialDev.PortName = "/dev/apalis-tty4";
```

```dockerfile
FROM ubuntu

RUN apt-get install minharola

CMD [ "rola" ]

```

With the correct device set we can now run and debug the application. 

## Run Application Debug  ##

### Remote UI ###

On VS Code press F5 to run the Debug. See the [.NET Core Development and Debug on TorizonCore Using Visual Studio Code](https://developer.toradex.com/knowledge-base/net-core-development-and-debug-on-torizoncore-using-visual-studio-code) article for detailed instructions about debug tools.

You can access the running ASP.NET Core Blazor page application remotly through the IP address of the board on the port `5000` in a browser. 

### Local UI ###

#### Set docker-compose File ####

To configure the application for show the local UI, on the display connected to the board, we still have to configure a `docker-compose.yml` file that will have the dependency containers and  settings to run our [multi-container application](#Application-Architecture). 

On the sample folder [appconfig_0](https://github.com/toradex/torizon-samples/gps/dotnet/blazor/appconfig_0) we have two docker-compose files:

- [docker-compose.arm64.yml](https://github.com/toradex/torizon-samples/gps/dotnet/blazor/appconfig_0/docker-compose.arm64.yml) for ARMv8 64bits Toradex Modules
- [docker-compose.arm32.yml](https://github.com/toradex/torizon-samples/gps/dotnet/blazor/appconfig_0/docker-compose.arm32.yml) for ARMv7 32bits Toradex Modules

Usin the Torizon Configurations on VS Code edit the property `dockercomposefile` with the name of the file that correspond to the architecture of your board:

![Add the reference to the docker-compose file](https://docs.toradex.com/107680-ix7pubp259.gif)

Press F5 to run the application debug. This will run the docker-compose multi-container application.

You can also set break-points in the code and interact with the application on the local or remote UI to debug.

![,](https://docs.toradex.com/107681-blazor-remote-debug-torizon.gif)

See the [.NET Core Development and Debug on TorizonCore Using Visual Studio Code](https://developer.toradex.com/knowledge-base/net-core-development-and-debug-on-torizoncore-using-visual-studio-code) article for detailed instructions about debug tools.
