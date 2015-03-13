# Debugging with Visual Studio #

To set up debugging in Visual Studio, do the following:

  1. From the menu, select Project | pyactivemq Properties... (Alt+F7)
  1. Configuration Properties | Debugging
  1. Command: `C:\Python24\python.exe`
  1. Command Arguments: `..\..\src\test\alltests.py`
  1. Working Directory: `$(SolutionDir)$(ConfigurationName)`

You might have to set up breaking on exceptions to debug some errors when the module is imported. Do the following:

  1. From the menu, select Debug | Exceptions...
  1. Check all the Thrown checkboxes.