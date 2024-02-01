## Repo
`db-university`

## DB
[[Database/2024-01-31 - DB University|DB University]]

## Todo
Dopo aver testato le vostre query con `phpMyAdmin`, riportatele in un file `txt` o `md` e caricatelo nella vostra repo.

### Query
#### Group by
1. Contare quanti iscritti ci sono stati ogni anno
```sql
SELECT year(enrolment_date) 'anno', COUNT(*)
FROM students
GROUP BY year(enrolment_date);
```

2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio
```sql
SELECT office_address 'ufficio', count(*)'numero insegnanti'
FROM teachers
GROUP by office_address;
```

3. Calcolare la media dei voti di ogni appello d'esame (dell'esame vogliamo solo l'`id`)
```sql
SELECT exam_id, FLOOR(AVG(vote)) 'voto medio'
FROM exam_student
GROUP BY exam_id;
```

4. Contare quanti corsi di laurea ci sono per ogni dipartimento
```sql
SELECT degrees.name, COUNT(*) 'quantita corsi'
FROM departments
JOIN degrees
ON departments.id = degrees.department_id
JOIN courses
ON degrees.id = courses.degree_id
GROUP by degrees.name;
```


#### Join
1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
```sql
SELECT degrees.name, students.name, students.surname
FROM students
JOIN degrees
on students.degree_id = degrees.id
WHERE degrees.name LIKE 'Corso di Laurea in Economia';
```

2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze
```sql
SELECT departments.*
FROM degrees
JOIN departments
on degrees.department_id = departments.id
WHERE level like 'magistrale' and departments.name like 'Dipartimento di Neuroscienze';
```

3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
```sql
SELECT degrees.*
FROM teachers
JOIN course_teacher 
on teachers.id = course_teacher.teacher_id
JOIN courses
on course_teacher.course_id = courses.id
JOIN degrees
ON courses.degree_id = degrees.id
WHERE teachers.id =44;
```

4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome
```sql
SELECT students.name, students.surname, degrees.name 'nome corso', departments.name 'nome dipartimento'
FROM students
JOIN degrees
ON students.degree_id = degrees.id
JOIN departments
ON degrees.department_id = departments.id
ORDER BY students.name , students.surname;
```

5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
```sql
SELECT teachers.name 'nome insegnante', teachers.surname 'cognome insegnante', courses.name, degrees.name 'nome corso'
FROM teachers
JOIN course_teacher
ON teachers.id =  course_teacher.teacher_id
JOIN courses
ON course_teacher.course_id = courses.id
JOIN degrees
ON courses.degree_id = degrees.id;
```

6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)
```sql
SELECT DISTINCT departments.name, teachers.name, teachers.surname
FROM departments
JOIN degrees
ON departments.id = degrees.department_id
JOIN courses
ON degrees.id = courses.degree_id
JOIN course_teacher
ON courses.id = course_teacher.course_id
JOIN teachers
ON course_teacher.teacher_id = teachers.id
WHERE departments.name LIKE 'Dipartimento di matematica';
```


##### Bonus
7. Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.
```sql

```