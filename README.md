# app-deployer
Build and deploy application written in Pharo

## Stateless images
It is a common assertion that application deployed should not write directly to the directory where they are installed. It is even mandatory when you deploy with a user having privileges (root, Admin) and when a standard user. Stateless images are also needed if you want a simple (command-line) Pharo interpreter (like python, ruby, etc.).
Known issues:
- 'pharo-local' folder is not configurable. A lot of tools rely on the hardcoded path (relative to the image): `FileLocator>>#localDirectory`. The same method exists in `SystemResolver`(which seems to be a bad place for that) and is configurable. Probably we should move the `SystemResolver>>#localDirectory` implementation to `FileLocator` and ensure that all tools use it (GT play cache, iceberg cache, monticello cache, github cache, epicea. There are, at least, 2 options to solve that:
  - use a MemoryFileSystem to store the 'pharo-local' folder
  - configure 'pharo-local' folder to be in the standard application data folder. If so, we should take care that data saved in this folder does not have any influence on the behavior of the application.
- Pharo command-line handler tries to create a file to simulate StdOut on Windows. See implementors of `#standardIOStreamNamed:forWrite:`

## Trusted app
On Windows, there is now the [SmartScreen](https://docs.microsoft.com/en-us/windows/threat-protection/windows-defender-smartscreen/windows-defender-smartscreen-overview) system telling the user if an application is trustable or not. We should be able to provide trusted app for Windows.
On OS X, If your app is not certified by Apple, you need to modify your system settings (trust any app) before being able to install the app. We should be able to provide trusted app for OS X.

## Deployment
### Unix
We should be able to provide system package for applications (using [Open Build Service](http://openbuildservice.org/)).
### Windows
We should provide an installer (we already have a [template with NSIS](https://github.com/pharo-project/pharo-build-scripts/tree/master/windows-installer)) able to check if the user has enough permissions to install in the choose folder. Then, we should propose the creation of shorctuts (desktop, OS menu)

## Source of input

The presentation of Maximillo Tabacman at Smalltalk is nice and we should contact him. 
The pdf is in the repo. 