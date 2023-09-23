# Guida alla build di emception
In questo file verrà spiegato come effettuare la build della demo di emception. Nella repository è **già presente la demo buildata**, ma è *necessario* sapere quali passaggi sono necessari affinchè questa possa essere replicata su ogni dispositivo.


# Requisiti

La build è stata effettuata su macchina virtuale GNOME, ma può essere usata qualsiasi distro di Linux. Attualmente emception non funziona su Windows/MacOS.
Questi sono i requisiti minimi necessari alla build di sistema (da dover implementare su VirtualBox o, eventualmente, per qualsiasi computer.
- **50 GB di spazio** (fra sistema operativo e tentativi, Emception ve ne occuperà almeno 10)
- **16 GB minimi di RAM, ma sono consigliati 23GB**. La motivazione verrà spiegata nei passaggi successivi.
- La build impiegherà **diverso tempo**, quindi anche quello, ma di avere un occhio attento soprattutto attorno ai 2100 file buildati.

## Inizializzazione

I passaggi iniziali segnati sul readme di Emception sono corretti fino ad un certo punto. Riporto qui i passaggi necessari:
> git clone https://github.com/jprendes/emception.git
> git checkout [da323f9](https://github.com/jprendes/emception/commit/da323f97400492fcfdaef2dd7eaf3868f60c26b4)

Perchè usare questo commit? Come riportato [qui](https://github.com/jprendes/emception/issues/20) sembra essere attualmente l'unico commit funzionante. 
Dopo ciò, si consiglia altamente di eseguire i seguenti comandi per avere tutte le dipendenze aggiornate. Si consiglia inoltre di avere permessi di root per svolgere queste operazioni, altrimenti sarà inutile:
> sudo apt update
> sudo apt install nodejs
> sudo apt install npm
> sudo wget -qO /usr/local/bin/ninja.gz https://github.com/ninja-build/ninja/releases/latest/download/ninja-linux.zip
> sudo gunzip /usr/local/bin/ninja.gz
> sudo chmod a+x /usr/local/bin/ninja

Ora arriva la parte più importante. Nonostante possa sembrare un passaggio semplice, la parte non risiede di per sè nel comando, ma nell'accortezza dell'esecuzione.

>cd emception
>./build-with-docker.sh

Da qui, la build impiegherà circa **1 ora e mezza** fino a **3 ore**  per poter essere completata (dipende purtroppo dalle caratteristiche della Virtual Machine). Il passaggio più importante è quando raggiungerà il building [2156/2623]: se l'esito dovesse essere come segue...
> FAILED tools/Clang/lib/AST/CMakeFiles...
> [...]
> ... (received SIGKILL (-9))

La motivazione è data da un *overflow* di memoria. E' necessario dunque aggiungere altra memoria alla Virtual Machine. **(Secondo i requisiti qui sopra segnati)**.


## Demo

Una volta terminata l'esecuzione, è necessario installare la build per la demo. 
> pushd demo
npm install
npm run build

L'ultimo passaggio (nonchè l'unico **obbligatorio** per questa repository) è eseguire la demo.

> popd
npx serve build/demo

Se siete arrivati a questo punto senza alcun errore o problema, la demo vi fornirà un link statico a cui accedere per far partire l'IDE in browser. 
