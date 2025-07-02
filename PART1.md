
# Creazione delle Routing Tables e Gestione del Traffico

In questa sezione del progetto, l'obiettivo è creare le **routing table**, i **gruppi di sicurezza** e configurare un **ACL (Network Access Control List)** per la protezione e gestione del traffico all'interno della VPC.

## Fasi di sviluppo

### 1. Creazione della Routing Table

Per abilitare la comunicazione dall'esterno, ho creato una nuova **Routing Table**.  
La routing table definisce la direzione che il traffico deve seguire per raggiungere una destinazione.

Quando viene creata una VPC, AWS genera automaticamente una routing table con una sola route:

- **Destinazione**: `10.0.0.0/16`  
- **Target**: `local`

Questa route permette la comunicazione interna tra le risorse all'interno della VPC.  
Per consentire la comunicazione con l'esterno (Internet), ho aggiunto una nuova route:

- **Destinazione**: `0.0.0.0/0`  
- **Target**: `Internet Gateway`

In questo modo, tutto il traffico che non è destinato agli indirizzi interni verrà inoltrato all'Internet Gateway.

---

### 2. Associazione della Routing Table alla Subnet

Una subnet, per poter comunicare con l'esterno o con altre subnet interne, deve essere associata a una routing table.  
Dopo aver associato la subnet alla routing table appena creata, questa può essere considerata una **subnet pubblica**, in quanto instrada il traffico verso l'esterno tramite le rotte definite.

---

### 3. Configurazione del Gruppo di Sicurezza

Ogni risorsa all'interno di una subnet deve essere protetta da un **Security Group**, che filtra il traffico in entrata e in uscita in base a porte e protocolli.

Il gruppo di sicurezza è stato creato con le seguenti impostazioni:

- **Nome**: `my-sg-main`
- **Descrizione**: Gruppo di sicurezza generale per VPC Main
- **VPC**: `my-vpc-main`
- **Regole di ingresso**:
  - HTTP su porta `80`
  - Origine: `0.0.0.0/0` (consente il traffico da qualsiasi origine)

---

### 4. Configurazione del Network ACL (NACL)

A differenza dei Security Group, che proteggono **singole risorse**, il **Network ACL** protegge l’intera **subnet**.  
Per esempio, possiamo bloccare un protocollo a livello di subnet con l’ACL e bloccare un IP specifico con un Security Group.

Configurazione del NACL:

- **Nome**: `my-acl-main`
- **VPC**: `my-vpc-main`
- **Regole**:
  - Ingresso: consente tutto il traffico
  - Uscita: consente tutto il traffico

Infine, ho associato il NACL alla subnet `public-subnet-1`.

---

Con queste configurazioni, il traffico nella rete è ora **instradato correttamente**, e le risorse all'interno della subnet sono **protette** sia a livello di risorsa che a livello di subnet.
