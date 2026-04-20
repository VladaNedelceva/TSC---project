# InkTime Smartwatch — Proiect TSC 2026


## Diagrama Bloc

```
                        ┌─────────────────────────────────────────┐
                        │            nRF52840 (U$1)               │
                        │         BLE SoC + MCU principal         │
                        │                                         │
          ┌─────────────┤ I2C (SDA/SCL)    SPI (MOSI/SCK/CS)    ├──────────────┐
          │             │                                         │              │
          │    ┌────────┤ I2C              GPIO (EN/INT)         ├──────┐        │
          │    │        │                                         │      │        │
          │    │        │ GPIO (UP/ENT/DN) SWDCLK/SWDIO/SWO     │      │        │
          │    │        └──────┬──────────────────┬──────────────┘      │        │
          │    │               │                  │                      │        │
    ┌─────▼──┐ │         ┌─────▼─────┐    ┌──────▼──────┐        ┌─────▼──┐    │
    │BQ25180 │ │         │  Butoane  │    │  TC2030-IDC │        │DRV2605 │    │
    │LiPo    │ │         │SW_UP      │    │  SWD Debug  │        │Haptic  │    │
    │Charger │ │         │SW_ENT     │    │  Connector  │        │Driver  │    │
    └───┬────┘ │         │SW_DN      │    └─────────────┘        └───┬────┘    │
        │      │         └───────────┘                               │         │
    ┌───▼────┐ │                                               ┌─────▼──┐      │
    │ LiPo  │ │    ┌──────────────────────┐                   │ Motor  │      │
    │Battery│ │    │  RT6160AWSC          │                   │Haptic  │      │
    └───────┘ │    │  DC/DC Converter     │                   └────────┘      │
              │    │  (VREG 3.3V)         │                                    │
    ┌─────────▼┐   └──────────────────────┘              ┌─────────────────────▼┐
    │MAX17048  │                                          │  503480-2400         │
    │Fuel Gauge│         ┌───────────────┐               │  E-Paper FPC 24pin   │
    │(ALERT)   │         │  BMA421       │               │  Connector           │
    └──────────┘         │  IMU Accel    │               └──────────────────────┘
                         │  (INT1/INT2)  │
                         └───────────────┘          ┌─────────────────────────┐
                                                     │  KH-TYPE-C-16P          │
                         ┌───────────────┐           │  USB-C Connector        │
                         │ 2450AT18B100E │           │  + USBLC6 ESD           │
                         │ Chip Antenna  │           └─────────────────────────┘
                         │ 2.4GHz BLE   │
                         └───────────────┘
```

---

## BOM (Bill of Materials)

