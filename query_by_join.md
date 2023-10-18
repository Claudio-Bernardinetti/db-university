##
Group by:

1. Contare quanti iscritti ci sono stati ogni anno
# 1 SELECT COUNT(*) AS `enrolment_date` 
    FROM `students`;

2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio
# 2 SELECT `office_address` AS office, COUNT(DISTINCT `name`, `surname`) AS number_teachers
    FROM `teachers`
    GROUP BY `office_address`;

3. Calcolare la media dei voti di ogni appello d'esame
# 3 SELECT `exam_id` AS exam, AVG(vote) AS avg_vote 
    FROM `exam_student` 
    GROUP BY `exam_id`;

4. Contare quanti corsi di laurea ci sono per ogni dipartimento
# 4 SELECT `department_id`, COUNT(*) AS number_courses 
    FROM `degrees` 
    WHERE `name` LIKE 'Corso di Laurea in%' 
    GROUP BY `department_id`;

##
Joins:

1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
# 1 SELECT students.* 
    FROM `students` 
    JOIN `degrees` ON `students`.`degree_id` = `degrees`.`id` 
    WHERE `degrees`.`name` = 'Corso di Laurea in Economia';

2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze
# 2 SELECT `degrees`.`name` AS couses 
    FROM `degrees` 
    JOIN `departments` ON `degrees`.`department_id` = `departments`.`id` 
    WHERE `degrees`.`level` = 'Laurea Magistrale' AND `departments`.`name` = 'Dipartimento di Neuroscienze';

3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
# 3 SELECT `teachers`.`name`, `teachers`.`surname`, COUNT(*) as courses_number
    FROM `teachers` 
    JOIN `course_teacher` ON `teachers`.`id` = `course_teacher`.`teacher_id`
    WHERE `course_teacher`.`teacher_id` = 44;

4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome
# 4 SELECT `students`.`name`, `students`.`surname`, `degrees`.`name` AS `degree_name`, `departments`.`name` AS     `department_name`
    FROM `students`
    JOIN `degrees` ON `students`.`degree_id` = `degrees`.`id`
    JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`
    ORDER BY `students`.`surname`, `students`.`name`;
5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
# 5 SELECT `degrees`.`name` AS Degree_Name, `degrees`.`level` AS Degree_Level, `courses`.`id` AS Course_ID, `teachers`.`name` AS Teacher_Name, `teachers`.`surname` AS Teacher_Surname
    FROM `course_teacher`
    JOIN `courses` ON `course_teacher`.`course_id` = `courses`.`id`
    JOIN `teachers` ON `course_teacher`.`teacher_id` = `teachers`.`id`
    JOIN `degrees` ON `courses`.`degree_id` = `degrees`.`id`
    ORDER BY `courses`.`id`;

6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.