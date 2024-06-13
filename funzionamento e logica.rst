Funzionamento e logica
======================

Questa sezione è dedicata a spiegare il funzionamento e la logica del programma, in particolare di come sono gestiti gli appuntamenti, l'integrazione con IFB e altro. 

Ogni prenotazione effettuata tramite SmartBooking viene salvata nel database insieme alle prenotazioni di eventuali partecipanti. Queste prenotazioni sono poi renderizzate nella tabella che si vede nelle varie pagine di SmartBooking. 

Per invece le prenotazioni non effettuate con SmartBooking ma fatte con, ad esempio, Outlook o in generale sfruttando il protocollo IFB, esiste un engine separato dalla web application di SB che sincronizza i dati delle stanze con i database di SB. 
In particolare, ogni 5 secondi fa una richiesta al server di posta aziendale i dati IFB delle stanze. Questi dati vengono controllati e in caso di aggiornamenti (sia cancellazione sia aggiunta di nuovi appuntamenti), i nuovi dati vengono serializzati e inviati a SmartBooking.
Un app separata da SB è in continuo ascolto per la ricezione dei dati aggiornati. Una volta ricevuto il tipo di operazione (cancellazione o aggiunta), tramite il modello Booking va a gestire il database, aggiungendo o togliendo gli appuntamenti.
Questo approccio predilige la semplicità realizzativa e la velocità (in particolare in fase di render dell'applicazione), oltre che alla gestione delle risorse in quanto la maggior parte dell'elaborazione viene effettuata dall'engine, che è un programma differente e completamente staccato da SmartBooking. 
Supera anche un limite del protocollo IFB, ovvero che le prenotazioni saranno salvate anche dopo i 30 giorni e si potranno prenotare stanze per piu di 30 giorni nel futuro. 
Il tutto è basato su DRF.

Sullo stesso principio iniziale si basa anche la gestione dei Meeting. Sono entità separate dai normali Booking perché non riguardano le sale riunione ma gli utenti finali. 
IFB in questo caso è solo usato per controllare la disponibilità degli utenti. Non viene fatto alcun sync fra i dati IFB degli utenti e il modello Meeting in quanto si creerebbe un numero esponenziale di entries, che crescerebbe al numero degli utenti.
