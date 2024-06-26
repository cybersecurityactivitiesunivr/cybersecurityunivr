---
layout: default
title: Attacchi ai sistemi di autenticazione basati su password
description: Prof.ssa Federica Paci
---

# Attacchi offline 
## Dictionary attack – documento pdf protetto da password

Eseguiremo un dictionary attack per scoprire la password del documento confidential.pdf.  L’hash della password che protegge l’accesso al documento è memorizzato nei metadati del documento. Per estrarre l’hash della password usiamo il tool pdf2john.pl di John The Ripper

Aprite un terminale digitate i seguenti comandi
```
# cd <path alla cartella dove avete scompattato il password.zip>
# pdf2john confidential.pdf
```
Il comando restituirà il seguente valore

```
confidential.pdf:$pdf$4*4*128*-4*1*16*be67ac70a35391f5b6716bfe7c30af81*32*4f185e9a05c20bf7eb9aceea2d1e3a7d00000000000000000000000000000000*32*a6454eaef509a12ad3f3d3caaafe8acd835b0be4f56ceb5ac5dc733d9b838a4f
```
Dove l’hash della password è:
```
$pdf$4*4*128*-4*1*16*be67ac70a35391f5b6716bfe7c30af81*32*4f185e9a05c20bf7eb9aceea2d1e3a7d00000000000000000000000000000000*32*a6454eaef509a12ad3f3d3caaafe8acd835b0be4f56ceb5ac5dc733d9b838a4f
```
Per recuperare la password in chiaro utilizzeremo hashcat con il seguente comando
```
hashcat -m 10500 -a 0 '$pdf$4*4*128*-4*1*16*be67ac70a35391f5b6716bfe7c30af81*32*4f185e9a05c20bf7eb9aceea2d1e3a7d00000000000000000000000000000000*32*a6454eaef509a12ad3f3d3caaafe8acd835b0be4f56ceb5ac5dc733d9b838a4f' dictionary.txt
```
dove 
*	-m 10500 indica la tipologia dell’hash utilizzato per proteggere la password
*	-a 0 indica la tipologia di attacco che in questo caso è un dictionary attack
*	‘password’ è l’hash della password da recuperare
*	dictionary.txt è il dizionario che viene utilizzato per recuperare la password
 

## Dictionary attack – Cracking MD5 password hashes 

Eseguiremo un dictionary attack per scoprire le password presenti nel file hashes.txt contenuto nella cartella hashcat. Il file contiene 9 MD5 hashes

Dal terminale digitate il seguente comando
```
hashcat -m 0 -a 0 hashes.txt  dictionary.txt
```
* -m 0 indica la tipologia dell’hash MD5
  
Per consentire di recuperare le altre password, eseguiremo un dictionary attack dove alle parole del dizionario applicheremo delle regole supportate da hashcat per rappresentare  patterns utilizzati dagli utenti nel formulare le loro passwords.

Utilizzeremo la regola leapspeak.rule che si trova sotto la cartella /usr/share/hashcat/rules/leetspeak.rule. Questa regola va a sostituire le lettere che compongono le parole nel dizionario con simboli o numeri. Per esempio la parola password applicando questa regola può diventare “p455w0rd”, “p@5sw0rd”, “passw0rd”.

Per applicare la regola alle parole contenute nel dizionario dictionary.txt eseguiamo il seguente comando:
```
hashcat -m 0 -a 0 -r /usr/share/hashcat/rules/leetspeak.rule hashes.txt  dictionary.txt
```
Per consentire di recuperare le altre password, eseguiremo un dictionary attack applicando una maschera che rappresenta il pattern dove l’utente aggiunge dei numeri alla fine della password quali per esempio john22 o john2022.

Per applicare la maschera alle parole contenute nel dizionario dictionary.txt eseguiamo il seguente comando:
```
hashcat -m 0 -a 6 hashes.txt  dictionary.txt ?d?d?d?d
```
 
## A –  John The Ripper

Eseguiremo brute force e dictionary attacks per scoprire le password presenti nel file sensitive.txt contenuto nel file password.zip. Il file contiene 22 MD5 hashes. Utilizzeremo il tool John The Ripper. Iniziamo a condurre un brute force attack
Dal terminale digitate i seguenti comandi:
```
john --incremental sensitive.txt
```
Per consentire di recuperare le altre password, eseguiremo un dictionary attack con il dizionario di John The Ripper che si trova sotto la cartella /usr/share/john/password.lst. Digitate il seguente comando:
```
john --wordlist=/usr/share/john/password.lst sensitive.txt
```

Ripetete il dictionary attack utilizzando i dizionari che si trovano sotto la cartella cain.txt  facebook-pastebay.txt  hotmail.txt  myspace.txt.

## Dictionary attacks - Cracking 
Eseguiremi una serie di dictionary attacks per scoprire le password presenti nei file passwd e shadow  che contengono gli username e gli hash delle password degli utenti che hanno accesso alla macchina Metasploitable2. 
•	Per ottenere una copia dei file passwd e shadow dobbiamo ottenere una shell sulla macchina Metasploitable2 utilizzando la vulnerabilità presente in vsftp come abbiamo visto nel laboratorio su tecniche di reconnaissance e esploitation.
•	Una volta ottenuta la shell utilizzate il comando cat /etc/passwd per visualizzare  il contenuto del file. Copiate il contenuto in un file di testo locale chiamato passwd.txt.
•	Poi utilizzate il comando cat /etc/shadow per visualizzare  il contenuto del file. Copiate il contenuto in un file di testo locale chiamato shadow.txt.
•	Da terminale digitate il seguente comando per combinare i due file passwd e shadow in un unico file passwords.txt
unshadow passwd.txt shadow.txt > passwords.txt
•	Eseguiremo una serie di dictionary attacks con i dizionari che si trovano sotto la cartella john: cain.txt  facebook-pastebay.txt  hotmail.txt  myspace.txt. Digitate il seguente comando
john –wordlist=<dizionario sotto la cartella john> passwords.txt

