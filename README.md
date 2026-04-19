## Proiect InkTime
<img width="1176" height="855" alt="Screenshot 2026-04-20 013859" src="https://github.com/user-attachments/assets/08c8b449-cc6c-4a48-be57-613a13d5e7a2" />

## Diagrama Bloc
Sistemul este organizat in jurul microcontroller-ului nRF52840, care gestioneaza comunicarea Bluetooth, procesarea datelor de la senzori si controlul afisajului.
<img width="1148" height="888" alt="Screenshot 2026-04-20 022923" src="https://github.com/user-attachments/assets/33c5ee89-8255-4a05-b4a3-ce5a7932d7f6" />

## BOM (Bill Of Materials)
| Component | Part Number | Package | Function | Datasheet |
|---|---|---|---|---|
| MCU | nRF52840-QIAA-R | aQFN73 (7x7) | Microcontroller + BLE + USB | [Datasheet](https://docs.nordicsemi.com/) |
| Charger / Power Path | BQ25180YBGR | DSBGA-8 | Li-Ion/LiPo charger with power path | [Datasheet](https://www.ti.com/lit/ds/symlink/bq25180.pdf) |
| Buck-Boost Regulator | RT6160AWSC | WLCSP-15 | 3.3V system rail regulator | [Datasheet](https://www.richtek.com/assets/product_file/RT6160A/DS6160A-05.pdf) |
| Fuel Gauge | MAX17048G+T10 | DFN-8 (2x2) | Battery SOC monitoring | [Datasheet](https://www.analog.com/media/en/technical-documentation/data-sheets/MAX17048-MAX17049.pdf) |
| Accelerometer | BMA421 | LGA-12 (2x2) | Step counting + motion wake | [Datasheet](https://jlcpcb.com/partdetail/Bosch_Sensortec-BMA421/C5242966) |
| Haptic Driver | DRV2605LDGSR | VSSOP-10 | ERM motor driver with effects library | [Datasheet](https://www.ti.com/lit/ds/symlink/drv2605l.pdf) |
| PFET (EPD power) | SI2301CDS | SOT-23 | E-paper display power gating | [Datasheet](https://jlcpcb.com/partdetail/Changjiang_Electronics_Tech_CJ-SI2301CDS/C10487) |
| USB ESD Protection | USBLC6-2SC6Y | SOT-23-6 | ESD protection on USB data lines | [Datasheet](https://www.st.com/resource/en/datasheet/usblc6-2.pdf) |
| USB Type-C Connector | KH-TYPE-C-16P | 16-pin SMD | USB charging + data | [Datasheet](https://www.google.com/search?q=%23) |
 
> Toate rezistentele folosite sunt in capsula **0201**. Condensatoarele de bypass/decuplare de **100nF** sunt **0201**, iar cele care depasesc **100nF** sunt **0402**, conform constrangerilor de design.

## Functionalitate Hardware

### Module si Senzori

- **MCU – nRF52840:** Ales pentru consumul redus de energie si capabilitatile Bluetooth Low Energy (BLE). Acesta gestioneaza protocolul SPI pentru ecran, I2C pentru senzori si controleaza starea sistemului.

- **Display E-Paper:** Ofera o lizibilitate excelenta in lumina soarelui si consuma energie doar in momentul refresh-ului, fiind ideal pentru un smartwatch unde autonomia bateriei este critica.

- **Management Putere:** Sistem de power path si incarcare cu BQ25180YBGR, impreuna cu regulatorul Buck-Boost RT6160AWSC care asigura o tensiune stabila de 3.3V, indiferent de nivelul de descarcare al bateriei Li-Po. Monitorizarea precisa a bateriei (SOC) este realizata de integratul MAX17048G+T10.

- **Senzor Miscare:** Accelerometrul BMA421 este folosit pentru detectarea miscarii mainii (ex: "lift-to-wake" pentru a trezi ecranul din sleep) si pentru aplicatii de tip pedometru (step counting).

- **Feedback Haptic:** Motorul ERM este controlat precis de driverul DRV2605LDGSR, care include o librarie interna de efecte haptice.

---

### Specificatii Comunicatie

- **SPI (Display):** Interfata rapida pentru a asigura un refresh optim al ecranului (semnale MOSI, SCK, CS, DC).

- **I2C (Senzori & Power):** Folosita pentru comunicarea cu accelerometrul, fuel gauge-ul, charger-ul si driverul haptic.

- **SWD (Serial Wire Debug):** Interfata hardware standard de la ARM, conectata la un conector TC2030, folosita pentru incarcarea codului pe placa si pentru depanare pas cu pas a software-ului.

---

## Descriere pini nRF52840  

| Pin | Descriere |
|-----|----------|
| VDD | Alimentare 3V3 |
| DCC | Power regulation |
| DEC4 | Power regulation |
| VSS | GND |
| P0.02 / AIN0 | SPI SCK (clock pentru display) |
| P0.02 / AIN0 | SPI MOSI (master output slave in) |
| DEC2 | GND, power regulation |
| VDD | Alimentare 3V3 |
| XC2, XC1 | Oscilator X1 (32 MHz) |
| DEC3 | GND |
| DEC6 | Power regulation |
| VSS_PA | Alimentare antenă |
| ANT | Conectare antenă |
| P0.10 / NFC2 | Semnal alertă baterie (Fuel Gauge) |
| DEC5 | GND, power regulation |
| P1.02 | Buton Down |
| P1.01 | Control alimentare display |
| SWDIO, SWDCLK | Programare și debug |
| VDD | Alimentare 3V3 |
| VSS_PAD | GND |
| P1.00 | SWO (debug) |
| P0.18 / RESET | Pin Reset |
| P0.17, P0.16, P0.15 | Interfață display |
| P0.13, P0.14 | Butoane Enter / Up |
| D-, D+ | USB (transmisie diferențială) |
| VBUS | Alimentare USB 5V |
| DEC3V3 | GND (intern, power regulation) |
| DCCH | Nefolosit |
| VDDH, VDD | Alimentare 3V3 |
| P0.12 | Enable driver haptic |
| P0.11 | Alertă alimentare (de la LiPo Charger) |
| P1.08, P0.08 | Interrupții IMU |
| P0.07, P0.06 | I2C (SCL, SDA) |
| P0.05 / AIN3 | Chip Select display |
| XL2, XL1 | Oscilator X2 (32 kHz) |
| DEC1 | GND, power regulation |
