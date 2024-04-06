# Esercizio db-university

## Caricate un secondo file nella stessa repo di ieri (db-university) con le query di oggi.

## Group by:

1. Contare quanti iscritti ci sono stati ogni anno

```sql
SELECT YEAR(`enrolment_date`) AS `enrolment_year`, COUNT(*) AS `total_enrolment`
FROM `students`
GROUP BY `enrolment_year`;
```

2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio

```sql
SELECT `office_address`, COUNT(*) AS 'teachers_count'
FROM `teachers`
GROUP BY `office_address`
ORDER BY COUNT(*) DESC;
```

3. Calcolare la media dei voti di ogni appello d'esame

```sql
SELECT `exam_id`, AVG(`vote`) AS 'average_grades'
FROM `exam_student`
GROUP BY `exam_id`;
```

4. Contare quanti corsi di laurea ci sono per ogni dipartimento

```sql
SELECT `departments`.`name` AS 'department_name', COUNT(`degrees`.`department_id`) AS 'degrees_count'
FROM `departments`
JOIN `degrees` ON `departments`.`id` = `department_id`
GROUP BY `departments`.`name`
ORDER BY `degrees_count` DESC;
```

## Joins:

1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

```sql
SELECT `students` . `name` , `students` . `surname` , `degrees` . `name` AS `degree_name`
FROM `students`
JOIN `degrees` ON `students` . `degree_id` = `degrees` . `id`
WHERE `degrees` . `name` = 'Corso di Laurea in Economia';
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
SELECT `teachers`.`name`, `teachers`.`surname`, `courses`.`name` AS 'courses_name'
FROM `teachers`
JOIN `course_teacher` ON `teacher_id` = `teachers`.`id`
JOIN `courses` ON `courses`.`id` = `course_id`
WHERE `teacher_id` = '44';
```

4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

```sql
SELECT `students`.`name` AS 'student_name', `students`.`surname`, `degrees`.`name` AS 'degrees_name', `departments`.`name` AS 'department_name'
FROM `students`
JOIN `degrees` ON `students`. `degree_id` = `degrees`.`id`
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`
ORDER BY `students`.`name`, `students`.`surname`;
```

5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

```sql
SELECT `degrees`.`name` AS `degree_name`, `courses`.`name` AS `course_name`, `teachers`.`name` AS `teacher_name`, `teachers`.`surname`
FROM `degrees`
JOIN `courses` ON `degrees`.`id` = `courses`.`degree_id`
JOIN `course_teacher` ON `courses`.`id` = `course_teacher`.`course_id`
JOIN `teachers` ON `teachers`.`id` = `course_teacher`.`teacher_id`;
```

6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

```sql
SELECT DISTINCT `teachers`.`name` AS 'teacher_name', `teachers`.`surname` AS 'teacher_surname', `departments`.`name` AS 'department_name'
FROM `teachers`
JOIN `course_teacher` ON `teachers`.`id` = `course_teacher`.`teacher_id`
JOIN `courses` ON `course_teacher`.`course_id` = `courses`.`id`
JOIN `degrees` ON `courses`.`degree_id` = `degrees`.`id`
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`
WHERE `departments`.`name` = 'Dipartimento di Matematica'
ORDER BY `teacher_surname` ASC;
```

7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.

```sql
SELECT COUNT(*) AS 'exam_attemps', `students`.`name`, `students`.`surname`, `courses`.`name` AS 'course_name', MAX(`exam_student`.`vote`) AS 'max_vote', MIN(`exam_student`.`vote`) AS 'min_vote', AVG(`exam_student`.`vote`) AS 'average_vote'
FROM `students`
JOIN `exam_student` ON `students`.`id` = `exam_student`.`student_id`
JOIN `exams` ON `exam_student`.`exam_id` = `exams`.`id`
JOIN `courses` ON `exams`.`course_id` = `courses`.`id`
WHERE `exam_student`.`vote` >= '18'
GROUP BY `courses`.`id`, `students`.`id`
ORDER BY `average_vote` DESC;
```
