# nfclib

## Read/write MIFARE classic

Command `nfc-mfclassic`

## Read card ID

Place card on reader and issue command `nfc-list`

```bash
$ nfc-list
nfc-list uses libnfc 1.8.0
NFC device: Adafruit PN532 board via UART opened
1 ISO14443A passive target(s) found:
ISO/IEC 14443A (106 kbps) target:
    ATQA (SENS_RES): 00  04  
       UID (NFCID1): c4  5c  ec  ed  
      SAK (SEL_RES): 08  

```
