# 📊 Analisi Dati di Vendita 2024 - Test Pratico

Questo repository contiene la soluzione del test pratico. 
L'obiettivo del progetto è analizzare un file di vendite grezzo (`esercizio_it.csv`), fare pulizia dei dati (Data Cleaning) per correggere gli errori di inserimento, e calcolare i KPI richiesti dal business.

## 📂 Struttura del Progetto
* **`esercizio_it.csv`**: Il file originale con i dati di vendita.
* **`analisi_vendite.ipynb`**: Il Jupyter Notebook con il codice Python (libreria Pandas) e i risultati.
* **`requirements.txt`**: File di configurazione contenente la libreria utilizzata (`pandas`).
* **`README.md`**: Questo file con la spiegazione del lavoro e il report finale.


## 🛠️ Logica Applicata e Data Cleaning

Prima di fare qualsiasi calcolo matematico, ho analizzato il file CSV e ho notato che i dati contenevano alcuni errori tipici di quando si inseriscono i dati a mano. Senza correggerli prima, i calcoli finali sarebbero stati sbagliati. 

Ho strutturato il codice in Python seguendo questa logica:

1. **Rimozione degli spazi vuoti (`.str.strip()`):** Nel CSV, alcune righe del prodotto `"Antiparassitario Spot-On Cane "` avevano uno spazio vuoto alla fine del testo. Python li vedeva come due prodotti diversi. Pulendo le stringhe abbiamo unito i dati correttamente.
2. **Correzione di Maiuscole/Minuscole (`.str.title()`):** I nomi degli agenti commerciali erano scritti male (es. `BIANCHI LAURA`, `Bianchi Laura`, `rossi marco`). Ho normalizzato il testo mettendo la prima lettera maiuscola, altrimenti il fatturato di un agente si sarebbe diviso su più righe, falsando la classifica.
3. **Gestione delle Date (`pd.to_datetime`):** Ho convertito la colonna delle date in un formato nativo che Python potesse capire, così da poter estrarre facilmente i mesi ed evitare bug sul calcolo della stagionalità.
4. **Controllo di Integrità:** Ho verificato via software che la colonna `totale` corrispondesse sempre esattamente a `quantita` * `prezzo_unitario`. Non sono state trovate anomalie numeriche.

---

## 📊 Report Finale e Risultati

### 1. Totale venduto per prodotto
*I prodotti sono ordinati dal fatturato più alto al più basso dopo aver rimosso i duplicati testuali.*

| Posizione | Prodotto | Quantità Totale | Fatturato Totale (€) |
| :---: | :--- | :---: | :---: |
| **1** | Antinfiammatorio Iniettabile | 263 | 21.304,20 |
| **2** | Integratore Articolare | 250 | 17.415,62 |
| **3** | Shampoo Dermatologico | 257 | 14.409,32 |
| **4** | Antibiotico Orale | 256 | 14.152,03 |
| **5** | Antiparassitario Spot-On Gatto | 210 | 14.095,39 |
| **6** | Collare Antiparassitario | 157 | 13.132,53 |
| **7** | Antimicotico Topico | 210 | 13.084,65 |
| **8** | Antiparassitario Spot-On Cane | 232 | 12.637,83 |
| **9** | Probiotico Intestinale | 159 | 10.196,85 |
| **10** | Vaccino Polivalente Cane | 109 | 7.211,45 |

### 2. Totale venduto per agente e per area geografica
*Fatturato totale raggruppato per territorio e per commerciale.*

| Area | Agente | Fatturato Totale (€) |
| :--- | :--- | :---: |
| **Centro** | Ferrari Giovanni | 23.760,70 |
| **Nord Est** | Bianchi Laura | 27.374,20 |
| | Rossi Marco | 67.28 |
| **Nord Ovest** | Rossi Marco | 29.539,28 |
| | Marino Luca | 29.354,44 |
| | Bianchi Laura | 646.38 |
| **Sud** | Conti Sara | 26.897,59 |

*Nota:* L'agente *Ferrari Giovanni* ha venduto sia al Centro che al Sud; il codice assegna correttamente gli importi alle rispettive aree senza mischiare i dati.

### 3. Mesi con il fatturato più alto e più basso
* **Mese Top (Fatturato Maggiore):** Ottobre 2024 (`2024-10`) con **16.595,35 €**
* **Mese Flop (Fatturato Minore):** Giugno 2024 (`2024-06`) con **8.409,90 €**

### 4. Clienti con un solo ordine nell'anno
* **Risultato:** **0 clienti.**
* **Nota tecnica:** Analizzando il database tramite il conteggio delle frequenze, emerge che tutti i clienti presenti (da `CLI001` a `CLI012`) hanno effettuato ordini ricorrenti durante l'anno (da un minimo di 10 a un massimo di 23 ordini a testa). Non ci sono clienti "one-shot".

---

## 💻 Come eseguire il progetto in locale

Per scaricare il progetto ed eseguire il codice sul tuo computer:

```bash
# 1. Clona questo repository
git clone https://github.com/russelryanguevarra-cmyk/Data-Analysis-Report-Vendite-2024

# 2. Entra nella cartella
cd [NOME_DELLA_CARTELLA]

# 3. Installa la libreria Pandas
pip install -r requirements.txt

# 4. Avvia Jupyter Notebook per vedere il codice
jupyter notebook
