C Services have been removed from this repo. New repo for C Services and Trimmed WPF Clients https://github.com/EmonHaque/C-Services-WPF-Clients. Previously this repo name was ServicesAndApps.
=====================================================================================================================================================================

1) Logins.db is required for LoginServices in C/C#

2) AppRepo/applist.txt file format:
RentManager, 3.0, C:/Users/Emon/Desktop/AppRepo/RentManager
CDRM, 2.0, C:/Users/Emon/Desktop/AppRepo/CDRM

3) For each app you've to add an entry in applist.txt. First, Application Name, second, Version and third, Location of build outputs. For example, build outputs of WPF RentManager app will go in C:/Users/<Your Name>/Desktop/AppRepo/RentManager directory. These are required in LaunchService in C/C#.

4) To get served by these services, Yove to put all your apps in a directory, for example C:/Users/<Your Name>/Desktop/TestApps. In the root of TestApps directory put build outputs of WPF Launcher App and for other apps like RentManager or CDRM create a subdirectory and put build outputs there. When you Launch your app, for example, RentManager.exe from C:/Users/<Your Name>/Desktop/TestApps/RentManager that will go up a directory and launch Launcher.exe in C:/Users/<Your Name>/Desktop/TestApps. Launcher.exe will connect to LaunchService and if version doesn't match LauchService will send all files and Launcher.exe will receive and paste it in relevant App directory and Launch the relevant exe's Login Window. Put your username and password in Login window and hit connect, it will connect to LoginService and add entry in Logins.db. If UserName and Password match the AppWindow will Lauch and relevant ServiceProvider will Serve.

5) In C LaunchService sqlite3.dll hasn't been added. Download that from sqlite web or get it from C RentManagerService. you've to keep that dll together with service.exe where sqlite is used.

6) To build x64 lib of sqlite3 by your own, download the dll and def files from sqlite web, put those in a directory, for examle, C:\SQLite. Launch Visual Studio x64 Native Tools Command prompt and execute:
lib /DEF:"C:\SQLite\sqlite3.def" /OUT:"C:\SQLite\sqlite3.lib"

7) Build your gui-less Services in C, since it's easier for handling bytes, and Client apps in WPF. In your WPF Solution add existing CommonControls and CommonService projects. Add CommonService Reference to CommonControls project and add CommonControls reference to your project. LaunchService and LoginService will work automatically for your project this way. I've added one more project RentManagerCommon/CDRMCommon for my WPF Solutions. Those ..Common are used by both Client Apps and C# Services. For C Services you don't need that ..Common Project in you solution. You can add some extension methods or add all those functionalities in your project to convert objects into bytes and bytes back to objects.
