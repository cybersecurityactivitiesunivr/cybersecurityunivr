---
layout: default
title: Attacchi di Ingegneria sociale
description: Prof.ssa Federica Paci
---
# Attacchi di Ingegneria Sociale

L'ingegneria sociale è una tecnica di manipolazione psicologica utilizzata per indurre le persone a divulgare informazioni confidenziali, eseguire azioni che compromettano la sicurezza o rivelare dati sensibili. Questa tecnica si basa sull'interazione umana e sfrutta la fiducia, la curiosità, la paura o l'ignoranza delle vittime per ottenere accesso a informazioni o sistemi protetti.

Per questa attivita' utilizzeremo la macchina **Kali Linux** e il **Social Engineering Tookit (SET)** installato sulla macchina Kali Linux. 
SET  offre una vasta gamma di funzionalità per simulare attacchi di ingegneria sociale e valutare la resilienza di individui e organizzazioni contro tali attacchi. 

Prima di condurre gli attacchi di ingegneria sociale utilizzando SET dobbiamo installare sulla macchina Kali Linux il software **Mailhog**.

**Mailhog** è uno strumento di testing e sviluppo per le email. È un server SMTP simulato che cattura le email inviate dalle applicazioni in fase di sviluppo, consentendo agli sviluppatori di testare l'invio di email senza il rischio di inviare email reali a destinatari reali. MailHog fornisce un'interfaccia web semplice per visualizzare, cercare e gestire le email catturate.

## Installazione Mailhog

Scaricate sulla macchina Kali Linux il file MailHog_linux_amd64 dal seguente url https://github.com/mailhog/MailHog/releases/v1.0.0.

Salvate il file MailHog_linux_amd64 sotto la cartella Desktop.

Aprite un terminale e digitate i seguenti comandi per dare permessi di esecuzione al file:

```
# chmod +x MailHog_linux_amd64
```


## Creare un sito di phishing per rubare credenziali


Eseguite il Social Engineering Toolkit dal menu principale della macchina Kali come illustrato nella figura qui sotto.

![image](set1.png)

Selezionate l’opzione 1) Social Engineering Attacks

![image](set2.png)

Selezionate l' opzione 2) Website Attack Vector

![image](set3.png)

Selezionate l’opzione 3) Credential Harvester Attack Method

![image](set4.png)

Selezionare l’opzione 2 Site Cloner 

Specificare come indirizzo IP quello della macchina Kali Linux

Specificare URL del sito da clonare. Il sito deve avere una form di login

![image](set5.png)

Aprite Firefox e visitate il sito web digitando localhost nella barra degli indirizzi del browser e inserite un’ indirizzo email e una password fasulli

## Creare un eseguibile malevolo per Windows

Dal menù principale del Social Engineering Toolkit selezionare opzione 4) Website Attack Vector

Poi selezionare l'opzione Windows Shell Reverse TCP x64.

![image](payload.png)

Aprite un terminale e create un http server con il comando per trasferire il file sulla macchina della vittima.

```
python3 -m http.server 8888
```

## Creare Chiavetta USB infetta 

Dal menu' principale di SET selezionare l'opzione 3) Infectious Media Generator.

Poi Selezionare Opzione 1 – File Format Exploits

Specificare indirizzo IP della macchina Kali Linux 

Selezionare Opzione 13 – Adobe PDF Embedded Social Engineering

![image](usb1.png)

Selezionare Opzione 2 – Use built-in BLANK PDF for attack

Selezionare opzione 5 – Windows Meterpreter Reverse_TCP (x64)

Lasciare come indirizzo IP e porta di default

Copiare la cartella /root/.set/autorun su una chiavetta USB


## Creare un QRCode Malevolo 

Selezionare Opzione 8) QRCode Generator Attack Vector 

![image](qrcode1.png)

Specificare l'url del sito web di phishing a cui redirigere le potenziali vittime 

![image](qrcode2.png)

Aprite qrcode_attack.png con un QRCode scanner online e.g Web QR per vedere che il QRCode punta al sito malevolo


