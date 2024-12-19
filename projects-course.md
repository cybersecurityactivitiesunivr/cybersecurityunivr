---
layout: default
title: Progetti - Cyber Security e Protezione dei Dati
description: Prof.ssa Federica Paci
---
Questa pagina e' dedicata ai progetti per sostenere l'esame del corso di Cyber sicurezza e Protezione dei Dati. I progetti possono essere svolti in gruppo costituito al massimo da 2 studenti.

## Auditing di Tecnologie di Tracciamento 
Le tecnologie di tracciamento sono strumenti e metodi utilizzati per monitorare e analizzare il comportamento degli utenti su piattaforme digitali. Queste tecnologie sono fondamentali per personalizzare l’esperienza dell’utente, migliorare le prestazioni dei siti web e supportare strategie di marketing mirato. Tuttavia, l’uso di tali strumenti solleva importanti questioni legate alla privacy, soprattutto in relazione al Regolamento Generale sulla Protezione dei Dati (GDPR), che disciplina il trattamento dei dati personali nell’Unione Europea.

Un esempio comune di tecnologia di tracciamento sono i **cookie**, piccoli file di testo memorizzati sul dispositivo dell’utente per registrare informazioni come le preferenze di navigazione o le credenziali di accesso. Secondo il GDPR, è necessario ottenere un consenso esplicito e informato per l’uso di cookie non essenziali, come quelli per scopi pubblicitari o di tracciamento di terze parti. 

I **web beacon** o **tracking pixel** sono immagini invisibili integrate in email o pagine web che raccolgono informazioni come l’indirizzo IP, il tipo di dispositivo e le interazioni dell’utente.  

Un’altra tecnologia sofisticata è il **device fingerprinting**, che raccoglie caratteristiche uniche del dispositivo dell’utente, come il sistema operativo, il browser e la risoluzione dello schermo, per creare un’identità persistente. 

Anche le piattaforme di social media utilizzano tecnologie di tracciamento integrate, come il Facebook Pixel, per monitorare le interazioni degli utenti su e fuori dalla piattaforma. 

Queste tecnologie di tracciamento sono in contrasto con i principi fondamentali del GDPR, come il consenso esplicito, la trasparenza, la minimizzazione dei dati e la limitazione delle finalità. 

Questo progetto si focalizza sull'analisi delle tecnologie di tracciamento adottate da siti web. Gli studenti riceveranno una lista di 30 siti di cui 15 siti americani e 15 siti web europeri da analizzare. Le tecnologie di tracciamento utilizzate devono essere analizzate in 3 diversi scenari: quando l'utente non fa nessuna scelta sull'essere tracciato (**nessuna scelta**), quando nega il consenso ad essere tracciato (**consenso negato**) e quando autorizza il consenso ad essere tracciato (**consenso accettato**). Per effettuare l'analisi verra' utilizzato il Website Auditing Tool di EDPB. Il tool e' scaricabile dal seguente link: https://code.europa.eu/edpb/website-auditing-tool/-/releases. Il Website Auditing Tool effettua la scansione del sito ed e' in grado di rilevare diverse tecnologie di tracciamento quali ad esempio cookies, browser fingerprinting, e beacons. Per ciascuna tecnologia di tracciamento rilevata, il tool consente di scaricare i dati raccolti in diversi formati quali json, excel, pdf, e word. Per ciascun sito analizzato, ci dovranno essere 3 file excel per ciascuna tecnologia di tracciamento rilevata dal tool - cookies, local storage, traffic analysis, e beacons - ciascuno corrispondente alle tre condizioni **nessuna scelta**, **consenso negato**, e **consenso accettato**.

Il report del progetto dovra' confrontare le principali tecnologie di tracciamento adottate nelle tre condizioni **nessuna scelta**, **consenso negato**, e **consenso accettato** dai siti americani e quelli europei. 

## Phishing - Creazione di Allegato Word Malevolo

L'obiettivo di questo progetto è quello di realizzare un documento Word malevolo che contiene una macro VBA, che installa un information stealer che ruba file contenenti informazioni sensitive dalla macchina delle vittime. La macro si connette a Dropbox e scarica un'immagine in cui e' stato codificato l'indirizzo IP del server C2 da cui scaricare l'information stealer. Dopo di che scarica dal server C2 e lo lancia. L'information stealer dovra' inviare i file con le informazioni sensitive al server C2. Il codice della macro deve essere offuscato. 

Il report per presentare il progetto dovra' contenere le seguenti sottosezioni: 1) creazione immagine: in questa sezione dovete spiegare come avete codificato l'indirizzo IP del server C2 nell'immagine; 2) Macro VBA: questa sezione dovete presentare il codice della macro prima che venga offuscato, le tecniche adottate per offuscare il codice e il codice della macro offuscato; 3) infrastruttura attacco: in questa sezione dovete presentare le macchine virtuali utilizzate per condurre l’attacco e come sono state configurate. 

Durante l'esame orale gli studenti dovranno dimostrare che il documento malevolo scarica l'information stealer su una macchina Windows e che manda i file al server C2. Per la dimostrazione verranno utilizzate due macchine virtuali: una macchina che simula la macchina dell'attaccante dove e' ospitato il server C2 e una macchina Windows che è il target dell'attacco.

## Sfruttamento Vulnerabilita' Shellshock

L'obiettivo di questo progetto e' quello di condurre un attacco multi-stage sfruttando la vulnerabilita' Shellshock (CVE-2014-6271). La vulnerabilità Shellshock (o Bashdoor) è un grave problema di sicurezza scoperto nel 2014 che affliggeva il software Bash (Bourne Again Shell), una shell di comando molto diffusa in sistemi operativi basati su Unix, come Linux e macOS. 

Shellshock sfrutta una debolezza nel modo in cui Bash gestisce le variabili d'ambiente. In Bash, le variabili d'ambiente possono contenere funzioni (frammenti di codice), e la vulnerabilità permette l'esecuzione di codice arbitrario iniettato attraverso variabili d'ambiente appositamente create.

Un attaccante può utilizzare questa vulnerabilità per eseguire comandi arbitrari sul sistema vittima, ottenendo potenzialmente il controllo completo del sistema.

**Stage 1**: L'attaccante sfrutta la vulnerabilita' Shellshock per accedere ad macchina Linux vulnerabile (**Host 1**). 

**Stage 2**:  L'attaccante cerca altri host raggiungibili e trova una seconda macchina (**Host 2**) a cui accede sfruttando una vulnerabilita' presente nella macchina e.g ssh.

**Stage 3**: L'attaccante fa una copia dei file /etc/passwd e /etc/shadow presenti su **Host 2**  e li comprime in un file .tar chiamato **sensitive_data**.

**Stage 4** L'attaccante esegue il comando scp su **Host 1** per scaricare **sensitive_data** da **Host 2**

**Stage 5** L'attaccante esegue curl su **Host 1** per inviare alla macchina dell'attaccante il file **sensitive_data**.

Il report del progetto deve avere una sottosezione per ogni stage dell'attacco dove viene spiegato come la fase dell'attacco e' stata eseguita e come sono configurate le macchine dell'attaccante, **Host 1** e **Host 2**.

Durante l'esame orale gli studenti dovranno dimostrare le fasi dell'attacco. Per la dimostrazione verranno utilizzate tre macchine virtuali: una macchina Linux che simula la macchina dell'attaccante, la macchina **Host 1** vulnerabile a Shellshock (https://www.vulnhub.com/entry/pentester-lab-cve-2014-6271-shellshock,104/) e la macchina **Host 2** Metasploitable2 (https://sourceforge.net/projects/metasploitable/).



