# The Smart Protocol

Despite the lack of official information from APC, this table has been constructed. It's standard RS-232 serial communications at 2400 bps/8N1.

First of all send "Y" command. You should get SM into response.
Some values can be changed in PROG mode only. Send 1..1 with few seconds delay to switch to PROG mode.

| Character | Meaning                                | Typical results   | Other info                                                                                                                                                                                                                                                                                             |
|-----------|----------------------------------------|-------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Ctrl + A  | Model string                           | SMART-UPS 700     | Spotty support for this query on older models                                                                                                                                                                                                                                                          |
| Ctrl + B  | Model HEX code                         | 0E                | Use + or - in PROG mode to change model. Check HEX codes in separate table.                                                                                                                                                                                                                            |
| Ctrl + P  | Print out EEPROM                       | long output       | Print out EEPROM values. Some parts will be readable                                                                                                                                                                                                                                                   |
| Ctrl + N  | Turn on UPS                            | n/a               | Send twice, with 1.5s delay between chars. Only on 3rd gen SmartUPS and Black Back-UPS Pros                                                                                                                                                                                                            |
| Ctrl + Y  | Clear EEPROM Values                    |                   | !!! Complete cleanup EEPROM. UPS may be unusable and may require to reflash EEPROM. Do not execute this comman until you know what you are doing                                                                                                                                                       |
| Ctrl + Z  | Permitted EEPROM Values                | long string       | Gives the EEPROM permitted values for your model. See EEPROM Values for details.                                                                                                                                                                                                                       |
| A         | Front panel test                       | Light show + "OK" | Also sounds the beeper for 2 seconds                                                                                                                                                                                                                                                                   |
| B         | Battery voltage                        | 27.87             | Varies based on current level of charge. See also Nominal Battery Voltage.                                                                                                                                                                                                                             |
| C         | Internal Temperature                   | 36                | Units are degrees C                                                                                                                                                                                                                                                                                    |
| D         | Runtime calibration                    | !, then $         | Runs until battery is below 25% (35% for Matrix) Updates the 'j' values. Only works at 100% battery charge. Can be aborted with a second "D"                                                                                                                                                           |
| E         | Automatic self test interval           | 336               | Writable variable. Possible values:"336" (14 days)"168" (7 days)"ON " (at power on) note extra space"OFF" (never)                                                                                                                                                                                      |
| F         | Line frequency                         | 60                | Units are Hz. Value varies based on locality, usually 50/60.                                                                                                                                                                                                                                           |
| G         | Cause of last transfer to battery      | O                 | Possible values:R (unacceptable utility voltage rate of change)H (high utility voltage)L (low utility voltage)T (line voltage notch or spike)O (no transfers since turnon)S (transfer due to U command or activation of UPS test from front panel)NA (transfer reason still not available; read again) |
| I         | Measure-UPS Alarm enable               | FF                | not decoded yet                                                                                                                                                                                                                                                                                        |
| J         | Measure-UPS Alarm status               | 0F,00             | not decoded yet                                                                                                                                                                                                                                                                                        |
| K         | Shutdown with grace period (no return) | OK or *           | Send twice with > 1.5s delay between chars. Older units send "*" instead of "OK". Length of grace period is set with Grace Period command. UPS will remain off and NOT power on if utility power is restored.                                                                                          |
| L         | Input line voltage                     | 118.3             | Value varies based on locality. Does not always read 000.0 on line failure.                                                                                                                                                                                                                            |
| M         | Maximum line voltage                   | 118.9             | This is the max voltage since the last time this query was run.                                                                                                                                                                                                                                        |
| N         | Minimum line voltage                   | 118.1             | This is the min voltage since the last time this query was run.                                                                                                                                                                                                                                        |
| O         | Output voltage                         | 118.3             | Also see on battery output voltage.                                                                                                                                                                                                                                                                    |
| P         | Power load %                           | 23.5              | Relative to capacity of the UPS.                                                                                                                                                                                                                                                                       |
| Q         | Status flags                           | 8                 | Bitmapped, see status bits below                                                                                                                                                                                                                                                                       |
| R         | Turn dumb                              | BYE               | Only on 3rd gen SmartUPS, SmartUPS v/s, BackUPS Pro. Must send enter smart mode command to resume comms.                                                                                                                                                                                               |
| S         | Soft shutdown                          | OK                | Command executes after grace period. UPS goes online when power returns. Only works when on battery.                                                                                                                                                                                                   |
| U         | Simulate power failure                 | !, then $         | See Alert messages section for info on ! and $.                                                                                                                                                                                                                                                        |
| V         | Old firmware revision                  | "GWD" or "IWI"    | See Interpretation of the Old Firmware Revision                                                                                                                                                                                                                                                        |
| W         | Self test                              | OK                | Tests battery, like pushing button on the front panel. Results stored in "X"                                                                                                                                                                                                                           |
| X         | Self test results                      | OK                | Possible values:OK = good batteryBT = failed due to insufficient capacityNG = failed due to overloadNO = no results available (no test performed in last 5 minutes)                                                                                                                                    |
| Y         | Enter smart mode                       | SM                | This must be sent before any other commands will work. See also turn dumb command to exit smart mode.                                                                                                                                                                                                  |
| Z         | Shutdown immediately                   | n/a               | Send twice with > 1.5s delay between chars. UPS switches load off immediately (no grace period)                                                                                                                                                                                                        |
| a         | Protocol info                          | long string       | Returns three main sections delimited by periods:Protocol versionAlert messages (aka async notifiers)Valid commands                                                                                                                                                                                    |
| b         | Firmware revision                      | 50.9.D            | See Interpretation of the New Firmware Revision.Decoding the example:50 = SKU (variable length)9 = firmware revisionD = country code (D=USA, I=International, A=Asia, J=Japan, M=Canada)                                                                                                               |
| c         | UPS local id                           | UPS_IDEN          | Writable variable. Up to 8 letter identifier for keeping track of your hardware.                                                                                                                                                                                                                       |
| e         | Return threshold                       | 0                 | Writable variable. Minimum battery charge % before UPS will return online after a soft shutdown. Possible values:00 = 00% (UPS turns on immediately)01 = 15%02 = 25%03 = 90%                                                                                                                           |
| f         | Battery level %                        | 99                | Percentage of battery charge remaining                                                                                                                                                                                                                                                                 |
| g         | Nominal battery voltage                | 24                | The battery voltage that's expected to be present in the UPS normally. This is a constant based on the type, number, and wiring of batteries in the UPS. Typically "012", "024" or "048".                                                                                                              |
| h         | Measure-UPS ambient humidity (%)       | 42.4              | Percentage. Only works on models with Measure-UPS SmartSlot card.                                                                                                                                                                                                                                      |
| i         | Measure-UPS dry contacts               | 0                 | Bitmapped hex variable. Mapping:10 = contact 120 = contact 240 = contact 380 = contact 4                                                                                                                                                                                                               |
| j         | Estimated runtime                      | 0327:             | Value is in minutes. Terminated with a colon.                                                                                                                                                                                                                                                          |
| k         | Alarm delay                            | 0                 | Writable variable. Controls behavior of UPS beeper. Possible values:0 = 5 second delay after power failT = 30 second delayL = alarm at low battery onlyN = no alarm                                                                                                                                    |
| l         | Low transfer voltage                   | 103               | Writable variable. UPS goes on battery when voltage drops below this point.                                                                                                                                                                                                                            |
| m         | Manufacture date                       | 11/29/96          | Format may vary by country (MM/DD/YY vs DD/MM/YY). Unique within groups of UPSes (production runs)                                                                                                                                                                                                     |
| n         | Serial number                          | WS9643050926      | Unique for each UPS                                                                                                                                                                                                                                                                                    |
| o         | Nominal Output Voltage                 | 115               | Expected output voltage when running on batteries. May be a writable variable on 220/230/240 VAC units.                                                                                                                                                                                                |
| p         | Shutdown grace delay                   | 20                | Seconds. Writable variable. Sets the delay before soft shutdown completes. (020/180/300/600)                                                                                                                                                                                                           |
| q         | Low battery warning                    | 2                 | Minutes. Writable variable. The UPS will report a low battery condition this many minutes before it runs out of power                                                                                                                                                                                  |
| r         | Wakeup delay                           | 0                 | Seconds. Writable variable. The UPS will wait this many seconds after reaching the minimum charge before returning online. (000/060/180/300)                                                                                                                                                           |
| s         | Sensitivity                            | H                 | Writable variable. Possible values:H = highestM = mediumL = lowestA = autoadjust (Matrix only)                                                                                                                                                                                                         |
| t         | Measure-UPS ambient temperature        | 80.5              | Degrees C. Only works on models with the Measure-UPS SmartSlot card.                                                                                                                                                                                                                                   |
| u         | Upper transfer voltage                 | 132               | Writable variable. UPS goes on battery when voltage rises above this point.                                                                                                                                                                                                                            |
| v         | Measure-UPS firmware                   | 4Kx               | Firmware information for Measure-UPS board                                                                                                                                                                                                                                                             |
| x         | Last battery change date               | 11/29/96          | Writable variable. Holds whatever the user set in it. Eight characters.                                                                                                                                                                                                                                |
| y         | Copyright notice                       | (C) APCC          | Only works if firmware letter is later than O                                                                                                                                                                                                                                                          |
| z         | Reset to factory settings              | CLEAR             | Resets most variables to initial factory values except identity or battery change date. Not available on SmartUPS v/s or BackUPS Pro.                                                                                                                                                                  |
| +         | Capability cycle (forward)             | various           | Cycle forward through possible capability values. UPS sends afterward to confirm change to EEPROM.                                                                                                                                                                                                     |
| -         | Capability cycle (backward)            | various           | Cycle backward through possible capability values. UPS sends afterward to confirm change to EEPROM.                                                                                                                                                                                                    |
| @nnn      | Shutdown and return                    | OK or *           | UPS shuts down after grace period with delayed wakeup after nnn tenths of an hour plus any wakeup delay time. Older models send "*" instead of "OK".                                                                                                                                                   |
| 0x7f      | Abort shutdown                         | OK                | Use to abort @, S, K                                                                                                                                                                                                                                                                                   |
| ~         | Register #1                            | see below         | See Register 1 table                                                                                                                                                                                                                                                                                   |
|           | Register #2                            | see below         | See Register 2 table                                                                                                                                                                                                                                                                                   |
| 0         | Battery constant                       |                   | See Resetting the UPS Battery Constant                                                                                                                                                                                                                                                                 |
| 1..1      | Enter to PROG mode                     | PROG              | Press 1 and another 1 after 2-3 seconds delay. Some constants can be changed in PROG mode only.                                                                                                                                                                                                        |
| 4         | Constant 4                             |                   | Prints 35 on SmartUPS 1000                                                                                                                                                                                                                                                                             |
| 5         | Constant 5                             |                   | Prints EF on SmartUPS 1000                                                                                                                                                                                                                                                                             |
| 6         | Constant 6                             |                   | Prints F9 on SmartUPS 1000                                                                                                                                                                                                                                                                             |
| 7         | DIP switch positions                   |                   | See Dip switch info                                                                                                                                                                                                                                                                                    |
| 8         | Register #3                            | see below         | See Register 3 table                                                                                                                                                                                                                                                                                   |
| 9         | Line quality                           | FF                | Possible values:00 = unacceptableFF = acceptable                                                                                                                                                                                                                                                       |
| >         | Number of external battery packs       |                   | SmartCell models return number of connected packs. Other models return value set by the user (use +/-). If you model has 2*17Ah batteries but you connect more Ah add battery pack for each 34Ah connected to UPS.                                                                                     |
| [         | Measure-UPS Upper temp limit           | NO,NO             | Degrees C. Writable Variable. Possible values: 55, 50, 45, ..., 05. Use +/- to change values.                                                                                                                                                                                                          |
| ]         | Measure-UPS lower temp limit           | NO,NO             | Degrees C. Writable Variable. Possible values: 55, 50, 45, ..., 05. Use +/- to change values.                                                                                                                                                                                                          |
| {         | Measure-UPS Upper humidity limit       | NO,NO             | Percentage. Writable Variable. Possible values: 90, 80, 70, ..., 10. Use +/- to change values.                                                                                                                                                                                                         |
| }         | Measure-UPS lower humidity limit       | NO,NO             | Percentage. Writable Variable. Possible values: 90, 80, 70, ..., 10. Use +/- to change values.                                                                                                                                                                                                         |