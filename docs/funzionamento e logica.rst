Funzionamento e logica
======================

Questa sezione è dedicata a spiegare il funzionamento e la logica del programma, in particolare di come sono gestiti gli appuntamenti, l'integrazione con IFB e altro. 

La tabella delle prenotazioni è basata sui dati IFB che ogni volta che carica la pagina, il server di SmartBooking richiede al server di posta aziendale. Una volta ricevuti i dati, questi vengono elaborati e visualizzati in una tabella.

Questa operazione viene eseguita ogni volta che si carica una nuova stanza o una nuova settimana. Risulta quindi molto lenta, sui 3 secondi per caricamento. Ho quindi scelto di adottare un sistema multi-threading per velocizzare il caricamento, che è ormai massimo un secondo.
Ciò non basta per garantire un'esperienza utente ottimale, quindi ho deciso di implementare un sistema di cache che salva i dati e li restituisce appena si accede ad una sala o settimana già caricata. Ciò rende il caricamento di settimane o sale già caricate istantaneo, mentre per quelle non ancora visualizzare il caricamento sarà normale.
La cache viene aggiornata ogni volta che si prenota un appuntamento, si cambia pagina o se si preme il bottone sulla destra nella barra di navigazione a destra apposito per aggiornare la cache manualmente. La cache è unica per utente, le chiavi cache sono differenziate per utente quindi non ci sono pericoli di avere la cache di altri utenti. 

Una limitazione di IFB è che sono disponibili i dati solo di 30 giorni nel passato e 30 giorni nel futuro. Non si potranno vedere in tabella le prenotazioni fatte dopo questo lasso di tempo, ma verranno comunque conservate e visualizzate nella sezione "Le mie prenotazioni".

Gli appuntamenti fatti con SmartBooking saranno salvati sia nel database, in modo tale da poterli vedere nella sezione "Le mie prenotazioni" e saranno anche inviate con IFB cosi da avere anche la rappresentazione grafica delle prenotazioni.
Le prenotazioni effettuate dall'utente saranno evidenziate in azzurro e questa visualizzazione sarà unica per utente, cosi gli altri non potranno vedere chi ha prenotato la sala. 

Nel momento in cui effettuerete una prenotazione, apparirà immediatamente nella vostra sezione ma per farla apparire in tabella e anche agli altri ci vorranno alcuni secondi, il tempo che il server elabori la richiesta e restituisca la tabella aggiornata. Potrebbe essere necessario aggiornare manualmente la cache. 
