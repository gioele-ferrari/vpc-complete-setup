# Creazione di due istanze EC2 per test di comunicazione

Questa è la fase conclusiva del mio progetto, in cui ho creato **due istanze EC2** per effettuare dei **test di rete (ping)** tra subnet pubblica e privata.

---

## Fasi di sviluppo

1. Ho creato due istanze EC2:
   - **EC2 Public Instance**, posizionata nella **subnet pubblica**
   - **EC2 Private Instance**, posizionata nella **subnet privata**

2. Ho testato la comunicazione eseguendo un comando **ping**:
   - **Dal mio computer locale verso l'istanza nella subnet pubblica** → Risposta positiva (il ping ha funzionato correttamente).
   - **Dal mio computer verso l'istanza nella subnet privata** → Nessuna risposta, come previsto, in quanto non esposta a Internet.

3. Infine, ho verificato che:
   - **Le due istanze EC2 comunicano tra loro senza problemi**, grazie alle configurazioni corrette di subnet, routing table e gruppi di sicurezza.

---

## Conclusione

Questo test ha confermato il corretto funzionamento della mia architettura VPC, con una distinzione chiara tra subnet pubblica e privata, e un controllo efficace del traffico in entrata e uscita.
