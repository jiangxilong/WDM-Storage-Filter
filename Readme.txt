  The license model is a BSD Open Source License. This is a non-viral license, only asking that if you use it, you acknowledge the authors, in this case Slava Imameev.
  
  This is a WDM driver filter that I found on the old hard drive. I developed it in 2008 in one day to test some ideas. The interesting feature of the driver is using an asynchronous multithreaded processing to speed up filtering. There is no PnP processing in this driver as its goal was to test asynchronous processing in multiple threads.
  
  The PctDriver folder contains code for the driver.
  The Test folder contains a test application code.
  
  I believe the solution was made in VS 2005, I do not remember the exact VS version I used for the project.
  The driver should be built by using WDK build environment (e.g. "build -cgwF" command ), the driver has been tested on 32 bit Windows Server 2003.
  The test application can be build from VS environment.
  
  The driver is intended to communicate with the FDO created by the disk class driver( i.e. disk.sys ).
  
  The driver uses the name space extending - the name sent to CreateFile is a concatenation of the driver's communication object and the name of the disk to be opened, e.g. CreateFile( L"\\\\.\\PctCommunicationObject\\Device\\Harddisk0\\DR0", ..... ); The returned handle is used for issuing read and write requests through DeviceIoControl, the number of the simultaneously opened handles is unrestricted ( the upper limit is defined by the OS kernel ).
  
  The driver supports asynchronous IO if the FILE_FLAG_OVERLAPPED flag is defined and DeviceIoControl parameters don't convert operation to a synchronous one.
