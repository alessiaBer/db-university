<!-- 
Modellizzare la struttura di un database per memorizzare tutti i dati riguardanti una università:
- sono presenti diversi Dipartimenti (es.: Lettere e Filosofia, Matematica, Ingegneria ecc.);
- ogni Dipartimento offre più Corsi di Laurea (es.: Civiltà e Letterature Classiche, Informatica, Ingegneria Elettronica ecc..)
- ogni Corso di Laurea prevede diversi Corsi (es.: Letteratura Latina, Sistemi Operativi 1, Analisi Matematica 2 ecc.);
- ogni Corso può essere tenuto da diversi Insegnanti;
- ogni Corso prevede più appelli d'Esame;
- ogni Studente è iscritto ad un solo Corso di Laurea;
- ogni Studente può iscriversi a più appelli di Esame;
- per ogni appello d'Esame a cui lo Studente ha partecipato, è necessario memorizzare il voto ottenuto, anche se non sufficiente.
Pensiamo a quali entità (tabelle) creare per il nostro database e cerchiamo poi di stabilirne le relazioni.
Infine, andiamo a definire le colonne e i tipi di dato di ogni tabella.
 -->

## entity:
- dipartimento
- corso di laurea
- corso
- insegnante
- appello
- studente
- esame



 ## Tables:
- dipartimenti
- corsi di laurea
- corsi
- insegnanti 
- appelli 
- studenti 
- esami 

### Tables departments
- id  PK, AI, UNIQUE, BIGINT, UNSIGNED, INDEX
- name VARCHAR(50)
- coordinators VARCHAR(50)

### Tables bachelor courses 
- id PK , AI , UNIQUE, BIGINT, UNSIGNED, INDEX
- department_id   FK, AI, UNIQUE, BIGINT, UNSIGNED, INDEX
- name VARCHAR(50)

### Tables courses
- id  PK, AI, UNIQUE, BIGINT, UNSIGNED, INDEX
- bachelor_id FK, AI, UNIQUE, BIGINT, UNSIGNED, INDEX
- name VARCHAR(50)
- duration VARCHAR(25)
- cfu TINYINT
- teacher_id VARCHAR(25)

## Tables teachers
- id  PK, AI, UNIQUE, BIGINT, UNSIGNED, INDEX
- name VARCHAR(50)
- lastname VARCHAR(50)
- address VARCHAR(100)
- email VARCHAR(50)
- phone VARCHAR(20)

## Tables exam calls
- id  PK, AI, UNIQUE, BIGINT, UNSIGNED, INDEX
- name VARCHAR(50)
- date TIMESTAMP
- type VARCHAR(50)
- max_students CHAR(3)
- place VARCHAR(50)
- teacher_id FK, AI, UNIQUE, BIGINT, UNSIGNED, INDEX

## Tables students
- id PK, AI, UNIQUE, BIGINT, UNSIGNED, INDEX
- name VARCHAR(50)
- lastname VARCHAR(50)
- address VARCHAR(100)
- email VARCHAR(50)
- phone VARCHAR(20)
- matriculation number CHAR(8)
- bachelor_courses_id FK, AI, UNIQUE, BIGINT, UNSIGNED, INDEX

## Tables exams
- id PK, AI, UNIQUE, BIGINT, UNSIGNED, INDEX
- name VARCHAR(50)
- number_test CHAR(10)
- result VARCHAR(20)
- student_id FK, AI, UNIQUE, BIGINT, UNSIGNED, INDEX

