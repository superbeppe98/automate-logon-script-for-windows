# Accensione, login automatico di un utente, avvio automatico di un programma e spegnimento automatico di un computer

## Accensione automatica
Per accendere un computer in automatico è possibile utilizzare la funzione ```Wake on Alarm```.

Per verificare se il tuo computer supporta tale funzione e per abilitarla, devi accedere al BIOS del tuo PC e seguire questi passi:

Accedi al BIOS del tuo computer durante la fase di avvio premendo il tasto F1 (o il tasto corrispondente indicato sullo schermo).
Naviga fino alla sezione ```Configurazione``` e seleziona ```Dispositivi PCI``` (nota: la funzione potrebbe essere disponibile all'interno di altri menù).
Seleziona ```RTC Alarm Date``` e imposta la data di accensione programmata.
Seleziona ```RTC Alarm Time``` e imposta l'ora di accensione programmata.
Salva le impostazioni e chiudi il BIOS.
Spegni il computer normalmente.
Aspetta fino all'ora impostata per l'accensione programmata e il tuo PC si accenderà automaticamente.

## Login di un utente senza inserire la password
Puoi effettuare il login automatico ad un utente attraverso una modifica del Registro di sistema. Segui questi passaggi: 
* Premi il tasto Windows + R per aprire la finestra di dialogo ```Esegui```
* Scrivi ```regedit``` e premi Invio per aprire il Registro di sistema
* Vai alla seguente chiave del Regisstro di sistema: ```HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon```
* Trova il valore ```DefaultUserName``` e assicurati che sia impostato sul nome utente dell'account che vuoi impostare per l'autenticazione automatica
* Se il valore ```DefaultUserName``` non esiste, crealo come tipo di valore REG_SZ e imposta il valore sul nome utente dell'account che vuoi impostare per l'autenticazione automatica
* Trova il valore ```DefaultPassword``` e assicurati che sia impostato sulla password dell'account utente che vuoi impostare per l'autenticazione automatica
* Se il valore ```DefaultPassword``` non esiste, crealo come tipo di valore REG_SZ e imposta il valore sulla password dell'account utente che vuoi impostare per l'autenticazione automatica
* Trova il valore ```AutoAdminLogon``` e imposta il valore su ```1``` per abilitare l'autenticazione automatica
* Chiudi il Registro di sistema e riavvia il computer per applicare le modifiche

## Avvio di un programma in automatico
Puoi utilizzare uno script PowerShell per avviare automaticamente una presentazione di PowerPoint in modalità presentazione. Ecco come:

```
$powerpoint = New-Object -ComObject PowerPoint.Application
$presentation = $powerpoint.Presentations.Open("C:\path\to\your\presentation.pptx")
$presentation.SlideShowSettings.Run()
```

Dovrai sostituire ```C:\path\to\your\presentation.pptx``` con il percorso completo del tuo file di presentazione PowerPoint. Puoi quindi salvare questo script come file .ps1.

Per eseguire lo script PowerShell attraverso l'utilità di pianificazione di Windows, puoi seguire questi passaggi:

* Crea il file di script PowerShell come descritto sopra.
* Apri il Task Scheduler (l'utilità di pianificazione di Windows) dal menu Start.
* Fai clic su ```Crea attività``` nella finestra del Task Scheduler.
* Nel campo ```Nome``` immetti un nome descrittivo per il task.
* Nella scheda ```Trigger```, specifica quando il task deve essere eseguito, ad esempio scegliendo una data e un'ora specifica o selezionando un evento di sistema.
* Nella scheda ```Azione```, fai clic su ```Nuova``` e seleziona ```Avvia un programma``` come tipo di azione.
* Nel campo ```Programma/script```, immetti il percorso completo del comando PowerShell.exe. Ad esempio, ```C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe```.
* Nel campo ```Argomenti```, immetti il percorso completo del tuo file di script PowerShell. Ad esempio, ```C:\path\to\your\powershell\script.ps1```.
* Fai clic su ```OK``` per salvare il task.
In questo modo, il Task Scheduler eseguirà lo script PowerShell al momento specificato.
* Potresti dover modificare le impostazioni di sicurezza del Task Scheduler per consentire l'esecuzione di script PowerShell, se non l'hai già fatto.Ad esempio, ```-ExecutionPolicy Bypass -File "C:\path\to\your\powershell\script.ps1```


## Spegnimento automatico di un computer
Puoi seguire questi passaggi per creare un'attività di pianificazione per lo spegnimento del PC:

* Apri il ```Pannello di controllo``` di Windows e seleziona ```Strumenti di amministrazione``` > ```Attività pianificate```.
* Nella finestra di ```Attività pianificate```, seleziona ```Crea attività``` dal menu laterale.
* Nella finestra di creazione dell'attività, nella scheda ```Generale```, assegna un nome all'attività (ad esempio, ```Spegnimento PC ogni Venerdì```).
* Nella scheda ```Attivazione```, seleziona ```Settimanale``` e poi seleziona il giorno della settimana desiderato (in questo caso ```Venerdì```).
* Inserisci l'ora esatta in cui desideri che il PC si spenga nel campo ```Attiva```. Ad esempio, inserisci ```19:00``` per spegnere il PC ogni venerdì alle 19.
* Nella scheda ```Azione```, seleziona ```Avvia un programma```. Nel campo ```Programma/script``` immetti ```C:\Windows\System32\shutdown.exe``` e nel campo ```Argomenti``` inserisci il seguente testo: ```-s -t 00``` (senza virgolette). Questi comandi inviano una richiesta di spegnimento al sistema operativo al momento stabilito.
* Fai clic su ```OK``` per creare l'attività di pianificazione.

