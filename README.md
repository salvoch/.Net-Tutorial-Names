# Names


## Tutorial
A super simple first tutorial for working with .net and WPF. See tutorial here:

https://docs.microsoft.com/en-us/dotnet/desktop/wpf/get-started/create-app-visual-studio?view=netdesktop-6.0

## Deploying project:

Documentation: https://docs.microsoft.com/en-us/dotnet/core/rid-catalog

To deploy an .exe
There is a GUI way of doing this under the "Build" section of VS. However, there are some issues with this.

You have more flexibility using the command line. Right click the project in the "Solution Explorer" section and select "Open in terminal".

In the terminal you can deploy a project like this:

```Powershell
dotnet publish -c Release
```

By default, this deployment requires that the final user has .net installed on their computer!
This is good because the project is tiny, however, it's bad since it won't run with every computer.

To deploy this as a self-contained application do it like this:

Note, we have to specify a RunTimeIdentifier, with the `-r` identifier, which describes what platform our application will run on. You can select OSX, Windows, etc.

*NOTE*: WPF is not cross platform, so you have to choose a windows platform. Some options:

* win-x64
* win-x86
* win-arm
* win-arm64
* win10-x64
* win10-x86
* win10-arm
* win10-arm64

```Powershell
dotnet publish -c Release --self-contained -r win-x64
```

The problem here is that there a huge amount of files. This can be annoying for the users. The best way to do this is to specify 
single file mode, like this!

```Powershell
dotnet publish -c Release --self-contained -r win-x64 -p:PublishSingleFile=true
```

You will see the executable in the `...\win-x64\publish` directory.

However! In newer versions there are still some straggling .dlls. What you can do is this:

```Powershell
dotnet publish -c Release --self-contained -r win-x64 -p:PublishSingleFile=true -p:IncludeNativeLibrariesForSelfExtract=true
```

There is also a .pbd file there that is not needed. But this should work!