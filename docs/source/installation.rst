Installation
=============

Downloading a Pre-Compiled Version
-----------------------------------

Installing the Barotrauma Mod Generator is quite easy.

#. Go to the `releases page <https://github.com/Jlobblet/Barotrauma-Mod-Generator/releases>`_ and download the latest release.
    
    Make sure you download one of the pre-compiled archives, rather than the source code.

   .. image :: /_images/installation/downloads.png
        :alt: Make sure to download the pre-compiled program.

#. Extract the program into the directory you want to run it.

That's it! From here you can run the executable file from that folder.

Compiling From Source
---------------------

Recommended prerequisites: Visual Studio 2019, .NET Core SDK for .NET Core 3.1, git

#. Download the source code by running ``git clone https://github.com/Jlobblet/Barotrauma-Mod-Generator.git``

    * If you don't have ``git`` you can download the source code as a zip file and extract it yourself.

#. Open the solution (``Barotrauma Mod Generator.sln``) in Visual Studio

#. Change the build configuration to your preferred option.

#. Build the project.

Alternatively, you can build it from the command line using ``dotnet publish "Barotrauma Mod Generator.csproj" -c Release`` 