Quali password siete riusciti a recuperare?
 

# Online Attacks with Hydra

•	Per questo attacco vi serviranno sia la macchina Kali Linux che la macchina Metasploitable2 dove è installata l’applicazione web di cui trovare la password DVWA. Utilizzeremo anche BurpSuite per capire quali parametri vengono passati all’applicazione durante la fase di autenticazione.
•	L’obiettivo dell’attacco è trovare la password di amministratore per accedere all’applicazione DVWA
•	Fate partire entrambe le macchine e assicurative che tra le macchine ci sia una rete NAT.
•	Quando fate partire la macchina su cui è installata DVWA  vi chiederà uno username e password. Specificate msfadmin come username e come password msfadmin
•	Da riga di comando eseguite il comando ifconfig per determinare l’indirizzo IP della macchina Metasploitable2
•	Aprite un terminale sulla macchina Kali ed eseguite il seguente comando per controllare che la macchina su cui è installata DVWA è raggiungibile:

ping <INDIRIZZO IP METASPLOITABLE2>

•	Aprite il browser sulla macchina Kali e navigate all’URL http://<INDIRIZZO IP METASPLOITABLE2>
•	Dobbiamo configurare il browser per usare Burp Suite come proxy per intercettare la richiesta POST fatta all’applicazione quando un utente tenta di fare il login
•	Andate sulle Preferenze del browser e cliccate su Network Settings in fondo alla pagina delle preferenze come illustrato nella figura qui sotto

 


•	Selezionate Manual proxy configuration e sia per il protocollo http che https specificate come indirizzo 127.0.0.1 e come porta 8080 e poi cliccate OK in fondo.
 
•	Aprite Burpsuite e accettate i termini e le condizioni per il servizio come illustrato nella figura qui sotto
 

•	Quando si presenta la seguente interfaccia cliccate Next 

•	 












•	Cliccate Start Burp come illustrato nella figura qui sotto
 

•	Cliccate su Proxy 

 





•	Se Intercept is on è evidenziato come illustrato nella figura qui sotto allora Burp Suite sta funzionando correttamente

 

•	Tornate sulla pagina di login di DVWA e provato a fare login

 





•	Burp Suite ha intercettato la POST request. Potete vedere che ci sono 3 parametri: username, password e Login che è l'azione che viene eseguita.
 
•	Aprite un terminale sulla macchina Kali e digitate il seguente comando
hydra -V -l admin -P /usr/share/john/password.lst <INDIRIZZO IP METASPLOITABLE2) http-post-form "/dvwa/login.php:username=^USER^&password=^PASS^&Login=Login:Login Failed"

                   dove 
	L’opzione -V indica la modalità verbose dove ogni password provata verrà stampata a video
	-l indica lo username di cui recuperare la password
	-P indica il dizionario da utilizzare per recuperare la password
	 indica l’indirizzo IP del target da attaccare in questo caso la macchina Metasploitable2
	http-post-form indica che l’applicazione accetta richieste POST
	l’ultimo parametro indica l’URL della pagina di login e i parametri passati alla pagina di login che avevamo intercettato con Burp Suite

•	Ora proviamo a recuperare la password  dell’account istheory necessaria per accedere alla seguente wiki disponibile online: https://is.theorizeit.org. Visitate la pagina https://is.theorizeit.org/auth. Vedete che richiede uno username e una password. 
•	Per fare questo utilizzeremo il dizionario rockyou.txt che si trova sotto la cartella /usr/share/wordlists che contiene circa 32 milioni di password
•	Dobbiamo innanzitutto decomprimere rockyou digitando dal terminale della macchina Kali Linux i seguenti comandi: 
	cd /usr/share/wordlists
	sudo gunzip /usr/share/wordlists/rockyou.txt.gz

•	Sempre dallo stesso terminale digitate il seguente comando per trovare la password associata all’account istheory

hydra -V -l istheory -P /usr/share/wordlists/rockyou.txt https-get://is.theorizeit.org/auth/

Online Dictionary Attacks with Metasploit

•	Dobbiamo recuperare la password degli account root,  admin e user utilizzati per collegarsi alla applicazione myPhPAdmin sulla macchina Metasploitable2.

•	Creaiamo il file /tmp/users.txt gli utenti di cui recuperare la password e il file /tmp/passwords.txt 

 


















•	Facciamo partire la console di Metasploit  con il comando msfconsole e poi cerchiamo il modulo di Metasploit che implementa un online dictionary attack verso l’applicazione myPhPAdmin:

 

•	Selezioniamo l’opzione 1 e specifichiamo i vari parametri:
 
•	Dopo pochi secondi otterremo le password desiderate:
![image](https://github.com/cybersecurityactivitiesunivr/cybersecurityunivr/assets/173290227/555a81fd-e345-4008-9bbb-63ce1164eef9)

