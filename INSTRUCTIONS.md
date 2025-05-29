# Guida per l'Avvio del Progetto Real Time Chatbot

Questa guida ti fornirà tutti i passaggi necessari per avviare il progetto React in totale funzionalità, inclusa la configurazione delle variabili d'ambiente e l'installazione delle dipendenze.

-----

## Prerequisiti

Per iniziare, assicurati di avere installato sul tuo sistema:

  * **Node.js**: **Versione 20 o superiore**. Puoi scaricare l'ultima versione stabile dal sito ufficiale di Node.js: [nodejs.org](https://nodejs.org/).

-----

## Configurazione delle Variabili d'Ambiente

Per il corretto funzionamento dell'applicazione React, è fondamentale configurare alcune variabili d'ambiente. Queste verranno lette dall'applicazione e usate per connettersi ai servizi esterni.

Crea un file chiamato `.env` nella **directory principale del tuo progetto React** (se non esiste già). All'interno di questo file, aggiungi le seguenti righe:

```
OPENAI_API_KEY=la_tua_chiave_api_openai
REACT_APP_LOCAL_RELAY_SERVER_URL=http://localhost:8081
REACT_APP_LANGFUSE_HOST=https://langfuse.requrv.ai
REACT_APP_LANGFUSE_PUBLIC_KEY=la_tua_chiave_pubblica_langfuse
REACT_APP_LANGFUSE_SECRET_KEY=la_tua_chiave_segreta_langfuse
```

**Spiegazione delle Variabili:**

  * `OPENAI_API_KEY`: Questa è la tua chiave API personale per accedere ai servizi di OpenAI. Puoi ottenerla o crearne una nuova dalla [dashboard di OpenAI](https://platform.openai.com/account/api-keys). **Ricorda di mantenerla segreta\!**
  * `REACT_APP_LOCAL_RELAY_SERVER_URL`: Specifica l'URL del server relay locale che verrà eseguito sulla porta `8081`. Questo è essenziale per la comunicazione interna dell'applicazione.
  * `REACT_APP_LANGFUSE_HOST`: L'URL base della tua istanza Langfuse, che in questo caso è `https://langfuse.requrv.ai`.
  * `REACT_APP_LANGFUSE_PUBLIC_KEY` e `REACT_APP_LANGFUSE_SECRET_KEY`: Queste chiavi sono necessarie per autenticarsi e inviare dati alla tua istanza Langfuse. Le puoi ottenere direttamente dall'interfaccia di Langfuse (`https://langfuse.requrv.ai`) navigando nelle impostazioni del tuo progetto. **Sono cruciali per il tracciamento e il testing dei prompt.**

-----

## Installazione delle Dipendenze

Una volta configurato il file `.env`, è il momento di installare tutte le librerie e i pacchetti necessari al progetto React.

Apri il terminale, naviga nella **directory principale del tuo progetto React** e esegui il seguente comando:

```bash
npm install
```

Questo comando scaricherà e installerà tutte le dipendenze elencate nel file `package.json` del tuo progetto.

-----

## Avvio del Progetto

Ora sei pronto per avviare l'applicazione. Dovrai eseguire due comandi separati in terminali diversi, in quanto il progetto prevede un server relay e l'applicazione React stessa.

1.  **Avvia il server relay locale:**
    Apri il **primo terminale**, naviga nella directory principale del progetto ed esegui:

    ```bash
    npm run relay
    ```

    Questo comando avvierà il server relay che gestisce la comunicazione con i servizi esterni (come OpenAI, tramite Langfuse). Lascia questo terminale aperto e in esecuzione.

2.  **Avvia l'applicazione frontend React:**
    Apri un **secondo terminale**, naviga nella stessa directory principale del progetto ed esegui:

    ```bash
    npm run start
    ```

    Questo comando avvierà l'applicazione di sviluppo React. Una volta compilata, l'applicazione si aprirà automaticamente nel tuo browser predefinito, solitamente all'indirizzo `http://localhost:3000`. Se non si apre automaticamente, puoi accedervi manualmente tramite questo URL.

-----

## Testing del Prompt "real-time-chatbot"

Il progetto è configurato per utilizzare il prompt "**real-time-chatbot**". Puoi visualizzare, modificare e testare questo prompt direttamente dall'interfaccia Langfuse.

Accedi a `https://langfuse.requrv.ai` con le tue credenziali. Una volta dentro, naviga nella sezione "Prompts" per trovare e gestire il prompt "real-time-chatbot". Qualsiasi modifica tu apporti lì sarà riflessa nell'applicazione quando comunicherà con Langfuse.

-----

## Risoluzione dei Problemi Comuni

  * **`npm install` fallisce:** Assicurati di avere una connessione internet stabile. Se persistono problemi, prova a pulire la cache di npm con `npm cache clean --force` e riprova `npm install`.
  * **Variabili d'ambiente non caricate:** Controlla che il file `.env` sia nella **root del tuo progetto React** e che le variabili siano scritte esattamente come indicato, senza spazi extra o errori di battitura. Dopo aver modificato il file `.env`, devi **riavviare entrambi i processi (`npm run relay` e `npm run start`)** per far sì che le nuove variabili vengano caricate.
  * **Errore "Cannot GET /" o pagina bianca:** Se l'applicazione React non si carica correttamente, controlla i log di errore nel terminale dove hai eseguito `npm run start`. Assicurati che il server relay sia in esecuzione correttamente e che non ci siano errori di connessione tra l'applicazione React e il server relay.
  * **Connessione a Langfuse fallisce:** Verifica che le tue `REACT_APP_LANGFUSE_PUBLIC_KEY` e `REACT_APP_LANGFUSE_SECRET_KEY` siano corrette e che non ci siano restrizioni di rete che impediscano la connessione a `https://langfuse.requrv.ai`.