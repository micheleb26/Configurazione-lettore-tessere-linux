# Configurare il lettore tessere in Linux

## Indice
1. [Installazione dei driver e degli strumenti](#installazione)
2. [In caso di problemi](#problemi)
3. [Configurazione di firefox](./configurazione_firefox.md)
4. [Configurazione del CRS Manager](./configurazione_crsmanager.md)
5. [Per cultura](#cultura)
6. [Riferimenti](#riferimenti)

### Descrizione

> _Configurazione provata su Linux Mint 21 LTS "Vanessa" utilizzando un lettore di tessere [bit4id minilector EVO](https://www.amazon.it/gp/product/B0081SW1GE/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)._
> 
> _Lettori di schede diversi da quello riportato, potrebbero aver bisogno di configurazioni e/o librerie di sistema diverse da quelle descritte in questo articolo._

## Installazione<a id="installazione"></a>

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

1. `wget -c -q -O CRSManager.run https://www.ariaspa.it/wps/wcm/connect/7e4b38f4-bbf0-456a-8fb5-8dde442604e2/CRSManager.run?MOD=AJPERES&CACHEID=ROOTWORKSPACE-7e4b38f4-bbf0-456a-8fb5-8dde442604e2-obVps5-`

2. `wget -qc -O CRSManager.run.sha256 https://raw.githubusercontent.com/micheleb26/Configurazione-lettore-tessere-linux/main/programs/CRSManager.run.sha256`

3. `sha256sum -c CRSManager.run.sha256`

L'output deve essere 

```
CRSManager.run: OK
```

Se risulta qualcosa di diverso occorre rieseguire il comando _wget_ del punto 1.

**Alternativamente si può scaricare il programma da questo repository:**

1. `wget -qc -O CRSManager.run https://github.com/micheleb26/Configurazione-lettore-tessere-linux/blob/main/programs/CRSManager.run?raw=true`

2. `wget -qc -O CRSManager.run.sha256 https://raw.githubusercontent.com/micheleb26/Configurazione-lettore-tessere-linux/main/programs/CRSManager.run.sha256`

3. `sha256sum -c CRSManager.run.sha256`

L'output deve essere 

```
CRSManager.run: OK
```

Se risulta qualcosa di diverso occorre rieseguire il comando _wget_ del punto 1.

Il file è sui 4.4MB (4,579,454 byte) in caso sia stato scaricato parzialmente rilanciare il comando wget.

Dare i permessi di esecuzione al file scaricato

`chmod +x CRSManager.run`

Eseguire l'installazione

`sudo ./CRSManager.run`

Avvio del CRS Manager da terminale

`crsLinux.sh`

La prima volta scarica i certificati, quando finisce dare CTSL+C e rilanciarlo.

Adesso opzionalmente si può procedere con la configurazione del [CRS Manager](./configurazione_crsmanager.md)

O con la [configurazione di firefox](./configurazione_firefox.md).

**Questo dovrebbe bastare**.

## In caso di problemi<a id="problemi"></a>

Riavviare il demone PC/SC

`sudo systemctl restart pcscd`

Se il problema non è risolto, provare ad installare le seguenti librerie una alla volta finché va:

Scaricare dal sito [sanita.finanze.it](https://sistemats1.sanita.finanze.it/portale/elenco-driver-cittadini-modalita-accesso) il pacchetto in base al proprio sistema operativo

**Oppure:**
> `wget -c https://swdownload1.agenziaentrate.gov.it/pub/sanita/libbit4xpki-idemia-amd64.1.4.10-622.deb`
> 
> _Modificare il comando wget in base alle esigenze._
> 
> `echo '9d622a0f1fc4499f4795eb86cc7a21e29902ada62c5c822049bab4939eed06d7  libbit4xpki-idemia-amd64.1.4.10-622.deb' > libbit4xpki-idemia-amd64.1.4.10-622.deb.sha256`
> 
> `sha256sum -c libbit4xpki-idemia-amd64.1.4.10-622.deb.sha256`
> 
> L'output deve essere:
> 
> `libbit4xpki-idemia-amd64.1.4.10-622.deb: OK`
> 
> o riscaricare il pacchetto.

ed installarlo tramite il comando

`sudo dpkg -i libbit4xpki-idemia-amd64.1.4.10-622.deb`

Questo pacchetto installa le librerire in /usr/lib/bit4id/ configurare il CRSManager in modo che punti alla libreria `/usr/lib/bit4id/libbit4opki.so`
Lo stesso vale se si vuole configurare Firefox.

In caso non funziona ancora provare ad installare le seguenti librerie:

`sudo apt install -y opensc-pkcs11`

`sudo apt install libpcsclite1`

`sudo apt install libnss3-tools`

`sudo apt install zlib1g-dev`

# Per cultura<a id="cultura"></a>

Nella tabella di seguito riporto (in forma non completa) le descrizioni dei pachetti nominati in questa guida, che siano necessari per il corretto funzionamento del lettore di tessere o meno.

| Pacchetto     | Descrizione                              |
|---------------|------------------------------------------|
| libccid       | Driver PC/SC per smartcard reader USB    |
| pcscd         | Middleware per accedere alle smartcard   |
| opensc        | Smartcard utilities compatibili PKCS#15  |
| pcsc-tool     | Strumenti da utilizzare con le smartcard |
| opensc-pkcs11 | Smartcard utilities compatibili PKCS#15  |
| libacsccid1   | Driver PC/SC per smartcard reader USB    |
| libpcsclite1  | Middleware                               |
| libnss3-tools | Network security service tools           |

# Riferimenti<a id="riferimenti"></a>
- [Carta azionale dei servizi e firma digitale](https://wiki.golem.linux.it/Carta_Nazionale_dei_Servizi_e_Firma_Digitale#Firma_digitale_FD)
- [Elenco driver cittadini modalità accesso](https://sistemats1.sanita.finanze.it/portale/elenco-driver-cittadini-modalita-accesso)
- [Software per TS-CNS](https://www.ariaspa.it/wps/portal/Aria/Home/DettaglioRedazionale/cosa--facciamo/innovazione-digitale/certificazione-digitale/software-cns)
- [Istruzioni per configurare i Driver delle TS-CNS
per sistemi operativi Linux](https://www.ariaspa.it/wps/wcm/connect/d44b3b70-1333-43d1-9af3-b6941f28be79/Istruzioni+per+configurare+i+Driver+delle+carte+su+Firefox+e+su+CRS+per+sistemi+operativi+Linux_v4.pdf?MOD=AJPERES&CACHEID=ROOTWORKSPACE-d44b3b70-1333-43d1-9af3-b6941f28be79-nCAjxHP)
- [Manuale di installazione e configurazione software CRS per Linux a 64bit](https://www.lispa.it/wps/wcm/connect/83e872ef-a750-47c1-b0c5-a608029bc8a2/Manuale+per+l%27installazione+e+la+configurazione+del+Software+CRS+per+Linux+64bit+v2.0.pdf?MOD=AJPERES&CONVERT_TO=URL&CACHEID=83e872ef-a750-47c1-b0c5-a608029bc8a2)
