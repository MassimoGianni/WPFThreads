				WPF threads

Thread.Sleep()  → Quando il metodo Thread.Sleep() viene chiamato, il thread corrente viene sospeso e non esegue alcun codice per il tempo specificato. Dopo che il tempo di attesa è trascorso, il thread riprende l'esecuzione dal punto in cui è stato interrotto.
private void Button_Click(object sender, RoutedEventArgs e) 
{
    for (int x = 0; x < GIRI; x++)
    {
        lblCounter1.Text = x.ToString();
        Thread.Sleep(100);
    }
}
Poi bisogna lanciare un Thread separato alla velocità che gli viene imposti ma bisogna lasciare libero il thread presente all'interno della GUI.
Però prima di tutto bisogna fare un metodo che non ti fa Tornare nulla così la GUI Puoi continuare a girare indipendentemente.

Però tra i 2 thread non possono usare le risorse reciproche senza pagare spazio, perciò si usa un “lasciapassare” ovvero dispatcher anche detto zona critica, e all’interno di esso si fanno delle azioni che in norma non si potrebbero fare.


Dopo aver usato il dispatcher nella interfaccia grafica verrà visualizzato un conteggio in tempo che all’inizio da solo un risultato finale, però il conteggio si altera perché 2 
stanno lavorando sulla stessa variabile.

I stati dei Thread sono:
Non avviato: è lo stato iniziale del thread. Il thread è stato creato ma non è ancora iniziato.
In esecuzione: il thread è in esecuzione ed esegue il codice.
WaitSleepJoin (in attesa o in sospensione): il thread è stato sospeso utilizzando il metodo Thread.Sleep() o è in attesa di un'altra operazione, ad esempio un'operazione di I/O.
Interrotto: il thread è terminato o un'eccezione irreversibile che ha interrotto l'esecuzione. Questo stato può essere raggiunto anche quando si chiama il metodo Abort() su un Thread.

Più avanti nel codice abbiamo  messo 2 contatori e abbiamo notato che non possono andare d’accordo perché c'è concorrenza nella variabile e finché il risultato non è stato preso,  Per sistemare questo problema usiamo il LOCK.



Però nasce un altro problema ovvero  che nessuno aggiorna la label di incrementa1 e per questo un contatore conta in Maniera ottimale e l’altro no.
Per questo problema serve un lock che serve per far sì che il processo non si blocchi e svolga la funzione di semaforo(IL semaforo è un intero che non può essere negativo).
Poi si usa signal finché non arriva a 0, Wait invece è una procedura bloccante che si sblocca quando I processi sono finiti. Per far sì che capiamo che tutto è andato a buon fine facciamo stampare una stringa che però ci darà un errore, i semafori non possono essere messi dentro un event end  perciò dobbiamo lanciare il terzo thread e abbiamo bisogno di un metodo e Siccome il metodo uno e due non tornano niente la strada migliore è creare un altro metodo dove infilarci il .
Devo fare un altro dispatcher per sistemare questo problema e Per far capire che tutto è finito mandiamo un messaggio di avviso.
Se clicco una seconda volta il button il semaforo smette di funzionare perché vengono a meno i Reference del 1 semaforo, Per questo nominiamo il pulsante e lo disabilitiamo dopo averlo attivato per la prima volta.
Infine mettiamo il bottone in modalità “true” cosi lo possiamo attivare quando lo vogliamo e se tutto andrà bene ci verrà fuori questa interfaccia. 


