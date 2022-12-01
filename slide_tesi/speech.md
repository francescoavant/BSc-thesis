## Intro
Il lavoro di tesi si è basato sullo studio e lo sviluppo di connettori di scraping da sorgenti social network, in particolare da Facebook ed Instagram e la loro gestione per la successiva ingestione in sistemi di Big Data Analytics.
Il fine del progetto è l'estrazione massiva dei dati dai social, in modo da successivamente porli in sistemi di analisi.

## Attività svolta
L'attività svolta è consistita principalmente nello studio dello stato dell'arte dell'attività di scraping dai social network. Si è poi posta l'attenzione sui metodi attuati dalle piattaforme per contrastare l'attività di estrazione dei dati.
Successivamente è iniziata la fase di sviluppo sia per i connettori (in totale due, uno per facebook ed uno per instagram) sia per la creazione di metodi di elusione dei controlli attuati.


## Web Scraping
Il web scraping rappresenta l'attività di estrazione automatica di dati dal web.
Il termine inglese "scraping" significa letteralmente "raschiare" ed applicato nel contesto informatico, ciò fa riferimento al "prelevare tutte le informazioni da internet".

La sua funzionalità di differenzia a seconda dell'obiettivo, ovvero:
* alcuni provider mettono a disposizione delle Application Programming Interface per consentire l'estrazione di informazioni, questo in realtà accade anche per alcuni social network, però rappresenta una soluzione molto limitante in quanto la stessa ha delle soglie numeriche sui dati da estrarre e sulla sua funzionalità in generale. 
* l'effettiva estrazione avviene attraverso richieste HTTP di tipologia GET
* esistono anche tecniche dedicate

## Aspetti legali ed uso dei dati
Il web scraping rientra in un "zona grigia" della legalità in quanti questa attività non viene espressamente definita come non lecita da alcuna norma nazionale o internazionale. 

Sia nel GDPR europeo che nel CFAA americano, si fa riferimento in generale al trattamento dei dati, senza però identificare strumenti automatici di estrazione degli stessi. Diversi casi legali hanno individuato l'attività in sè come consentita, diversamente invece dell'utilizzo di questi dati. 

Esempi di fama internazionale sono il caso di Cambdridge Analytica e Facebook, oppure Linkedin e l'azienza hiQLabs.

I termini di servizio rappresentano le "regole" imposte dai servizi per il loro utilizzo. Ad esempio, i social di meta oggetto di studio in questo lavoro di tesi, vietano espressamente all'interno del file robots.txt (file tecnico che descrive le azioni consentite) lo scraping. 

L'impiego dei dati può appartenere a molteplici campi d'azione. I principali individuati nel lavoro di tesi appartengono ad usi investigativi, ovvero l'utilzzo dei connettori in azioni di Open Source Intelligence (analisi delle fonti aperte) e ad esempio ad applicazioni sul contrasto della radicalizzazione e del terrorismo online.

## Connettori sviluppati
I connettori sviluppati basano il loro funzionamento su due tool open source, rispettivamente per Facebook, facebook-scraper e per Instagram, instaloader.
Entrambi i tool non impiegano API ufficiali, perchè come detto prima, le stesse risultano avere carattistiche e regole molto stringenti.

Il sistemi ideale di implementazione dei connettori comprende anche le azioni di analisi e visualizzazione dati, le quali portano di conseguenza al filtraggio e all'output con decisioni finali.

## Estrazione dei dati
Le informazioni che i connettori sono in grado di estrarre sono simili sia per Facebook che per Instagram. Le principali differenze sono basate sulle carattistiche e funzionalità dei social stessi, come le storie, i follower, le pagine ed i gruppi.

I dati estratti sono eterogenei. I tool consentono l'estrazione di file JSON (formato leggibile da macchine e da umani), di file multimediali in vari formati sia foto che video e file di testo. 

Per ogni singola estrazione riferita ad un utente definito "target" (obiettivo) si è prevista sia la denominazione con UUID (universal unique identifier, un identificatore univoco per i file) e la funzione di zip per ridurre le dimensioni fisiche dei file, che possono arrivare anche a centinaia di MB, a seconda delle informazioni estratte.


## Controlli anti-scraping
I social per salvaguardare la privacy dei dati degli utenti adottano soluzioni di contrasto alle azioni di scraping. In particolare impiegano sistemi di:
* autenticazione, ovvero non si possono vedere le informazioni e scaricarle se prima non si effettua il login
* politiche di ban, ovvero si proibisce disattivando l'account di un utente, la fruizione delle informazioni e l'utilizzo del social
* controllo sul numero delle richieste e sulla loro provenienza tramite indirizzo IP e posizione geografica dello stesso. Si è osservato come questa categoria di controllo sia molto efficace come metodo di contrasto.
* fingerprinting, il browser fingerprinting è la raccolta di informazioni di un dispositivo con il fine di identificare lo stesso
* aggiornamenti, si è osservato come sia stato necessario aggiornare continuamente la funzionalità dei tool e dei connettori a causa di aggiornamenti tecnici delle piattaforme social e conseguenti  cambiamenti.

## Metodi di elusione dei controlli
Per garantire l'operatività dei connettori sono stati sviluppati ed integrati questi metodi di elusione:
* creazione ed impiego di account multipli, idealmente sarebbero necessari centinaia di account per far fronte alle soluzioni anti-scraping
* cookie rotation e account rotation
* aggiunta di ritardo tra le operazioni, impersonificando l'attività automatica dei tool, dimostrando così al social che le azioni, essendo più lente, siano assimilabili ad un utente umano e non ad un computer.

## Cookie-rotation e automazione
In particolare per lo sviluppo della cookie-rotation, funzione fondamentale tra quelle di elusione, si è previsto l'utilizzo di Selenium (strumento di automatizzazione dei browser) per effettuare il login ed estrarre i cookies.

Una volta fatto ciò viene avviata una rotazione e una scelta randomica dell'account da utilizzare. Qualora l'utenza incorra in soluzioni anti-scraping che prevedono ban o altre tipologie di "stop" alle operazioni, si provvede ad avviare nuovamente la rotazione dei cookies ed impiegare un nuovo account.


## Test e prestazioni
Dai test effettuati sui due collettori, si è osservata una maggiore velocità nello scraping, da parte del collettore di instagram. Impostata la soglia sia per i post che nel caso di lista testuale di follower, il collettore di instagram raggiunge con una velocità circa doppia il limite.

Il limite è stato impostato sulla base del comportamento dei sistemi di anti-scraping adottati dai social.

Se da un lato la velocità di instagam consente la fruizione dei dati in maniera più celere, dall'altro si preferisce la lentezza operativa del collettore di facebook, la quale è in grado di essere più resistente al contrasto.

## Conclusioni
I connettori sviluppati adottano un buon comportamento sia a livello operativo che a livello di elusione del contrasto.
Lo sviluppo delle API e la conteinerizzazione del software ha consentito anche la portabilità del sistema rendendolo multipiattaforma.

I possibili sviluppi futuri di questo progetto possono basarsi sulla creazione di nuovi metodi di elusione più forti e resistenti, ad esempio adottando una rotazione degli indirizzi IP, o implementare i connettori in sistemi distribuiti.