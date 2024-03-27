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

## Dopo aver creato un nuovo database nel vostro phpMyAdmin e aver importato lo schema allegato, eseguite le query del file allegato.

1. Selezionare tutti gli studenti nati nel 1990 (160)

- ```sql
  SELECT * FROM `students` WHERE `date_of_birth` BETWEEN '1990-01-01' AND '1990-12-31';
  ```

2. Selezionare tutti i corsi che valgono più di 10 crediti (479)

- ```sql
  SELECT * FROM `courses` WHERE `cfu` > 10;
  ```

3. Selezionare tutti gli studenti che hanno più di 30 anni

- ```sql
  SELECT * FROM `students` WHERE DATEDIFF(NOW(), `date_of_birth`) / 365 > 30
  ```

4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di laurea (286)

- ```sql
  SELECT * FROM `courses` WHERE `period` = 'I semestre' AND `year` = '1';
  ```

5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del 20/06/2020 (21)

- ```sql
  SELECT * FROM `exams` WHERE `date` = '2020-06-20' AND TIME(`hour`) > '14:00:00';
  ```

6. Selezionare tutti i corsi di laurea magistrale (38)

- ```sql
  SELECT * FROM `degrees` WHERE `name` LIKE '%Laurea Magistrale%';
  ```

7. Da quanti dipartimenti è composta l'università? (12)

- ```sql
  SELECT * FROM `departments` COUNT;
  ```

8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)

- ```sql
  SELECT * FROM `teachers` WHERE `phone` IS null;
  ```
