# Configurare il lettore tessere in Linux

### Descrizione

> _Configurazione provata su Linux Mint 21 LTS "Vanessa"_

## Comandi

Collegare il lettore e inserire la tessera sanitaria:

Aggiornare il sistema operativo

`sudo apt update && sudo apt upgrade -y`

Installare le librerie, gli strumenti e il middleware

`sudo apt install -y libccid pcscd opensc libacsccid1 pcsc-tools`

Verifica corretto funzionamento del lettore, a tessera inserita dare il comando da terminale

`pcsc_scan`

L'output sarà qualcosa di simile, le descrizioni cambiano in base al lettore e alla tessera sanitaria

```
Using reader plug'n play mechanism
Scanning present readers...
0: bit4id miniLector-EVO [miniLector-EVO] 00 00
 
Sat Oct  8 11:35:58 2022
 Reader 0: bit4id miniLector-EVO [miniLector-EVO] 00 00
  Event number: 0
  Card state: Card inserted, 
  ATR: 3B FF 18 00 00 81 31 FE 45 00 6B 05 05 10 17 01 21 01 43 4E 53 10 31 80 5E

ATR: 3B FF 18 00 00 81 31 FE 45 00 6B 05 05 10 17 01 21 01 43 4E 53 10 31 80 5E
+ TS = 3B --> Direct Convention
+ T0 = FF, Y(1): 1111, K: 15 (historical bytes)
  TA(1) = 18 --> Fi=372, Di=12, 31 cycles/ETU
    129032 bits/s at 4 MHz, fMax for Fi = 5 MHz => 161290 bits/s
  TB(1) = 00 --> VPP is not electrically connected
  TC(1) = 00 --> Extra guard time: 0
  TD(1) = 81 --> Y(i+1) = 1000, Protocol T = 1 
-----
  TD(2) = 31 --> Y(i+1) = 0011, Protocol T = 1 
-----
  TA(3) = FE --> IFSC: 254
  TB(3) = 45 --> Block Waiting Integer: 4 - Character Waiting Integer: 5
+ Historical bytes: 00 6B 05 05 10 17 01 21 01 43 4E 53 10 31 80
  Category indicator byte: 00 (compact TLV data object)
    Tag: 6, len: B (pre-issuing data)
      Data: 05 05 10 17 01 21 01 43 4E 53
    Mandatory status indicator (3 last bytes)
      LCS (life card cycle): 10 (Proprietary)
      SW: 3180 (Error not defined by ISO 7816)
+ TCK = 5E (correct checksum)

Possibly identified card (using /usr/share/pcsc/smartcard_list.txt):
3B FF 18 00 00 81 31 FE 45 00 6B 05 05 10 17 01 21 01 43 4E 53 10 31 80 5E
	Regional Card - Regione Liguria, Veneto - Italy (eID)
	Tessera Sanitaria - Carta Regionale dei Servizi
```

Scaricare il programma di gestione delle firme _CRSManager_ dal sito di [ARIA](https://www.ariaspa.it/wps/portal/Aria/Home/DettaglioRedazionale/cosa--facciamo/innovazione-digitale/certificazione-digitale/software-cns)

Oppure usare il comando wget (In caso installarlo: `sudo apt install -y wget`)

`wget -q -O CRSManager.run https://www.ariaspa.it/wps/wcm/connect/7e4b38f4-bbf0-456a-8fb5-8dde442604e2/CRSManager.run?MOD=AJPERES&CACHEID=ROOTWORKSPACE-7e4b38f4-bbf0-456a-8fb5-8dde442604e2-obVps5-`

Dare i permessi di esecuzione al file scaricato

`chmod +x CRSManager.run`

Eseguire l'installazione

`sudo ./CRSManager.run`

Avvio del CRS Manager da terminale

`crsLinux.sh`

La prima volta scarica i certificati, quando finisce dare CTSL+C e rilanciarlo

### In caso di problemi

Riavviare il demone PC/SC

`sudo systemctl restart pcscd`

provare ad installare le seguenti librerie una alla volta finché va:

Scaricare dal sito [sanita.finanze.it](https://sistemats1.sanita.finanze.it/portale/elenco-driver-cittadini-modalita-accesso) il pacchetto in base al proprio sistema operativo ed installarlo tramite il comando

`sudo dpkg -i libbit4xpki-idemia-amd64.1.4.10-622.deb`

Questo pacchetto installa le librerire in /usr/lib/bit4id/ configurare il CRSManager in modo che punti alla libreria `/usr/lib/bit4id/libbit4opki.so`
Lo stesso vale se si vuole configurare Firefox.

In caso non funziona ancora provare ad installare le seguenti librerie:

`sudo apt install -y opensc-pkcs11`

`sudo apt install libpcsclite1`

`sudo apt install libnss3-tools`

`sudo apt install zlib1g-dev`
