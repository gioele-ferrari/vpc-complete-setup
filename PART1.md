
# Creazione delle Routing Tables e Gestione del Traffico

In questa sezione del progetto, l'obiettivo è creare le **routing table**, i **gruppi di sicurezza** e configurare un **ACL (Network Access Control List)** per la protezione e gestione del traffico all'interno della VPC.

## Fasi di sviluppo

### 1. Creazione della Routing Table

Per abilitare la comunicazione dall'esterno, ho creato una nuova **Public Routing Table**.
La routing table definisce la direzione che il traffico deve seguire per raggiungere una destinazione.

- **Destinazione**: `10.0.1.0/16`  
- **Target**: `local`

- **Destinazione**: `0.0.0.0/0`  
- **Target**: `Internet Gateway`

Configurazione della seconda **Public Routing Table** fatta così:

- **Destinazione**: `10.0.0.0/16`  
- **Target**: `local`

---

### 2. Associazione della Routing Table alla Subnet

Una subnet, per poter comunicare con l'esterno o con altre subnet interne, deve essere associata a una routing table.  
Dopo aver associato la subnet alla routing table appena creata, questa può essere considerata una **subnet pubblica**, in quanto instrada il traffico verso l'esterno tramite le rotte definite. Mentre la seconda rimane privata **subnet privata**.

---

### 3. Configurazione del Gruppo di Sicurezza

Ogni risorsa all'interno di una subnet deve essere protetta da un **Security Group**, che filtra il traffico in entrata e in uscita in base a porte e protocolli.

Il gruppo di sicurezza è stato creato con le seguenti impostazioni:

- **Nome**: `Security Group Main`
- **Descrizione**: Gruppo di sicurezza generale per VPC Main
- **VPC**: `Main VPC`
- **Regole di ingresso**:
  - SSH Consentito
  - ICMP Consentito

---

### 4. Configurazione del Network ACL (NACL)

A differenza dei Security Group, che proteggono **singole risorse**, il **Network ACL** protegge l’intera **subnet**.  
Per esempio, possiamo bloccare un protocollo a livello di subnet con l’ACL e bloccare un IP specifico con un Security Group.

Configurazione del NACL Privato:

- **Nome**: `Private ACL`
- **VPC**: `My VPC`
- **Regole**:
  - Ingresso: consente solo traffico ICMP da 10.0.1.0/24
  - Uscita: consente solo traffico ICMP verso 10.0.1.0/24

Configurazione del NACL Pubblico:

- **Nome**: `Public ACL`
- **VPC**: `My VPC`
- **Regole**:
  - Ingresso: consente solo traffico ICMP da 0.0.0.0/0
  - Uscita: consente solo traffico ICMP da 0.0.0.0/0

---

Con queste configurazioni, il traffico nella rete è ora **instradato correttamente**, e le risorse all'interno della subnet sono **protette** sia a livello di risorsa che a livello di subnet.

---

A questo punto il setup delle tabelle di instradamento e gruppi di sicurezza è completo, prosegue in [Creazione di un server web con EC2](PART2.md)
