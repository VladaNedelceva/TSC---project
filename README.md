# TSC---project


# InkTime

Smartwatch ieftin și open source bazat pe nRF52840, cu display e-paper. Proiect realizat în cadrul cursului TSC 2026.

---

## Cum funcționează hardware-ul

### nRF52840

MCU-ul principal. Rulează totul: BLE, USB, SPI spre display, I2C spre periferice. Alimentat la 3.3V. Are două cristale: 32MHz pentru radio și 32.768kHz pentru RTC (low power).

Circuitul de matching pentru antenă (L1, L3, C3, C4) e cam mic și delicat de rutate, dar e conform schemei de referință din datasheet.

### Alimentare

Bateria LiPo se încarcă prin **BQ25180** (IC1) direct de pe VBUS USB-C. Tensiunea bateriei (VREG) intră în **RT6160A** (IC2), un regulator buck-boost care scoate 3.3V indiferent de nivelul bateriei. **MAX17048** (U3) monitorizează starea de încărcare prin I2C și poate da un ALERT când bateria e aproape goală.

Am legat bateria direct la două test pad-uri (TP_VBAT, TP_BAT_GND) fără conector JST, ca să economisesc spațiu conform cerințelor proiectului.

### Display E-Paper

Conectat prin FPC 24 pini (J2). MCU-ul comunică prin SPI (SCK pe P0.02, MOSI pe P0.03) + semnale de control (CS, DC, RST, BUSY). Circuitul de drive al displayului (boost cu L5, diode Schottky, Q1, Q3) generează tensiunile necesare panoului e-paper, care sunt mai mari decât 3.3V.

### IMU BMA423

Accelerometru pe I2C, același bus cu restul. CSB legat la 3.3V ca să fie forțat modul I2C (altfel merge pe SPI). Are două linii de întrerupere (INT1 pe P0.08, INT2 pe P1.08) pentru step counter, wakeup etc.

### Haptic

DRV2605 pe I2C, activat de MCU prin pinul EN (P0.12). Suportă atât motoare ERM cât și LRA.

### USB-C

Mufa KH-TYPE-C-16P cu protecție ESD USBLC6. R1_USB și R2_USB (5.1kΩ) pe CC1/CC2 pentru ca sursa să știe că e un device normal. Condensatoarele C42/C43 filtrează VBUS.

### Butoane

Trei butoane (UP/ENT/DN), fiecare cu pull-up 10kΩ la 3.3V și condensator 1uF pentru debounce hardware.

---

## Pinii nRF52840

| Pin | Semnal | Ce face |
|-----|--------|---------|
| P0.00/XL1 | XL1 | Cristal 32kHz |
| P0.01/XL2 | XL2 | Cristal 32kHz |
| P0.02 | SCK | SPI clock spre EPD |
| P0.03 | MOSI | SPI data spre EPD |
| P0.05 | EPD_CS | Chip select EPD |
| P0.06 | SDA | I2C data |
| P0.07 | SCL | I2C clock |
| P0.08 | IMU_INT1 | Întrerupere BMA423 |
| P0.11 | PMIC_INT | Întrerupere BQ25180 |
| P0.12 | HAPTIC_EN | Activare DRV2605 |
| P0.13 | SW_UP | Buton sus |
| P0.14 | SW_ENT | Buton enter |
| P0.15 | EPD_DC | Data/Command EPD |
| P0.16 | EPD_RST | Reset EPD |
| P0.17 | EPD_BUSY | Busy EPD |
| P0.18 | RESET | Reset hardware |
| P1.00 | SWO | SWD trace |
| P1.01 | EPD_PWR | Control alimentare EPD |
| P1.02 | SW_DN | Buton jos |
| P1.08 | IMU_INT2 | Întrerupere BMA423 #2 |

I2C-ul e shared între RT6160A, BQ25180, MAX17048, BMA423 și DRV2605. Fiecare are adresă diferită, sper că nu e vreo coliziune :)

---

## Note și decizii de design

- PCB dublu strat, 1mm grosime (nu 1.6mm standard!)
- Toate componentele pe TOP layer
- Antena la marginea PCB-ului, cu decupaj sub ea (no copper)
- Bateria conectată direct la test pad-uri, fără JST
- Am acceptat câteva erori de overlap la butoane și mufa USB din cauza constrângerilor mecanice ale carcasei

