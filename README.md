# Seeed_Arduino_Grove_DopplerRadar

This library Grove DopplerRadar.

### Software usage  

-Install Seeed Arduino Grove DopplerRadar library to Arduino.  

-Start a project.  

-You can choose to use the hardware or software serial port.
  ```
      #ifdef __AVR__
      #include <SoftwareSerial.h>
      SoftwareSerial SSerial(2, 3); // RX, TX
      #define COMSerial SSerial
      #define ShowSerial Serial

      GBT24LTR11<SoftwareSerial> GBT;
      #endif

      #ifdef ARDUINO_SAMD_VARIANT_COMPLIANCE
      #define COMSerial Serial
      #define ShowSerial SerialUSB

      GBT24LTR11<Uart> GBT;
      #endif

      #ifdef ARDUINO_ARCH_STM32F4
      #define COMSerial Serial
      #define ShowSerial SerialUSB

      GBT24LTR11<HardwareSerial> GBT;
      #endif

  ```

-Set the communication baud rate of the DopplerRadar module (115200).

-Then initialize GBT in the setup function.

-Set the working mode.
  ```
  void setup()
  {
    // put your setup code here, to run once:
    ShowSerial.begin(9600);
    COMSerial.begin(115200);
    GBT.init(COMSerial);
    while (!ShowSerial)
      ;
    while (!COMSerial)
      ;
    /*
     * MODE 0 -->detection target mode
     * MODE 1 -->I/Q ADC mode
     * 
     */
    while (!GBT.setMode(0))
      ;
  }
  
  ```
  
-You can use the getSpeed() function and the getTargetState() function to get the speed and target state.

-You can set I/Q ADC mode using the setMode (1) function.This pattern retrieves I/Q information.


