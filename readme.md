1. Selezionare tutti gli studenti nati nel 1990 (160)
2. Selezionare tutti i corsi che valgono più di 10 crediti (479)
3. Selezionare tutti gli studenti che hanno più di 30 anni
4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di laurea (286)
5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del 20/06/2020 (21)
6. Selezionare tutti i corsi di laurea magistrale (38)
7. Da quanti dipartimenti è composta l'università? (12)
8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)

## 1
SELECT * 
FROM `students` 
WHERE YEAR(`date_of_birth`) = 1990;

## 2
SELECT * 
FROM `courses` 
WHERE `cfu` > 10;

## 3
SELECT * 
FROM `students` 
WHERE 2023 - YEAR(`date_of_birth`) > 30;
soluzione giusta:
TIMESTAMPDIFF(YEAR, `date_of_birth`, CURDATE()) > 30;

## 4
SELECT * 
FROM `courses` 
WHERE `period` = 'I semestre' 
AND `year` = 1;

## 5
SELECT * 
FROM `exams` 
WHERE `date` = '2020-06-20' 
AND TIME(`hour`) > '14:00:00';

## 6
SELECT * 
FROM `degrees` 
WHERE `level` = 'magistrale';

## 7
SELECT COUNT(*) 
FROM `departments`;

## 8 
SELECT * 
FROM `teachers` 
WHERE `phone` 
IS NULL;
bisognava contarli:
SELECT COUNT(*)
FROM `teachers`
WHERE `phone`
IS NULL;


**LIVE**
## Join Lorenzo 2:
Selezionare le informazioni sul corso con id = 144, con tutti i relativi appelli d’esame */


SELECT `courses`.`id` AS `course_id`, `courses`.`name`, `courses`.`description`, `courses`.`year`, `courses`.`cfu`, `courses`.`website`, `exams`.`id` as `exam_id` 
FROM `courses` 
JOIN `exams` ON `courses`.`id` = `exams`.`course_id` 
WHERE `course_id` = 144;


## CArmelo query joint 3:
Selezionare a quale dipartimento appartiene il Corso di Laurea in Diritto
dell'Economia (Dipartimento di Scienze politiche, giuridiche e studi internazionali)*/


SELECT `departments`.* 
FROM `departments` 
JOIN `degrees` ON `departments`.`id` = `degrees`.`department_id` 
WHERE `degrees`.`name` = 'Corso di Laurea in Diritto dell\'Economia';


## Rizzo Join 4:
Selezionare tutti gli appelli d'esame del Corso di Laurea Magistrale in Fisica del primo anno*/


SELECT `courses`.`name` as `course_name`, `courses`.`period`, `courses`.`cfu`, `exams`.`date`, `exams`.`address`, `degrees`.`name` as `degree_name`
FROM `degrees` 
JOIN `courses` ON `degrees`.`id` = `courses`.`degree_id` 
JOIN `exams` ON `courses`.`id` = `exams`.`course_id` 
WHERE `degrees`.`name` = 'Corso di Laurea Magistrale in Fisica' 
AND `courses`.`year` = 1;


## Join Giuseppe 5:
Selezionare tutti i docenti che insegnano nel Corso di Laurea in Lettere (21) */


SELECT DISTINCT `teachers`.* 
FROM `teachers` 
JOIN `course_teacher` ON `teachers`.`id` = `course_teacher`.`teacher_id` 
JOIN `courses` ON `course_teacher`.`course_id` = `courses`.`id` 
JOIN `degrees` ON `courses`.`degree_id` = `degrees`.`id` 
WHERE `degrees`.`name` = 'Corso di Laurea in Lettere';


## Join Riccardo 6:
Selezionare il libretto universitario di Mirco Messina (matricola n. 620320)


SELECT `students`.`name`, `students`.`surname`, `students`.`registration_number`, `courses`.`id`, `courses`.`name`, `exams`.`date`, `exam_student`.`vote`
FROM `exam_student`
JOIN `students` ON `exam_student`.`student_id` = `students`.`id`
JOIN `exams` ON `exam_student`.`exam_id` = `exams`.`id`
JOIN `courses` ON `exams`.`course_id` = `courses`.`id`
WHERE `students`.`name` = 'Mirco' 
AND `students`.`surname` = 'Messina' 
AND `exam_student`.`vote` >= 18;

## Roberto Nesta 7:
Selezionare il voto medio di superamento d'esame per ogni corso, con anche i dati
del corso di laurea associato, ordinati per media voto decrescente


SELECT AVG(`exam_student`.`vote`) as `vote_average`, `courses`.`name` as `course_name`, `degrees`.`name` as `degree_name`
FROM `exam_student`
JOIN `exams` ON `exam_student`.`exam_id` = `exams`.`id`
JOIN `courses` ON `exams`.`course_id` = `courses`.`id`
JOIN `degrees` ON `courses`.`degree_id` = `degrees`.`id`
GROUP BY `courses`.`id`
ORDER BY `vote_average` DESC;