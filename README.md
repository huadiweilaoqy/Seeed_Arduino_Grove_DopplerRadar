# Seeed_Arduino_Grove_DopplerRadar

This library Grove DopplerRadar.

## Hardware requirements

- Arduino Zero
- Grove Shield and a cable
- Grove DopplerRadar(BGT24LTR11)
<img src=img/DopplerRadar.jpg width=300 height=200> 

#### connection of the hardware
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <img src=img/connect.jpg width=300 height=200> 
Connect DopplerRadar to the serial port of the board.In this example, we use hardware serial as the serial port; If you have other software Serial ports on you board, you can also connect to it.But software serial port may cause data loss.

###  Usage

- Git clone this resp to your Arduino IDE'S libraries directory.

- Run the demo "BGT24LTR11_DETECTION_TARGET" on examples directory.

- Start a project.  

- You can choose to use the hardware or software serial port.
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

- Set the communication baud rate of the DopplerRadar module (115200).

- Then initialize GBT in the setup function.

- Set the working mode.
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
     */
    while (!GBT.setMode(0))
      ;
  }
  
  ```
###Methods

- uint16_t getSpeed();

- uint16_t getTargetState();

- uint8_t getIQADC(uint16_t I_d[],uint16_t Q_d[],uint16_t *len);

- uint8_t setSpeedScope(uint16_t maxspeed,uint16_t minspeed);

- uint8_t getSpeedScope(uint16_t *maxspeed,uint16_t *minspeed);

- uint8_t setMode(uint16_t mode);
	- mode 0 :detect the target mode.
	- mode 1 :Gets the I/Q information ADC value mode.

	
- uint8_t getMode();

- uint8_t setThreshold(uint16_t whreshold);

- uint16_t getThreshold();


