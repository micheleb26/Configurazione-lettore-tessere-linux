# Configurazione di Firefox per leggere le tessere

### Descrizione

> _Configurazione provata su Linux Mint 21 LTS "Vanessa" con Mozilla Firefox 105.0.2 (64-bit)_
Uso la verisone in inglese quindi le voci potrebbero essere leggermente diverse.

## Configurazione di Firefox

### Passo 1

Andare sul menù (il bottone in alto a destra con le tre linee orizzontali [in gergo hamburger]) e selezionare _Impostazioni_
Oppure digitare sulla barra degli indirizzi about:preferences#privacy per fare prima e saltare il passo 2

<img title="a title" alt="Creazione lanciatore" src="/img/configurazione_firefox_01.png">

### Passo 2
Selezionare la voce _Privacy & sicurezza_

<img title="a title" alt="Creazione lanciatore" src="/img/configurazione_firefox_02.png">

### Passo 3

Scendere fino a Certificati e cliccare sul bottone _Dispositivi di sicurezza_, si aprirà la seguente finestra:

<img title="a title" alt="Creazione lanciatore" src="/img/configurazione_firefox_03.png">

### Passo 4

Selezionare la voce _NSS Internal PKCS # 11Module_ e cliccare sul mottone _Carica_

<img title="a title" alt="Creazione lanciatore" src="/img/configurazione_firefox_04.png">

Indicare un nome significativo a scelta
Indicare il percorso della libreria del lettore, nel mio caso `/usr/lib/x86_84-linux-gnu/opensc-pkcs11.so` e dare _OK_

### Passo 5

Eseguire il login inserendo in PIN della tessera sanitaria

<img title="a title" alt="Creazione lanciatore" src="/img/configurazione_firefox_05.png">
