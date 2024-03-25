# Esercizio db-university

## Modellizzare la struttura di un database per memorizzare tutti i dati riguardanti una università:

- sono presenti diversi Dipartimenti (es.: Lettere e Filosofia, Matematica, Ingegneria ecc.);
- ogni Dipartimento offre più Corsi di Laurea (es.: Civiltà e Letterature Classiche, Informatica, Ingegneria Elettronica ecc..);
- ogni Corso di Laurea prevede diversi Corsi (es.: Letteratura Latina, Sistemi Operativi 1, Analisi Matematica 2 ecc.);
- ogni Corso può essere tenuto da diversi Insegnanti;
- ogni Corso prevede più appelli d'Esame;
- ogni Studente è iscritto ad un solo Corso di Laurea;
- ogni Studente può iscriversi a più appelli di Esame;
- per ogni appello d'Esame a cui lo Studente ha partecipato, è necessario memorizzare il voto ottenuto, anche se non sufficiente.

Pensiamo a quali entità (tabelle) creare per il nostro database e cerchiamo poi di stabilirne le relazioni.
Infine, andiamo a definire le colonne e i tipi di dato di ogni tabella.

### Elenco delle tabelle:

1. Dipartimenti

- id | BIGINT PRIMARY-KEY AUTO-INCREMENT UNIQUE NOTNULL
- nome | VARCHAR (255) NOTNULL

2. Corsi di Laurea

- id | BIGINT PK AI UNIQUE NOTNULL
- nome | VARCHAR (255) NOTNULL
- dipartimento_id | FK

3. Corsi selezionati

- id | BIGINT PK AI UNIQUE NOTNULL
- nome | VARCHAR (255) NOTNULL
- corsolaurea_id | FK
- ? insegnante_id

4. Insegnanti

- id | BIGINT PK AI UNIQUE NOTNULL
- nome | VARCHAR (50) NOTNULL
- cognome | VARCHAR (50) NOTNULL
- ? corsoselezionato_id

5. Appelli d'esame

- id | BIGINT PK AI UNIQUE NOTNULL
- data | DATE NOTNULL
- corsoselezionato_id | FK
- voto | FLOAT NOTNULL
- studente_id | FK

6. Studenti

- id | BIGINT PK AI UNIQUE NOTNULL
- nome | VARCHAR (50) NOTNULL
- cognome | VARCHAR (50) NOTNULL
- anno di nascita | DATE NULL
- corsolaurea_id | FK
