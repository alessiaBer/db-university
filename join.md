1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze
3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome
5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)
7. BONUS: Selezionare per ogni studente quanti tentativi d’esame ha sostenuto per superare ciascuno dei suoi esami

## 1
SELECT `students`.`name` as `student_name`, `students`.`surname` as `student_surname`, `degrees`.`name` as `degree_name` 
FROM `students` 
JOIN `degrees` ON `students`.`degree_id` = `degrees`.`id` 
WHERE `degrees`.`name` = 'Corso di Laurea in Economia';

## 2
SELECT `degrees`.`name` as `degree_name`, `departments`.`name` as `department_name` 
FROM `degrees` 
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id` 
WHERE `departments`.`name` = 'Dipartimento di Neuroscienze' 
AND `degrees`.`level` = 'magistrale';

## 3
SELECT `teachers`.`name` as `teacher_name`, `teachers`.`surname` as `teacher_surname`, `courses`.`name` as `course_name` 
FROM `course_teacher` 
JOIN `teachers` ON `course_teacher`.`teacher_id` = `teachers`.`id` 
JOIN `courses` ON `course_teacher`.`course_id` = `courses`.`id` 
WHERE `course_teacher`.`teacher_id` = 44;

## 4
SELECT `students`.`surname` as `student_surname`, `students`.`name` as `student_name`, `degrees`.`name` as `degree_name`, `departments`.`name` as `department_name` 
FROM `students` 
JOIN `degrees` ON `students`.`degree_id` = `degrees`.`id` 
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id` 
ORDER BY `student_surname`,`student_name`;

## 5
SELECT `degrees`.`name` as `degree_name`, `courses`.`name` as `course_name`, `teachers`.`name` as `teacher_name`, `teachers`.`surname` as `teacher_surname` FROM `course_teacher` 
JOIN `teachers` ON `course_teacher`.`teacher_id` = `teachers`.`id` 
JOIN `courses` ON `course_teacher`.`course_id` = `courses`.`id` 
JOIN `degrees` ON `courses`.`degree_id` = `degrees`.`id` 
ORDER BY `degree_name`;

## 6
SELECT DISTINCT `teachers`.`name` as `teacher_name`, `teachers`.`surname` as `teacher_surname`, `departments`.`name` as `department_name` 
FROM `course_teacher` 
JOIN `teachers` ON `course_teacher`.`teacher_id` = `teachers`.`id` 
JOIN `courses` ON `course_teacher`.`course_id` = `courses`.`id` 
JOIN `degrees` ON `courses`.`degree_id` = `degrees`.`id` 
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id` 
WHERE `departments`.`name` = 'Dipartimento di Matematica';