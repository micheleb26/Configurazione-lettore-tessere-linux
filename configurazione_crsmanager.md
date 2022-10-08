# Configurazione CRS Manager

### Descrizione

> _Configurazione provata su Linux Mint 21 LTS "Vanessa" con desktop XFCE 4.16_

Una volta installato il CRS Manager possiamo configurarlo.

## Creazione di un lanciatore

Tasto destro del mouse sul desktop e apparirà un menù come il seguente

<img title="a title" alt="Creazione lanciatore" src="/img/configurazione_crsmanager_01.png">

Selezionare quindi _Crea lanciatore_

<img title="a title" alt="Creazione lanciatore" src="/img/configurazione_crsmanager_02.png">

Indicare un nome a piacere, io ho inserito CRS Manager per praticità (il creatore riconosce già il comando e completa alcune parti del form)

inserire `/usr/bin/crsLinux.sh` in _Comando_.

Si può cliccare anche sull'icona e sceglierne una a piacere, io ho scelto quella acocmpagnata dal CRS Manager.

<img title="a title" alt="Creazione lanciatore" src="/img/configurazione_crsmanager_03.png">

Selezionare _Crea_ e apparirà l'icona del CRS Manager sul desktop.

## In caso di problemi con le librerie

In caso in cui il CRS Manager non veda il lettore di schede lo si può configurare.
Andare quindi in Modifica

<img title="a title" alt="Creazione lanciatore" src="/img/configurazione_crsmanager_05.png">

Indicare una libreria di driver, io ad esempio ho usato `/usr/lib/x86_64-linux-gnu/opensc-pkcs11.so`.

<img title="a title" alt="Creazione lanciatore" src="/img/configurazione_crsmanager_04.png">

---

**NOTE**

In caso di problemi e si è installato il pacchetto scaricato dal sito [sanita.finanze.it](https://sistemats1.sanita.finanze.it/portale/elenco-driver-cittadini-modalita-accesso) provare ad inserire il percorso: `/usr/lib/bit4id/libbit4opki.so`

---
