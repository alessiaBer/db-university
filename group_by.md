1. Contare quanti iscritti ci sono stati ogni anno
2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio
3. Calcolare la media dei voti di ogni appello d'esame
4. Contare quanti corsi di laurea ci sono per ogni dipartimento

## 1
SELECT COUNT(*) as `total_students`, YEAR(`enrolment_date`) as `enrolment_year` 
FROM `students` 
GROUP BY `enrolment_year`;

## 2
SELECT COUNT(*) as `total_teachers`, `office_address` 
FROM `teachers` 
GROUP BY `office_address`;

## 3
SELECT AVG(`vote`) as `average_vote`, `exam_id` 
FROM `exam_student` 
GROUP BY `exam_id`;

## 4
SELECT COUNT(*) as `total_degrees`, `department_id` 
FROM `degrees` 
GROUP BY `department_id`;