# mysql-senac
create database senac;

use senac;

create table gestor(
matriculaGestor int primary key not null unique,
nome varchar(255) not null,
sobrenome varchar(255) not null,
cpf char(15) not null unique,
dataNascimento date,
area_formacao varchar(100) not null,
titulacao varchar(100) not null,
email_insti varchar(200) not null,
senha varchar(100) not null,
telefone char(20) not null

);

CREATE TABLE ENDERECO(
ID INT PRIMARY KEY AUTO_INCREMENT,
RUA VARCHAR(250),
CEP CHAR(15),
COMPLEMENTO VARCHAR(150),
matriculaGestor int, 
matriculaCoordenador int, 
id_supervisor int,
matriculaProfessor int, 
matriculaAluno int
);

create table coordenador(
matriculaCoordenador int primary key not null unique,
nome varchar(255) not null,
sobrenome varchar(255) not null,
cpf char(15) not null unique,
rg char(10) not null unique,
dataNascimento date,
area_formacao varchar(100) not null,
titulacao varchar(100) not null,
email_insti varchar(200) not null,
senha varchar(100) not null,
telefone char(20) not null

);


create table supervisor(
id_supervisor int auto_increment primary key,
nome varchar(255) not null,
sobrenome varchar(255) not null,
cpf char(15) not null unique,
rg char(10) not null unique,
dataNascimento date,
area_formacao varchar(100) not null,
especializacao char(70) not null, 
titulacao varchar(100) not null,
email_insti varchar(200) not null,
senha varchar(100) not null,
telefone char(20) not null

);


create table professor(
matriculaProfessor int primary key not null unique,
email_insti varchar(200) not null,
nome varchar(255) not null,
sobrenome varchar(255) not null,
cpf char(15) not null unique,
rg char(10) not null unique,
dataNascimento date,
especializacao char(70) not null, 
titulacao varchar(100) not null,
senha varchar(100) not null,
telefone char(20) not null,
area_formacao varchar(100) not null
);


create table aluno(
matriculaAluno int primary key not null unique,
nome varchar(255) not null,
sobrenome varchar(255) not null,
cpf char(15) not null unique,
dataNascimento date,
email_insti varchar(200) not null,
senha varchar(100) not null,
telefone char(20) not null

);


create table responsavel(
id_resp int auto_increment primary key,
matriculaAluno int,
nome varchar(255) not null,
sobrenome varchar(255) not null,
cpf char(15) not null unique,
rg char(10) not null unique,
dataNascimento date,
email varchar(200) not null,
telefone char(20) not null,
FOREIGN KEY (matriculaAluno) REFERENCES aluno(matriculaAluno)
);

create table turma(
id_turma int auto_increment primary key,
matriculaCoordenador int,
id_supervisor int,
matriculaAluno int,
ano char(10) not null,
turno varchar(50) not null,
quantidadeAlunos int not null,
FOREIGN KEY (matriculaCoordenador) REFERENCES coordenador(matriculaCoordenador),
FOREIGN KEY (id_supervisor) REFERENCES supervisor(id_supervisor),
FOREIGN KEY (matriculaAluno) REFERENCES aluno(matriculaAluno)
);

create table questoes(
id_questoes int auto_increment primary key,
matriculaProfessor int,
id_materias int,
nivel char(50) not null,
numeroQuetoes varchar(200) not null,
FOREIGN KEY (matriculaProfessor) REFERENCES professor(matriculaProfessor ),
FOREIGN KEY (id_materias ) REFERENCES materias(id_materias )
);

create table prova(
id_prova int auto_increment primary key,
matriculaProfessor int,
id_questoes int,
id_materias int,
matriculaAluno int,
materias char(70) not null,
FOREIGN KEY (matriculaProfessor) REFERENCES professor(matriculaProfessor),
FOREIGN KEY (id_questoes) REFERENCES questoes(id_questoes),
FOREIGN KEY (id_materias) REFERENCES materias(id_materias),
FOREIGN KEY (matriculaAluno) REFERENCES aluno(matriculaAluno)
); 



create table materias(
id_materias int auto_increment primary key,
matriculaProfessor int,
matriculaAluno int,
materias char(70) not null,
FOREIGN KEY (matriculaProfessor) REFERENCES professor(matriculaProfessor),
FOREIGN KEY (matriculaAluno) REFERENCES aluno(matriculaAluno)
); 

create table nota(
id_nota int auto_increment primary key,
matriculaAluno int,
id_materias int,
nota char(5) not null,
materia char(50)  not null,
FOREIGN KEY (id_materias) REFERENCES materias(id_materias ),
FOREIGN KEY (matriculaAluno) REFERENCES aluno(matriculaAluno)
);

create table frequencia(
id_frequencia int auto_increment primary key,
matriculaAluno int,
id_turma int,
freqencia char(1),
dataProva date,
FOREIGN KEY (matriculaAluno) REFERENCES aluno(matriculaAluno),
FOREIGN KEY (id_turma) REFERENCES turma(id_turma)
);
show tables;
