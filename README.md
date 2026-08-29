# ClaimBoard Scanner

**Current version: 0.3.0**

[⬇️ Download ClaimBoard Scanner 0.3.0 APK](https://github.com/SebRoLENS/claim/actions/runs/33277374984/artifacts/9721917623)

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

## Privacy e sicurezza

- nessun permesso Internet, contatti o notifiche;
- servizio Accessibilità limitato a `com.whatsapp.w4b`;
- scansione attiva solo dopo un comando esplicito;
- arresto automatico dopo due ore;
- dati conservati nell’archivio privato dell’app e cancellabili dall’utente.

## Compilazione

Il progetto non richiede Gradle né dipendenze di terze parti. Servono JDK 17 e Android SDK Platform 35 con Build Tools 35.0.0. La compilazione pubblica produce un APK allineato non firmato; la chiave privata di release non viene mai salvata nel repository.

```bash
chmod +x build.sh verify.sh
./build.sh
./verify.sh
```

L’APK non firmato viene creato in `build/outputs/ClaimBoard-Scanner-0.3.0-aligned-unsigned.apk`. Se vengono fornite tramite variabili d’ambiente le credenziali di firma, `build.sh` produce anche `build/outputs/ClaimBoard-Scanner-0.3.0.apk`.

Il fingerprint del certificato è documentato in `SIGNING.md`.
