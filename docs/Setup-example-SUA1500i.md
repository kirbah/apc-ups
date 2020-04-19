# SUA1500i specific commands to setup.

Once connect to UPS via serial 2400 bps/8N1 execute below commands to perform complete setup of UPS. It is better to perform entire setup on battery only WITHOUT input and output lines connected.

To verify configured value in many cases it is helpful to sent same command again to see actually configured values. + and - are used to change values in most cases. "+..." means multiple "+" characters should be send to change value. Other options provided in setup command.

Commands L and B most likely require hardware specific configuration. Different hardwares most likely will need different constants.

| Command  | Setup command | Result value | Description                                                                                                                                                 |
|----------|---------------|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Y        |               | SM           | Enter into SMART mode                                                                                                                                       |
| 1..1     |               | PROG         | Switch to PROG mode                                                                                                                                         |
| Ctrl + b | +...          | 0E           | Set HEX code for SUA1500I model                                                                                                                             |
| Ctrl + A |               | SUA1500I     | Verify configured model                                                                                                                                     |
| 4        | +...          | 09           | Set register 4                                                                                                                                              |
| 5        | -...          | B9           | Set register 5                                                                                                                                              |
| 6        | +...          | 13           | Set register 6                                                                                                                                              |
| 0        | -...          | A1           | Set register 0                                                                                                                                              |
| b        | +601          | OK           | Set firmware version to 601                                                                                                                                 |
| b        |               | 601.3.I      | Check full firmware version                                                                                                                                 |
| L        | -...          | D3           | Set input line voltage                                                                                                                                      |
| B        | -...          | EA           | Battery charger voltage controlled with multimeter during charging. Increase constant if battery charging voltage is more than 27.7. 27.4v is avarage value |
| x        | +04/14/20     |              | Last battery change date                                                                                                                                    |
| m        | +08/20/02     |              | UPS manufacture date                                                                                                                                        |
| n        | +AS0234212047 |              | UPS serial number. Add spaces at the end                                                                                                                    |
| >        | +...          | 0            | Number of external battery packs                                                                                                                            |
| c        | +SUA1500i     |              | UPS local id                                                                                                                                                |
| o        | +...          | 00           | Nominal Output Voltage. 230v                                                                                                                                |
| u        | +...          | 00           | Upper transfer voltage. 253v                                                                                                                                |
| l        | +...          | 00           | Low transfer voltage. 208v                                                                                                                                  |
| e        | +...          | 01           | Minimum battery charge % before UPS will return online after a soft shutdown. 01=15%                                                                        |
| k        | +...          | 0            | Alarm delay. Controls behavior of UPS beeper. Possible values:0 = 5 second delay after power fail                                                           |
| E        | +...          | 00           | Automatic self test interval. 00 = 14 days                                                                                                                  |
| p        | +...          | 01           | Shutdown grace delay in seconds. 01 = 180 sec                                                                                                               |
| q        | +...          | 02           | Low battery warning. 02 = 8 minutes                                                                                                                         |
| r        | +...          | 01           | Wakeup delay. 01 = 60 seconds                                                                                                                               |
| s        | +...          | 02           | Sensitivity. 02 = lowest                                                                                                                                    |
| R        |               | BYE          | Exit from PROG mode                                                                                                                                         |
