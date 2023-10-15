# Arduino DCF77 library
[![Build Status](https://travis-ci.org/thijse/Arduino-DCF77.svg?branch=master)](https://travis-ci.org/thijse/Arduino-DCF77)
[![License: LGPL v21](https://img.shields.io/badge/License-LGPL%20v2.1-blue.svg)](https://img.shields.io/badge/License-LGPL%20v2.1-blue.svg)

The DCF77 library adds the ability to read and decode the atomic time broadcasted by the 
DCF77 radiostation. It has been designed to work in conjunction with the Arduino Time 
library and allows a sketch to get the precise CET time and date as a standard C time_t.
The DCF77 Library download. Example sketches have been added to

1. illustrate and debug the incoming signal 
2. use the library, using the setSyncProvider callback and converting to different 
   time zones. In order to exploit all features in the library, Both the Time and 
   TimeZone library are included.

Additional documentation and full explanations of the samples can be found in these blog 
posts on DCF Hardware, DCF Signal can be found here:
[http://thijs.elenbaas.net/2012/04/arduino-dcf77-radio-clock-receiver-library/](http://thijs.elenbaas.net/2012/04/arduino-dcf77-radio-clock-receiver-library/)


## Downloading

This package can be downloaded in different manners 


- The Arduino Library Manager: [see here how to use it](http://www.arduino.cc/en/guide/libraries#toc3).
- The PlatformIO Library Manager: [see here how to use it](http://docs.platformio.org/en/latest/ide/arduino.html).
- By directly loading fetching the Archive from GitHub: 
 1. Go to [https://github.com/thijse/Arduino-DCF77](https://github.com/thijse/Arduino-DCF77)
 2. Click the DOWNLOAD ZIP button in the panel on the
 3. Rename the uncompressed folder **Arduino-DCF77-master** to **DCF77**.
 4. You may need to create the libraries subfolder if its your first library.  
 5. Place the **DCF77** library folder in your **arduinosketchfolder/libraries/** folder. 
 5. Restart the IDE.
 6. For more information, [read this extended manual](http://thijs.elenbaas.net/2012/07/installing-an-arduino-library/)
- If you want to have a package that includes all referenced libraries, use the pre-packaged library
 1. Download the package as a zipfile [here](https://github.com/thijse/Zipballs/blob/master/DCF77/DCF77.zip?raw=true) or as a tarball [here ](https://github.com/thijse/Zipballs/blob/master/DCF77/DCF77.tar.gz?raw=true).
 2. Copy the folders inside the **libraries** folder  to you your **arduinosketchfolder/libraries/** folder.
 3. Restart the IDE.
 3. For more information, [read this extended manual](http://thijs.elenbaas.net/2012/07/installing-an-arduino-library/)

##Samples
 
The DCF77 directory contains some examples:

### DCFSignal.pde

  This is the most basic example: it shows the raw signal coming from the 
  DCF decoder. It will show Pulse-to-Pulse times of approximately 1000 ms and 
  pulse widths of approx 100ms and 200ms.

### DCFPulseLength

  This example illustrates the pulse-to-pulse time and pulse lengths 
  coming from the DCF decoder. While the DCF specification says that pulses 
  should be either 100 or 200 ms, you will probably see longer pulse lengths. 
  For optimal distinction between long and short pulses use the output of this 
  sketch to set the parameter #define DCFSplitTime in DCF77.h to (Tshort+Tlong)/2.

### DCFBinaryStream

  This example shows the binary stream generated by the pulse train coming 
  from the DCF decoder and the resulting CET time.

### InternalClockSync

  This is the probably the most important example: It shows how to fetch a 
  DCF77 time and synchronize the internal Arduino clock. 

### SyncProvider

  This sketch shows how to fetch a DCF77 time and synchronize the internal clock 
  using the setSyncProvider function. Note that the loop code does not require any 
  logic to maintain time sync. The Time library will monitor DC77 and sync the 
  time as necessary. 

### TimeZones

  This example shows how to convert the DCF77 time to a different timezone. It uses 
  the UTC time to ensure that no ambiguities can exist. For timezone conversion it 
  employs the TimeZone library.

### Signal visualisation
 
  The getSignal() functions allow to analyze the DCF77 signal. This helps to get the 
  antenna in right direction e.g. Frankfurt.
  Example: 
  ```
   bool signal = DCF.getSignal(); // Get DCF77 signal for LED     
   if (signal) { digitalWrite(BUILTIN_LED,LOW); } else { digitalWrite(BUILTIN_LED,HIGH); }
  ```
*** Using the Library ***

To use the library, first download the DCF77 library here: 
https://github.com/thijse/Arduino-Libraries/downloads
and install it in the Arduino Library folder. 
For a tutorial on how to install new libraries for use with the Arduino development 
environment please refer to http://www.arduino.cc/en/Reference/Libraries
or follow this step-by-step how-to article on installing Arduino libraries:
http://thijs.elenbaas.net/2012/07/installing-an-arduino-library

If the library is installed at the correct location, you can find the examples discussed 
in this and the previous post under Examples > DCF77. I also added the time library to 
the archive for convenience.

The DCFF77 directory contains the DCFF77 library and some example sketches

- DCFSignal.pde

  This is the most basic example: it shows the raw signal coming from the 
  DCF decoder. It will show Pulse-to-Pulse times of approximately 1000 ms and 
  pulse widths of approx 100ms and 200ms.

- DCFPulseLength.pde

  This example illustrates the pulse-to-pulse time and pulse lengths 
  coming from the DCF decoder. While the DCF specification says that pulses 
  should be either 100 or 200 ms, you will probably see longer pulse lengths. 
  For optimal distinction between long and short pulses use the output of this 
  sketch to set the parameter #define DCFSplitTime in DCF77.h to (Tshort+Tlong)/2.

- DCFBinaryStream.pde

  This example shows the binary stream generated by the pulse train coming 
  from the DCF decoder and the resulting CET time.

- InternalClockSync.pde

  This is the probably the most important example: It shows how to fetch a 
  DCF77 time and synchronize the internal Arduino clock. 

- SyncProvider.pde

  This sketch shows how to fetch a DCF77 time and synchronize the internal clock 
  using the setSyncProvider function. Note that the loop code does not require any 
  logic to maintain time sync. The Time library will monitor DC77 and sync the 
  time as necessary. 

- TimeZones.pde

  This example shows how to convert the DCF77 time to a different timezone. It uses 
  the UTC time to ensure that no ambiguities can exist. For timezone conversion it 
  employs the TimeZone library.


### Example sketch 
The sketch below implements the most DCF77 basic functionality. It reads the signal from 
pin 2, and 2-3 minutes it will update the internal clock. More information on this example 
can be found here: 

[http://thijs.elenbaas.net/2012/04/arduino-dcf77-radio-clock-receiver-library/
](http://thijs.elenbaas.net/2012/04/arduino-dcf77-radio-clock-receiver-library/)
    
    #include "DCF77.h"
    #include "TimeLib.h"
    
    #define DCF_PIN 2// Connection pin to DCF 77 device
    #define DCF_INTERRUPT 0  // Interrupt number associated with pin
    
    time_t time;
    DCF77 DCF = DCF77(DCF_PIN,DCF_INTERRUPT);
    
    void setup() {
      Serial.begin(9600);
      DCF.Start();
      Serial.println("Waiting for DCF77 time ... ");
      Serial.println("It will take at least 2 minutes before a first time update.");
    }
    
    void loop() {
      delay(1000);
      time_t DCFtime = DCF.getTime(); // Check if new DCF77 time is available
      if (DCFtime!=0)
      {
    Serial.println("Time is updated");
    setTime(DCFtime);
      }
      digitalClockDisplay();  
    }
    
    void digitalClockDisplay(){
      // digital clock display of the time
      Serial.print(hour());
      printDigits(minute());
      printDigits(second());
      Serial.print(" ");
      Serial.print(day());
      Serial.print(" ");
      Serial.print(month());
      Serial.print(" ");
      Serial.print(year());
      Serial.println();
    }
    
    void printDigits(int digits){
      // utility function for digital clock display: prints preceding colon and leading 0
      Serial.print(":");
      if(digits < 10)
    Serial.print('0');
      Serial.print(digits);
    }

## On using and modifying libraries

- [http://www.arduino.cc/en/Main/Libraries](http://www.arduino.cc/en/Main/Libraries)
- [http://www.arduino.cc/en/Reference/Libraries](http://www.arduino.cc/en/Reference/Libraries) 

## Copyright

DCF77 is provided Copyright © 2013-2017 under LGPL License.

