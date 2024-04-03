# Esercizio db-university

## Caricate un secondo file nella stessa repo di ieri (db-university) con le query di oggi.

## Group by:

1. Contare quanti iscritti ci sono stati ogni anno

```sql
SELECT YEAR(`enrolment_date`) AS `enrolment_year`, COUNT(*) AS `total_enrolment` FROM `students` GROUP BY `enrolment_year`;
```

2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio

```sql

```

3. Calcolare la media dei voti di ogni appello d'esame

```sql


```

4. Contare quanti corsi di laurea ci sono per ogni dipartimento

```sql


```

## Joins:

1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

```sql
SELECT `students` . `name` , `students` . `surname` , `degrees` . `name` AS `degree_name` FROM `students` JOIN `degrees` ON `students` . `degree_id` = `degrees` . `id` WHERE `degrees` . `name` = 'Corso di Laurea in Economia';
```

2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

```sql
SELECT `degrees` . *
FROM `degrees`
JOIN `departments`
ON `degrees` . `department_id` = `departments` . `id`
WHERE `degrees` . `level` = 'magistrale' AND  `departments` . `name` = 'Dipartimento di Neuroscienze';
```

3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

```sql


```

4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

```sql

SELECT `students`.`name` AS `name_student`, `students`.`surname`, `degrees`.`name`, `departments` . `name`
FROM `students`
JOIN `degrees` ON `students`. `degree_id` = `degrees`.`id`
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`
ORDER BY `students`.`name`, `students`.`surname`;

```

5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

```sql

SELECT `degrees`.`name` AS `degree_name`, `courses`.`name` AS `course_name`, `teachers`.`name` AS `teacher_name`, `teachers`.`surname` FROM `degrees` JOIN `courses` ON `degrees`.`id` = `courses`.`degree_id` JOIN `course_teacher` ON `courses`.`id` = `course_teacher`.`course_id` JOIN `teachers` ON `teachers`.`id` = `course_teacher`.`teacher_id`;


```

6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

```sql


```

7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.

```sql


```
