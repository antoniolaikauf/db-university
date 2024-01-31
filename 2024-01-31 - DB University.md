## Repo
`db-university`

## Todo
Dopo aver testato le vostre query con `phpMyAdmin`, riportatele in un file `txt` o `md` e caricatelo nella vostra repo.

### Query
1. Selezionare tutti gli studenti nati nel 1990 (160)
```sql
SELECT *
FROM students
WHERE year(date_of_birth) = 1990;
```

2. Selezionare tutti i corsi che valgono più di 10 crediti (479)
```sql
SELECT *
FROM courses
WHERE cfu > 10;
```

3. Selezionare tutti gli studenti che hanno più di 30 anni
```sql
SELECT *
FROM students
WHERE year(now()) - 30 > year(date_of_birth);
```

4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di laurea (286)
```sql
SELECT *
FROM courses
WHERE period LIKE 'I semestre' AND year = 1;
```

5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del 20/06/2020 (21)
```sql
SELECT *
FROM exams
WHERE date = '2020-06-20'AND hour(hour) >= 14;
```

6. Selezionare tutti i corsi di laurea magistrale (38)
```sql
SELECT *
FROM degrees
WHERE level LIKE 'magistrale';
```

7. Da quanti dipartimenti è composta l'università? (12)
```sql
SELECT COUNT(id) as quantità_dei_dipartimenti
FROM departments;
```

8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)
```sql
SELECT COUNT(id) AS insegnanti_senza_numero
FROM teachers
WHERE phone IS null;
```