| Ref | Componentă | Valoare | Package | Cantitate | Link JLC | Datasheet |
|-----|-----------|---------|---------|-----------|----------|-----------|
| U$1 | nRF52840 | - | AQFN50 7x7mm | 1 | [JLC](https://jlcpcb.com/partdetail/NordicSemiconductor-nRF52840_QIAA/C190794) | [DS](https://infocenter.nordicsemi.com/pdf/nRF52840_PS_v1.7.pdf) |
| IC1 | BQ25180YBGR | - | BGA 1.0x1.55mm | 1 | [JLC](https://jlcpcb.com/partdetail/TexasInstruments-BQ25180YBGR/C2665644) | [DS](https://www.ti.com/lit/ds/symlink/bq25180.pdf) |
| IC2 | RT6160AWSC | - | BGA 1.4x2.3mm | 1 | [JLC](https://jlcpcb.com/partdetail/RichTek-RT6160AWSC/C2826062) | [DS](https://www.richtek.com/assets/product_file/RT6160A/DS6160A-01.pdf) |
| IC3 | BMA421 | - | LGA 2x2mm | 1 | [JLC](https://jlcpcb.com/partdetail/Bosch-BMA421/C2837244) | [DS](https://www.bosch-sensortec.com/media/boschsensortec/downloads/datasheets/bst-bma421-ds000.pdf) |
| IC4 | DRV2605YZFR | - | BGA 1.44x1.44mm | 1 | [JLC](https://jlcpcb.com/partdetail/TexasInstruments-DRV2605YZFR/C2066821) | [DS](https://www.ti.com/lit/ds/symlink/drv2605.pdf) |
| U3 | MAX17048G+T10 | - | SOT23-6 | 1 | [JLC](https://jlcpcb.com/partdetail/MaximIntegrated-MAX17048GT10/C112196) | [DS](https://datasheets.maximintegrated.com/en/ds/MAX17048-MAX17049.pdf) |
| J1 | TC2030-IDC | - | TC2030-IDC | 1 | [JLC](https://jlcpcb.com/partdetail/TagConnect-TC2030IDC/C2682595) | [DS](https://www.tag-connect.com/wp-content/uploads/bsk-pdf-manager/TC2030-IDC_1.pdf) |
| J2 | 503480-2400 | - | FPC 24pin 0.5mm | 1 | [JLC](https://jlcpcb.com/partdetail/Molex-5034802400/C393465) | [DS](https://www.molex.com/pdm_docs/sd/5034802400_sd.pdf) |
| J4 | KH-TYPE-C-16P | - | USB-C 16pin | 1 | [JLC](https://jlcpcb.com/partdetail/Korean_Hroparts_Elec-TYPE_C_16P/C2765186) | [DS](https://datasheet.lcsc.com/lcsc/2206011830_Korean-Hroparts-Elec-TYPE-C-16P_C2765186.pdf) |
| ANT1 | 2450AT18B100E | - | SMD | 1 | [JLC](https://jlcpcb.com/partdetail/Johanson-2450AT18B100E/C89719) | [DS](https://www.johansontechnology.com/datasheets/2450AT18B100E/2450AT18B100E.pdf) |
| D3 | USBLC6-2SC6Y | - | SOT363 | 1 | [JLC](https://jlcpcb.com/partdetail/STMicroelectronics-USBLC6_2SC6Y/C2827693) | [DS](https://www.st.com/resource/en/datasheet/usblc6-2.pdf) |
| D2,D4,D5 | MBR0530 | - | SOD-123 | 3 | [JLC](https://jlcpcb.com/partdetail/Onsemi-MBR0530T1G/C181024) | [DS](https://www.onsemi.com/pdf/datasheet/mbr0530t1-d.pdf) |
| Q3 | SI1308EDL-T1-GE3 | - | SOT23-3 | 1 | [JLC](https://jlcpcb.com/partdetail/Vishay-SI1308EDLT1GE3/C2102724) | [DS](https://www.vishay.com/docs/63508/si1308edl.pdf) |
| X1 | Crystal | 32MHz | SMD | 1 | [JLC](https://jlcpcb.com/partdetail/Txc-7M32000020/C255888) | - |
| X2 | Crystal | 32.768kHz | SMD | 1 | [JLC](https://jlcpcb.com/partdetail/Micro_Crystal-CM8V_T1A/C32346) | - |
| L1 | Inductor | 3.9nH | 0201 | 1 | [JLC](https://jlcpcb.com/partdetail/Tdk-MLF1608DR39KTD25/C1046) | - |
| L2 | Inductor | 10µH | MLP2016 | 1 | [JLC](https://jlcpcb.com/partdetail/Taiyo_Yuden-NR3015T100M/C408336) | - |
| L3 | Inductor | 15nH | 0201 | 1 | [JLC](https://jlcpcb.com/partdetail/Tdk-MLF1608DR15KTD25/C1045) | - |
| L5 | Inductor | 68µH | MLP2016 | 1 | [JLC](https://jlcpcb.com/partdetail/FTC252012SR47MBCA/C408335) | - |
| L7 | Inductor | 0.47µH | MLP2016 | 1 | [JLC](https://jlcpcb.com/partdetail/FTC252012SR47MBCA/C408335) | - |
| SW_UP,SW_ENT,SW_DN | EVP-AKE31A | - | EVP-AKE31A | 3 | [JLC](https://jlcpcb.com/partdetail/Panasonic-EVPAKE31A/C2926735) | [DS](https://industrial.panasonic.com/cdbs/www-data/pdf/ATK0000/ATK0000CE5.pdf) |
| R1_USB,R2_USB | Rezistor | 5K1 | 0201 | 2 | [JLC](https://jlcpcb.com/partdetail/21388-0201WAF5101T5E/C27853) | - |
| R17,R18 | Rezistor | 3K3 | 0201 | 2 | [JLC](https://jlcpcb.com/partdetail/21388-0201WAF3301T5E/C22978) | - |
| R5,R7,R8 | Rezistor | 10k | 0201 | 3 | [JLC](https://jlcpcb.com/partdetail/21388-0201WAF1002T5E/C22775) | - |
| R9,R_PWR_EPD,R2_EP_DR | Rezistor | 10K | 0201 | 3 | [JLC](https://jlcpcb.com/partdetail/21388-0201WAF1002T5E/C22775) | - |
| R2,R3,R4 | Rezistor | 0Ω | 0201 | 3 | [JLC](https://jlcpcb.com/partdetail/21388-0201WAF0000T5E/C17168) | - |
| R1_EP_DR | Rezistor | 0.47Ω | 0201 | 1 | [JLC](https://jlcpcb.com/partdetail/0201WAF_R47T5E/C105872) | - |
| R_TYPE_SEL | Rezistor | 2.2Ω | 0201 | 1 | [JLC](https://jlcpcb.com/partdetail/0201WAF2R20T5E/C105876) | - |
| C1,C17,C18,C26 | Condensator | 12pF | 0201 | 4 | [JLC](https://jlcpcb.com/partdetail/21342-CL03A120JQ3NNNC/C32949) | - |
| C3,C4 | Condensator | 1pF | 0201 | 2 | [JLC](https://jlcpcb.com/partdetail/SamsungElectro_Mechanics-CL03A1R0BC3NNNC/C32U) | - |
| C5,C7,C8,C12,C19 | Condensator | 100nF | 0201 | 5 | [JLC](https://jlcpcb.com/partdetail/21342-CL03B104KO3NNNC/C21120) | - |
| C6,C14,C20,C21 | Condensator | 4.7µF | 0402 | 4 | [JLC](https://jlcpcb.com/partdetail/21342-CL05A475MO5NRNC/C25126) | - |
| C9 | Condensator | 820pF | 0402 | 1 | [JLC](https://jlcpcb.com/partdetail/21342-CL05B821KB5NNNC/C131229) | - |
| C11 | Condensator | 100pF | 0402 | 1 | [JLC](https://jlcpcb.com/partdetail/21342-CL05B101KB5NNNC/C32U) | - |
| C15 | Condensator | 1.0µF | 0402 | 1 | [JLC](https://jlcpcb.com/partdetail/21342-CL05A105KO5NNNC/C52923) | - |
| C16 | Condensator | 47nF | 0402 | 1 | [JLC](https://jlcpcb.com/partdetail/21342-CL05B473KO5NNNC/C22947) | - |
| C23,C27,C34,C42 | Condensator | 0.1µF | 0201/0402 | 4 | [JLC](https://jlcpcb.com/partdetail/21342-CL03B104KO3NNNC/C21120) | - |
| C24,C39 | Condensator | 10µF | 0402 | 2 | [JLC](https://jlcpcb.com/partdetail/21342-CL05A106MQ5NUNC/C15525) | - |
| C25,C33 | Condensator | 22µF | 0402 | 2 | [JLC](https://jlcpcb.com/partdetail/21342-CL05A226MP5NUNC/C45783) | - |
| C29,C30,C31,C32,C37,C38 | Condensator | 1µF | 0201 | 6 | [JLC](https://jlcpcb.com/partdetail/21342-CL03A105MQ3CSN/C1588) | - |
| C43 | Condensator | 4.7µF | 0402 | 1 | [JLC](https://jlcpcb.com/partdetail/21342-CL05A475MO5NRNC/C25126) | - |
| EPD_C1..C12 | Condensator | 1µF/50V | 0402 | 10 | [JLC](https://jlcpcb.com/partdetail/21342-CL05A105KO5NNNC/C52923) | - |
| C1-EP-DR | Condensator | 10µF | 0402 | 1 | [JLC](https://jlcpcb.com/partdetail/21342-CL05A106MQ5NUNC/C15525) | - |

---

## Descrierea Funcționalității Hardware

### Microcontroller — nRF52840 (U$1)
Creierul dispozitivului. SoC ARM Cortex-M4F la 64MHz cu BLE 5.0 integrat, 1MB Flash, 256KB RAM. Alimentat la 3.3V de la DC/DC converter. Cristal extern 32MHz pentru clock principal și 32.768kHz pentru RTC (timp real în sleep mode).

### Alimentare — BQ25180 (IC1) + RT6160AWSC (IC2)
- **BQ25180** — încărcător LiPo cu curent programabil, monitorizare temperatură prin NTC (R9 10K). Bateria se conectează direct la două test pad-uri (TP_VBAT, TP_BAT_GND), fără conector JST.
- **RT6160AWSC** — DC/DC buck-boost converter care generează 3.3V stabil (VREG) din tensiunea bateriei (3.0–4.2V). Inductanță externă L2 10µH, condensatori output 22µF × 2.
- **MAX17048 (U3)** — fuel gauge pe I2C, măsoară SOC (state of charge) baterie prin modelarea tensiunii. Trimite alertă prin pinul ALERT.

### Display E-Paper — via FPC J2 (503480-2400)
Conectat prin SPI la nRF52840. Circuit de drive dedicat cu boost converter (L5 68µH, diode MBR0530) care generează tensiunile PREVGH/PREVGL necesare display-ului e-paper. MOSFET Q3 (SI1308EDL) controlează alimentarea display-ului. Condensatori serie (EPD_C1..C12, 1µF/50V) pe liniile de date pentru protecție.

**Interfață SPI:**
- MOSI → P0.24
- SCK → P0.25
- EPD_CS → P1.01
- EPD_DC → P0.15
- EPD_RST → P0.16
- EPD_BUSY → P0.17

### IMU — BMA421 (IC3)
Accelerometru 3-axis pe I2C. Detectează mișcări, pași, gesturi wrist-tilt. Două linii de întrerupere (INT1, INT2) conectate la GPIO nRF pentru wake-up din sleep.

### Haptic Feedback — DRV2605 (IC4)
Driver haptic pe I2C cu bibliotecă de efecte tactile integrate. Controlează un motor LRA/ERM. Activat prin pin HAPTIC_EN (GPIO).

### USB-C — KH-TYPE-C-16P (J4)
Conector USB-C 16 pini. Rezistențe CC1/CC2 de 5.1kΩ pentru identificare ca device. Protecție ESD prin USBLC6-2SC6Y (D3). VBUS conectat la BQ25180 pentru încărcare.

### Comunicație Wireless — ANT1 (2450AT18B100E)
Antenă chip 2.4GHz pentru BLE 5.0. Plasată la exteriorul PCB-ului (colț dreapta-sus). PCB-ul este decupat sub antenă — nu există cupru sau trasee sub suprafața antenei. Circuit de matching RF: L1 (3.9nH), L3 (15nH), C3 (1pF).

### Butoane — SW_UP, SW_ENT, SW_DN (EVP-AKE31A)
Trei butoane tactile Panasonic plasate pe muchia de jos a PCB-ului, aliniate cu decupajele din carcasă. Pull-up 10kΩ și condensator de filtrare 1µF per buton.

### Debug — TC2030-IDC (J1)
Conector Tag-Connect pentru programare SWD fără pini de header. Semnale: SWDCLK, SWDIO, SWO, RESET, 3.3V, GND.

### Consum Energetic (estimativ)
| Mod | Curent | Durată |
|-----|--------|--------|
| BLE Advertising | ~3mA | periodic |
| BLE Connected | ~5mA | activ |
| Deep Sleep | ~2µA | idle |
| Display refresh | ~20mA | ~2s |
| IMU activ | ~500µA | continuu |
| **Medie estimată** | **~1.5mA** | |

Cu baterie 300mAh → autonomie estimată ~200 ore (~8 zile).

---

## Pinii nRF52840 Utilizați

| Pin nRF | Funcție | Componentă | Motiv alegere |
|---------|---------|-----------|---------------|
| P0.00/XL1 | Crystal IN | X2 (32.768kHz) | Pin dedicat cristal RTC |
| P0.01/XL2 | Crystal OUT | X2 (32.768kHz) | Pin dedicat cristal RTC |
| P0.04/AIN2 | Analog IN | - | ADC disponibil |
| P0.13 | HAPTIC_EN | DRV2605 IC4 | GPIO disponibil |
| P0.14 | EPD_CS | E-Paper | GPIO SPI CS |
| P0.15 | EPD_DC | E-Paper | GPIO SPI DC |
| P0.16 | EPD_RST | E-Paper | GPIO reset |
| P0.17 | EPD_BUSY | E-Paper | GPIO status |
| P0.18/RESET | RESET | TC2030 J1 | Pin reset hardware dedicat |
| P0.24 | MOSI | E-Paper SPI | SPI MOSI |
| P0.25 | SCK | E-Paper SPI | SPI Clock |
| P0.26 | SDA | I2C bus | I2C Data (BQ25180, BMA421, DRV2605, MAX17048) |
| P0.27 | SCL | I2C bus | I2C Clock |
| P1.01 | EPD_CS | E-Paper | SPI Chip Select |
| P1.02 | SW_UP | Buton UP | GPIO cu pull-up intern |
| P1.08 | SW_ENT | Buton ENTER | GPIO cu pull-up intern |
| P1.09 | SW_DN | Buton DOWN | GPIO cu pull-up intern |
| SWDCLK | SWDCLK | TC2030 J1 | Debug SWD Clock |
| SWDIO | SWDIO | TC2030 J1 | Debug SWD Data |
| P0.09/SWO | SWO | TC2030 J1 | Serial Wire Output trace |
| VBUS | VBUS | USB-C J4 | Detecție USB conectat |
| D+ | D+ | USB-C J4 | USB Data+ |
| D- | D- | USB-C J4 | USB Data- |
| ANT | RF | ANT1 | Antenă BLE 2.4GHz |

---

## Test Pad-uri

| Test Pad | Semnal | Scop |
|----------|--------|------|
| TP_3V3 | 3.3V | Verificare tensiune alimentare |
| TP_VREG | VREG | Verificare output DC/DC |
| TP_SCL | I2C SCL | Debug I2C |
| TP_SDA | I2C SDA | Debug I2C |
| TP_SWDCLK | SWDCLK | Programare SWD |
| TP_SWDIO | SWDIO | Programare SWD |
| TP_SWO | SWO | Trace debug |
| TP_RESET | RESET | Reset hardware |
| TP_3.3V | 3.3V | Redundant alimentare |
| TP_GND | GND | Masă referință |
| TP_VBAT | VBAT | Tensiune baterie |
| TP_BAT_GND | GND baterie | Masă baterie |

---

## Design Log

### Decizii luate

- **Grosime PCB 1mm** (nu 1.6mm standard) — conform cerințelor mecanice pentru a intra în carcasă.
- **Rutare 2 layere** — Top pentru componente și trasee principale, Bottom pentru trasee secundare și plan de masă. Via stitching aplicat între planurile de masă, în special în zona antenei.
- **Trasee putere 0.3mm** — VCC, VUSB, VBUS, 3V3 rutate la 0.3mm. Trasee de semnal la minimum 0.15mm.
- **Decupaj sub antenă** — Zona de sub ANT1 (2450AT18B100E) este exclusă din planul de masă și nu conține trasee.
- **Condensatori de decuplare 100nF** — Plasați cât mai aproape de pinii de alimentare ai fiecărui IC.
- **Butoane aliniate cu carcasa** — SW_UP, SW_ENT, SW_DN plasate la coordonatele exacte din inktime.fbrd pentru aliniere cu butoanele fizice ale carcasei.
- **Baterie fără conector JST** — Conectată direct la TP_VBAT și TP_BAT_GND pentru economie de spațiu.
- **Erori ignorate** — Erorile de Dimension cauzate de amplasarea butoanelor și mufei USB sunt neglijate conform specificațiilor proiectului. Eroarea "Only INPUT pins on NET ID" ignorată conform instrucțiunilor.

### Probleme întâmpinate

- Plasarea componentelor a necesitat ajustări manuale pentru a respecta atât layout-ul recomandat cât și constrângerile mecanice ale carcasei.
- Zona de sub antena chip necesită atenție specială — orice cupru în această zonă degradează performanța RF.
- Condensatoarele EPD de 1µF/50V trebuie să fie rated la tensiunea mai mare datorită tensiunilor generate de circuitul boost al display-ului.


