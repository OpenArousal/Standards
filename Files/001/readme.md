# TC++ (0.001)

T-Code, maintained and developed by [Tempest for the OSR-2, SR-6 as described here](https://stpihkal.docs.buttplug.io/docs/stpihkal/protocols/tcode/) link to their [Patreon](https://www.patreon.com/tempestvr) to show support.


The needs of [OSSM](https://OSSM.tech) are slightly different in that it is a single axis machine that can use mutiple parameters. To this end we are describing a few additional features that will help make the OSSM more useful. 


## List of Commands and Proposed Extended Commands

### Notes on values

All values given are between 0 and .9999 [Minimum digits for a value are 1, maximum of 10]. When providing the value we do not need to transmit the leading "0." and transmit only the digits following the decimal point. 


## Live Control
``` L[Channel][Value] ```

**[Channel]** is a value from 0 to 9

| Channel | Description (OSSM Specific) |
|---------|-------------|
|0| Toy Rail |
|1| Pin  IO2 |
|2| Pin IO15 |
|3| Pin IO33 |
|4| Pin IO22 |
|5 - 9| User Custom Axis |


**[Value]** is bewteen 0 and .9999

**Toy Rail**

``` 0 ``` is the toy fully retracted towards the body of the OSSM

``` .9999 ``` is the toy at full extension

**IO PINS**

0 to .9999 is PWM from 0 to 100% on the selected pin if configured for analog outputs

Anything above .1 is ON for the selected pin if configured for digital outputs

**Example**

``` L050 ``` "Move to half of stroke (50%)"

*Note*

Moves are made as fast as possible by the machine, this is based on the acceleration and speed limit configured in OSSM. Values are updated as soon as the command is sent. 



## Magnitude + Speed

Append the Live control with ``` S[Speed] ``` 

**[Speed]** 0-32767

Speed is expressed in milliseconds (**NOTE** this is a proposed change from t-code, and will need to be discussed)

*Example* 

```L050S100``` -> Half extension over 100 milliseconds


## Device Commands

 - ```D0``` Will return device & firmware version - "OSSM [Firmware]"
 - - *ex* ``` OSSM 0.24 ```
 - ```D1``` Will return tcode Version - "TC++ [Version]"
 - - *ex* ``` TC++ 0.001```
 -  ```D2``` Will return a list of axis available and their labels
 -  ```D3``` (OSSM Specific) Will return a list of Parameters [detailed below]
 -  ```DSTOP``` Stops device (Motor freze, does not release motor)








