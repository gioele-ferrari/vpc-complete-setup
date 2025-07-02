# Creazione di un’istanza EC2 con sito web statico

Questa è la parte finale del mio progetto: la creazione di un’istanza EC2 che ospita un sito web statico accessibile da Internet.

---

## Fasi di sviluppo

### 1. Creazione dell’istanza EC2

Ho creato una nuova istanza EC2 con le seguenti impostazioni:

- Nome: `my-ec2-webserver`  
- VPC: `my-vpc-main`  
- Gruppo di sicurezza: `my-sg-main`  
- Assegnazione automatica IP pubblico: abilitata

---

### 2. Connessione e configurazione del server web

Ho utilizzato EC2 Instance Connect (accesso via browser) per collegarmi all’istanza.  
All’interno della macchina virtuale ho installato e avviato un server Apache per ospitare il sito.

Comandi eseguiti:

```bash
sudo yum update -y
sudo yum install -y httpd
sudo systemctl start httpd
sudo systemctl enable httpd
```

Successivamente ho creato la pagina `index.html`:

```bash
echo '<h1>Benvenuto nel mio sito su EC2!</h1>' | sudo tee /var/www/html/index.html
```

---

### 3. Apertura del traffico HTTP

Infine, ho modificato le regole del gruppo di sicurezza `my-sg-main` per consentire l’accesso HTTP:

- Tipo: HTTP  
- Porta: 80  
- Origine: `0.0.0.0/0` (da qualunque IP)

---

## Risultato finale

Il sito web è ora visibile al seguente indirizzo:

```bash
http://3.70.53.168
```

---

## Conclusioni

Questo progetto mi ha introdotto in modo pratico al mondo AWS, consentendomi di comprendere:

- Il funzionamento delle istanze EC2
- La configurazione della rete tramite VPC e security group
- L'hosting di contenuti statici all’interno del cloud

Sono ora in grado di pubblicare e gestire una semplice infrastruttura cloud in autonomia.
