<p align="center">
  <img src="readme-icon.svg" width="112" alt="ClaimBoard Scanner icon">
</p>

<h1 align="center">ClaimBoard Scanner</h1>

<p align="center">
  <a href="https://github.com/SebRoLENS/claim/releases/latest"><img src="https://img.shields.io/endpoint?url=https%3A%2F%2Fraw.githubusercontent.com%2FSebRoLENS%2Fclaim%2Fmain%2Fversion-badge.json" alt="Current version"></a>
</p>

[⬇️ Download latest signed APK](https://github.com/SebRoLENS/claim/releases/latest/download/ClaimBoard-Scanner-latest.apk)

Il badge della versione e il pulsante di download sono automatici: ogni nuova build firmata pubblicata come GitHub Release diventa la versione `latest`, senza dover modificare manualmente il README.

Applicazione Android per creare il resoconto degli acquisti effettuati tramite le risposte agli annunci della Bacheca di WhatsApp Business.

## Funzionamento

Durante una scansione guidata l’app riconosce:

- numero, titolo, prezzo minimo e prezzo massimo del lotto;
- nome WhatsApp, testo e orario delle risposte;
- `Claim`, `Mio` o `Max` come offerta al prezzo massimo;
- `Min` come offerta al prezzo minimo;
- un importo numerico come offerta intermedia.

Per ogni lotto vince l’offerta valida più alta; a parità viene scelta la prima risposta. Il riepilogo raggruppa gli acquisti per nome WhatsApp e calcola il totale di ogni cliente. Thread non acquisiti, messaggi eliminati, importi fuori intervallo e offerte ambigue restano evidenziati per il controllo.

## Uso

1. Installa l’APK. Se viene usata la stessa chiave di firma della versione precedente, l’APK può essere installato come aggiornamento.
2. Apri ClaimBoard Scanner e abilita **ClaimBoard – lettura guidata** nelle impostazioni Accessibilità.
3. Tocca **Nuovo evento e apri WhatsApp**.
4. Apri **Community → Bacheca** e apri il thread delle risposte del **primo lotto** dell’evento.
5. Torna alla Bacheca, raggiungi manualmente l’**ultimo lotto** e apri il suo thread delle risposte.
6. Da questo momento l’app scorre automaticamente i commenti, torna alla Bacheca, apre i lotti intermedi e continua fino al primo estremo.
7. Al termine torna nell’app, controlla le segnalazioni ed esporta il CSV.
8. Se un dato non è stato interpretato correttamente, usa **Salva log anonimo per GitHub** e allega il JSON a un [nuovo issue](https://github.com/SebRoLENS/claim/issues/new) descrivendo il risultato atteso.

## Log diagnostico anonimo

Il file esportato contiene la chat acquisita, l’interpretazione di ogni risposta, i vincitori e i totali calcolati, la sequenza delle azioni automatiche e — in caso di errore — una fotografia testuale dell’albero Accessibilità. Questo permette di riprodurre e correggere un’estrazione errata senza richiedere screenshot o dati grezzi.

I partecipanti diventano `Cliente_001`, `Cliente_002`, … e `Tu` diventa `Operatore`. Telefoni, email, URL, handle social, indirizzi IP, percorsi file e date assolute vengono rimossi; gli identificativi dei lotti, i prezzi e l’ordine delle offerte restano disponibili per la diagnosi. Il file non contiene la tabella inversa degli pseudonimi.

Il log grezzo rimane nell’archivio privato dell’app e non viene caricato automaticamente. Poiché i messaggi sono testo libero, controlla comunque il JSON prima di pubblicarlo su GitHub.

## Privacy e sicurezza

- nessun permesso Internet, contatti o notifiche;
- servizio Accessibilità limitato a `com.whatsapp.w4b`;
- scansione attiva solo dopo un comando esplicito;
- arresto automatico dopo due ore;
- dati conservati nell’archivio privato dell’app e cancellabili dall’utente.
- esportazione diagnostica esplicita e anonimizzata, senza mappa inversa dei partecipanti.

## Compilazione

Il progetto non richiede Gradle né dipendenze di terze parti. Servono JDK 17 e Android SDK Platform 35 con Build Tools 35.0.0. La pipeline GitHub legge automaticamente `android:versionName` dal manifest preparato per la build e usa quella versione per il nome dell'artifact e per il badge del README.

La pipeline produce sia l'APK non firmato sia la release ufficiale firmata. La chiave privata è conservata esclusivamente in **GitHub Actions Secrets**, non nel repository pubblico. Prima della pubblicazione la pipeline verifica il certificato di firma e pubblica sia l'APK con numero di versione sia `ClaimBoard-Scanner-latest.apk`. Il fingerprint del certificato è documentato in `SIGNING.md`.
