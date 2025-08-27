# Databricks AI/BI Genie – NLQ Demo Dataset

Questo repository contiene **DDL e DML** per creare un database di esempio utilizzato per testare le funzionalità **Natural Language Query (NLQ)** di [Databricks AI/BI Genie](https://www.databricks.com/product/business-intelligence/ai-bi-genie).

## Contenuto del repository

- **`ddl/`**: contiene gli script di definizione delle tabelle (dimensioni e fatti), completi di chiavi primarie e foreign key.
- **`dml/`**: contiene gli script di popolamento con dati sintetici di esempio.
- **`diagram/`** (opzionale): schema ER o immagini di supporto (se presenti).

Il modello dati segue un approccio *star schema* e include:
- **Dimensioni**: Cliente, Prodotto, Punto Vendita, Società, Valuta, Calendario, Categoria, Marchio, Stagione.
- **Fatti**: Scontrino, Dettaglio Scontrino, Budget vendite.

## Caratteristiche principali

- Supporto a **due fatti con granularità differenti**:  
  - **Vendite Reali**: a livello di riga scontrino.  
  - **Budget Vendite**: a livello giornaliero per punto vendita/valuta.
- Inclusione delle relazioni tramite chiavi esterne.
- Dataset pensato per testare:
  - Aggregazioni su metriche additive e non additive (es. conteggi distinti).
  - Analisi temporali (YTD, MTD, LY).
  - Confronti actual vs budget.
  - Gestione multivaluta tramite tassi di cambio.

## Come utilizzare gli script

1. **Clona il repository:**
   ```bash
   git clone https://github.com/<tuo-username>/<nome-repo>.git
   cd <nome-repo>
   ```

2. **Imposta il catalogo e lo schema su Databricks:**
   ```sql
   USE CATALOG fashion_catalog;
   USE SCHEMA fashion_synthetic_2;
   ```

3. **Esegui gli script DDL** per creare le tabelle:
   ```sql
   -- Esempio
   %sql
   CREATE TABLE IF NOT EXISTS VALUTA (...);
   CREATE TABLE IF NOT EXISTS SCONTRINO (...);
   ...
   ```

4. **Esegui gli script DML** per popolare i dati di esempio.

## Note e Best Practice

- Gli script sono pensati per **Databricks SQL**, ma possono essere adattati anche ad altri ambienti.
- Non sono incluse metriche derivate (YTD, MTD, vs LY, ecc.): l’obiettivo è consentire a **Genie** di generarne dinamicamente durante le query NLQ.
- Il dataset è pensato per essere **NLQ-ready**: denormalizzato tramite viste (es. `vw_scontrini_and_budget`) per facilitare la comprensione del modello da parte di Genie.

## Riferimenti

- [Articolo Medium con il caso d’uso completo](<link-al-tuo-articolo>)
- [Documentazione ufficiale Databricks AI/BI Genie](https://docs.databricks.com/aws/en/genie)
- [Metric Views (Public Preview)](https://docs.databricks.com/aws/en/metric-views/)

---

[Andrea Carmè – Senior Manager, ICONSULTING] (https://www.linkedin.com/in/andreacarme/)
*Condividi e contribuisci: ogni feedback o miglioramento è benvenuto!*
