---
layout: default
title: Tecniche di anonimizzazione
description: Prof.ssa Federica Paci
---

In questo laboratorio utilizzeremo **Amnesia** e **ARX**, due software open-source per anonimizzare il contenuto di diversi dataset. 

**Amnesia** è un software open-source progettato per anonimizzare i dati sensibili, in particolare dataset contenenti informazioni personali. Il tool consente di applicare tecniche di anonimizzazione come la generalizzazione e la randomizzazione per ridurre il rischio di re-identificazione degli individui, preservando al contempo l'utilità dei dati. Amnesia supporta l'approccio di k-anonymity, che assicura che ogni individuo nel dataset anonimo non possa essere distinto da almeno altri k individui, rendendo più difficile collegare i dati a una persona specifica.

Il software è particolarmente utile per garantire la conformità con normative sulla privacy, come il GDPR, ed è utilizzabile sia tramite una interfaccia web che in modalità desktop per gestire dati sensibili con maggiore sicurezza.

**ARX** è un potente strumento open-source per l'anonimizzazione dei dati. È progettato per proteggere la privacy dei dati sensibili attraverso tecniche avanzate come k-anonymity, l-diversity, e t-closeness. ARX permette di applicare trasformazioni di generalizzazione e soppressione ai dataset, bilanciando la protezione della privacy con la qualità dei dati.

Lo strumento fornisce una piattaforma flessibile che supporta un'ampia gamma di scenari di anonimizzazione, rendendolo utile per garantire la conformità a normative come il GDPR. Inoltre, ARX offre funzionalità di analisi dei rischi per valutare il livello di protezione raggiunto dopo l'anonimizzazione, aiutando a prevenire la re-identificazione degli individui.

È utilizzato in vari settori, come la sanità, le ricerche di mercato e i servizi pubblici, per garantire la privacy dei dati durante la condivisione e l'analisi.

Prima di iniziare il laboratorio, Amnesia e ARX devono essere installati sulla macchina **Kali Linux** e i seguenti file devono essere salvati ed estratti sotto la cartella Desktop: [Databases](Databases.zip), [Hierarchies](IcdCodesPredefinedHierarchies.zip), [Project](example.deid).
