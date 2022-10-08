# Configurare il lettore tessere in Linux

### Descrizione

> _Configurazione provata su Linux Mint 21 LTS "Vanessa"_

## Comandi

Collegare il lettore e inserire la tessera sanitaria:

Aggiornare il sistema operativo

`sudo apt update && sudo apt upgrade -y`

Installare le librerie, gli strumenti e il middleware

`sudo apt install -y libccid pcscd opensc libacsccid1 pcsc-tools`

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

`sudo systemctl restart pcscd`

`pcsc_scan # test funzionamento lettore`
