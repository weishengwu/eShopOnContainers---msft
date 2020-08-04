## Windows

### Recommended Hardware requirements for Windows

- 16Gb of memory RAM - Since Hyper-V is needed for Docker Community Edition (a.k.a. Docker Desktop for Windows/Mac) in order to run the Linux Docker Host and and an SQL Server container and Redis container are also running. An 8Gb RAM machine might be too tight.

To run Hyper-V you also need:

- Windows 10 Pro, Education or Enterprise.
- 64-bit Processor with Second Level Address Translation (SLAT).
- CPU support for VM Monitor Mode Extension (VT-c on Intel CPU's).
- Virtualization must enabled in BIOS. Typically, virtualization is enabled by default.
  - This is different from having Hyper-V enabled.

### Software requirements for Windows

- Docker Desktop Community Edition (aka. Docker for Windows) - Requires Windows 10 Pro 64 bits and Hyper-V enabled.
- Latest **.NET Core 3.1 SDK** from: https://www.microsoft.com/net/download
- (Optional) Visual Studio 2017 **15.8** or later (Visual Studio 2019 recommended) – Much better for debugging multi-containers apps
- (Optional) Visual Studio Code.

If your system is OK with the Docker requirements above, you'll be fine for VS too.

### Setting up your development system for Windows

- Begin by installing Docker Desktop for Windows following the instructions in <https://docs.docker.com/docker-for-windows/install/>.

- Continue to the [Windows setup wiki page](Windows-setup).

## Mac

### Recommended Hardware requirements for Mac

- 16Gb of memory RAM - Since you run a VM in the Mac with the Linux Docker host and we're also running a SQL Server container and a Redis container, 8Gb of RAM might not be enough.
- Processor with support for MMU virtualization.

### Software requirements for Mac

- Docker Desktop Community Edition (a.k.a. Docker for Mac) - Requires OS X El Capitan 10.11 or newer macOS.
- Latest **.NET Core 3.1 SDK** from: https://www.microsoft.com/net/download
- (Optional) Visual Studio for Mac.
- (Optional) Visual Studio Code.

### Setting up your development system for Mac

- Begin by installing Docker Desktop for Mac following the instructions in <https://docs.docker.com/docker-for-mac/install/>.

- Continue to the [Mac setup wiki page](Mac-setup).
