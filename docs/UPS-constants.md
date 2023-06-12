# UPS constants

UPS registers 4, 5 and 6 should be set depending on UPS model.

Register 0 is battery constant might be set to FF and will be changed after the calibration to value similar to the table value.

Hex column contains model Hex code. It may be used to change model using Ctrl + B command.

Battery voltage cannot be changed. It is model specific setting.

| UPS Model        | 4  | 5  | 6  | 0  | Hex      | Firmware    | Battery voltage |
|------------------|----|----|----|----|----------|-------------|-----------------|
| SU250            |    | EE | F8 | B1 |          |             |                 |
| SU400            |    | EE | F8 | 9F | E1       |             |                 |
| SU420            | 25 | 95 | 09 |    |          | 21.1.I      | 24v             |
| SU420I           | 25 | 95 | 09 | 85 | 16       | 21.7.I      |                 |
| SU420SI          | 0E | 95 | 0A | 8C |          |             |                 |
| SU450,700        | 28 | F2 | FA | 96 | 07,RM=47 | 52.11.I     | 24v             |
| SU450XL,700XL    | 28 | EE | F8 | 9F | 700XL=27 | 51.9.I      | 24v             |
| SU600            |    | EA | F4 | 9F | E5       |             |                 |
| SU620I           | 29 | 99 | 0B | 8A | 1A       |             |                 |
| SU620 (2001year) | 10 | 97 | 0B | 99 |          | 22.6.I      |                 |
| SU700RMI2U       | 07 | B1 | 0D | 92 | 8A       | 152.4.I     |                 |
| SU900            |    | F3 | FC | 9F | ED       |             |                 |
| SU1000RMI2U      | 08 | B5 | 0D | C7 | 8E       | 157.3.I     |                 |
| SU1250           |    | EE | FA | 9F | F5       |             |                 |
| SU2000           |    | F1 | F9 | 9F | FD       |             |                 |
| SU1000,INET      | 35 | EF | F9 | A0 | 0B       | 60.11.I     |                 |
| SU1000XL         | 17 | EE | F9 | D5 |          |             |                 |
| SU1000XL         | 34 | EE | FC | 9A | 2B       | 61.9.I      |                 |
| SU1400           | 35 | EE | FC | 9A |          | 70.11.I     |                 |
| SU1400RM         | 28 | ED | FA | 89 |          |             |                 |
| SU1400RMI2U      | 08 | B4 | 10 | A3 | 92       | 162.3.I     |                 |
| SU1400R2IBX135   | 08 | B4 | 10 | A3 |          |             |                 |
| SU1400RMXLI3U    | 45 | F6 | F4 | 80 |          | 73.x.I      |                 |
| SU1400RMXLI3U    | 20 | F3 | FD | 81 |          | 73.x.I      |                 |
| SU1400XL,XLI,RM  | 45 | F6 | E4 | 80 |          |             |                 |
| SU2200I          | 35 | EE | FB | AF |          | 90.14.I     | 48v             |
| SU2200XL,3000    | 35 | EE | FB | AF | 3000=17  | 90.14.I     | 48v             |
| SU3000NET        |    |    |    | 96 |          |             | 48v             |
| SU3000RMXLI3Ublk | 35 | F3 | F4 | AF | 77       | 93.14.I     | 48v             |
| SU5000I white    | 20 | F2 | FA | 91 | 1F       | 110.14.I    |                 |
| BP420SI          | 0E | 95 | 0A | 8C | 06       | 11.2.I      |                 |
| BP500AVR         |    |    |    |    | 26       | 17.1.I      |                 |
| BP650SI          | 10 | 97 | 0C | 91 | 0A       | 12.3.I      |                 |
| Power Stack 250  | 0C | 95 | 0F | B2 |          | 26.5.I      |                 |
| Power Stack 450  | 0D | 96 | 10 | 99 | 36       | 26.5.I      |                 |
| SC250RMI1U       | 0C | 95 | 0F | B3 | 32       | 735.a.1     |                 |
| SC420I           | 0E | 95 | OA | 8C | 16       | 725.1.I     |                 |
| SC620I           | 10 | 97 | OB | 99 | 1A       | 726.x.I     |                 |
| SC1000I          | 08 | 95 | 10 | 94 | 8A       | 737.x.I     |                 |
| SC1500I          | 07 | 95 | 14 | 8F | 1E       | 738.x.I     |                 |
| MATRIX 3000,5000 |    | E9 | F5 | B0 |          |             |                 |
| SUA750XLI        | 0A | B9 | 0C | 86 | 46       | 630.3.I     |                 |
| SUA750I          | 04 | B6 | 14 | 82 | 06       | 651.12.I    |                 |
| SUA750RMI2U      | 07 | B1 | 0D | 82 | 86       | 619.12.I    |                 |
| SUA1000I         | 07 | B5 | 13 | BC | 0A       | 652.12.I    | 24v             |
| SUA1000XLI       | 0B | BD | 0F | 7F | 4A       | 681.13.I    |                 |
| SUA1500I         | 09 | B9 | 13 | A1 | 0E       | 601/653.x.I | 24v             |
| SUA1500RMI2U     | 08 | B4 | 10 | A1 | 8E       | 617.3.I     |                 |
| SUA2200I         | 08 | B8 | 12 | B3 | 26       | 654.12.I    |                 |
| SUA2200RMI2U     | 09 | BC | 11 | 81 | A6       | 665.4.I     |                 |
| SUA2200XLI       | 0A | B7 | 0F | 7F | 66       | 690.x.I     |                 |
| SUA3000RMI2U     | 04 | B9 | 0E | 70 | AA       | 666.4.I     |                 |
| SUA3000RMXLI3U   | 0A | B6 | 0E | 89 | xx       | xxx.x.x     |                 |
| SUOL1000I        | 06 | B6 | 1B | A6 |          |             |                 |
| SUOL2000XL       | 0D | BD | 14 | 75 | 52       | 416.5.I     |                 |
| SURT1000XLI      | 0A | BB | 19 | A8 | 4E       | 411.x.I     |                 |
| SURT3000XLI      | 06 | B6 | 0F | CA | 56       | 450.2.I     |                 |
| SURT5000XLI      | 05 | BA | 15 | 86 | 5A       | 451.13.W    |                 |
| SURT6000XLI      | 07 | BE | 24 | 7E |          |             |                 |
| SURT7500XLI      | 03 | BB | 20 | 97 | 63       |             |                 |
| SURT8000XLI      | 0A | C0 | 28 | 8F |          |             |                 |
| SURT10000XLI     | 06 | B8 | 19 | 7E |          | 476.12.W    |                 |
| SURTA1500XL      | 05 | B7 | 12 | A0 |          |             |                 |
| SURTA1500XLJ     | 05 | B7 | 12 | A0 |          |             |                 |
| SURTA2000XL      | 04 | BC | 19 | 7E |          |             |                 |
| SURTA2400XLJ     | 0C | B5 | 10 | E4 |          |             |                 |
| SURTA3000XL      | 0C | BD | 1F | C2 |          |             |                 |
| SUM1500RMXLI2U   | 03 | B7 | 0D | A5 | 62       | 716.3.I     |                 |
| SUM3000RMXLI2U   | 03 | B7 | 0D | A5 | 6A       | 715.3.I     |                 |
