# SICADE---SISTEMA-DE-CADASTRA-ACADEMICO
**SICADE** é um projeto de banco de dados acadêmico desenvolvido em **SQL Server**, com o objetivo de centralizar as informações de uma instituição de ensino superior. Ele reúne dados de departamentos, cursos, disciplinas, professores, alunos, matrículas e horários, permitindo uma gestão acadêmica integrada.

---

## 🎯 Objetivo

Fornecer um modelo relacional funcional que possa ser usado para fins educacionais, acadêmicos ou como base para sistemas acadêmicos maiores.

---

## 📚 Estrutura do Banco de Dados

O sistema é composto pelas seguintes tabelas:

- **Departamentos**: Informações dos departamentos acadêmicos.
- **Cursos**: Associados aos departamentos.
- **Disciplinas**: Vinculadas aos cursos.
- **Professores**: Relacionados aos departamentos.
- **Alunos**: Matriculados nos cursos.
- **Matrículas**: Relação entre alunos e disciplinas.
- **Horários**: Organização das aulas (disciplina + professor + sala + dia/horário).

---

## 🛠️ Tecnologias

- **SGBD:** SQL Server  
- **Ferramenta:** SQL Server Management Studio (SSMS)  
- **Linguagem:** T-SQL

---

## 📁 Organização dos Scripts

- `CREATE TABLE`: Estruturação de todas as tabelas com chaves primárias e estrangeiras.
- `INSERT INTO`: Dados de exemplo para testar o sistema.

---

## 🚀 Como usar

1. Abra o SQL Server Management Studio (SSMS).
2. Crie um novo banco de dados (ex: `SICADE`).
3. Execute os scripts SQL (estrutura e inserts).
4. Faça consultas conforme necessário.

---

## 📌 Codigo

```sql

-- 1. Departamentos
CREATE TABLE Departamentos (
    departamento_id INT PRIMARY KEY IDENTITY(1,1),
    nome VARCHAR(100) NOT NULL,
    sigla VARCHAR(10),
    descricao TEXT,
    email_contato VARCHAR(100),
    telefone VARCHAR(20),
    campus VARCHAR(100)
);

-- 2. Cursos
CREATE TABLE Cursos (
    curso_id INT PRIMARY KEY IDENTITY(1,1),
    nome VARCHAR(100) NOT NULL,
    grau VARCHAR(20),
    departamento_id INT NOT NULL,
    FOREIGN KEY (departamento_id) REFERENCES Departamentos(departamento_id)
);

-- 3. Disciplinas
CREATE TABLE Disciplinas (
    disciplina_id INT PRIMARY KEY IDENTITY(1,1),
    nome VARCHAR(100) NOT NULL,
    carga_horaria INT NOT NULL,
    curso_id INT NOT NULL,
    FOREIGN KEY (curso_id) REFERENCES Cursos(curso_id)
);

-- 4. Professores
CREATE TABLE Professores (
    professor_id INT PRIMARY KEY IDENTITY(1,1),
    nome VARCHAR(100) NOT NULL,
    email VARCHAR(100),
    departamento_id INT NOT NULL,
    FOREIGN KEY (departamento_id) REFERENCES Departamentos(departamento_id)
);

-- 5. Alunos
CREATE TABLE Alunos (
    aluno_id INT PRIMARY KEY IDENTITY(1,1),
    nome VARCHAR(100) NOT NULL,
    email VARCHAR(100),
    data_ingresso DATE,
    curso_id INT NOT NULL,
    FOREIGN KEY (curso_id) REFERENCES Cursos(curso_id)
);

-- 6. Matrículas
CREATE TABLE Matriculas (
    matricula_id INT PRIMARY KEY IDENTITY(1,1),
    aluno_id INT NOT NULL,
    disciplina_id INT NOT NULL,
    semestre VARCHAR(10),
    nota_final DECIMAL(4,2),
    FOREIGN KEY (aluno_id) REFERENCES Alunos(aluno_id),
    FOREIGN KEY (disciplina_id) REFERENCES Disciplinas(disciplina_id)
);

-- 7. Horários
CREATE TABLE Horarios (
    horario_id INT PRIMARY KEY IDENTITY(1,1),
    disciplina_id INT NOT NULL,
    professor_id INT NOT NULL,
    sala VARCHAR(20),
    dia_semana VARCHAR(15),
    horario_inicio TIME,
    horario_fim TIME,
    FOREIGN KEY (disciplina_id) REFERENCES Disciplinas(disciplina_id),
    FOREIGN KEY (professor_id) REFERENCES Professores(professor_id)
);



INSERT INTO Departamentos (nome, sigla, descricao, email_contato, telefone, campus)
VALUES 
('Departamento de Computação', 'COMP', 'Departamento responsável pelos cursos de tecnologia.', 'comp@universidade.edu.br', '(11) 1234-5678', 'Campus Centro'),
('Departamento de Letras', 'LET', 'Área de linguística e literatura.', 'letras@universidade.edu.br', '(11) 8765-4321', 'Campus Sul');


INSERT INTO Cursos (nome, grau, departamento_id)
VALUES
('Engenharia de Software', 'Bacharelado', 1),
('Letras - Português', 'Licenciatura', 2);


INSERT INTO Disciplinas (nome, carga_horaria, curso_id)
VALUES
('Estrutura de Dados', 60, 1),
('Algoritmos e Programação', 60, 1),
('Literatura Brasileira', 60, 2),
('Linguística I', 45, 2);


INSERT INTO Professores (nome, email, departamento_id)
VALUES
('Maria Andrade', 'maria.andrade@universidade.edu.br', 1),
('Carlos Silva', 'carlos.silva@universidade.edu.br', 2);


INSERT INTO Alunos (nome, email, data_ingresso, curso_id)
VALUES
('João Pereira', 'joao.pereira@aluno.edu.br', '2023-02-15', 1),
('Ana Souza', 'ana.souza@aluno.edu.br', '2024-03-10', 2);


INSERT INTO Matriculas (aluno_id, disciplina_id, semestre, nota_final)
VALUES
(1, 1, '2024-1', 8.5),  -- João em Estrutura de Dados
(1, 2, '2024-1', 9.0),  -- João em Algoritmos
(2, 3, '2024-1', 7.8),  -- Ana em Literatura Brasileira
(2, 4, '2024-1', 8.2);  -- Ana em Linguística


INSERT INTO Horarios (disciplina_id, professor_id, sala, dia_semana, horario_inicio, horario_fim)
VALUES
(1, 1, 'Lab 101', 'Segunda-feira', '08:00', '10:00'),
(2, 1, 'Lab 102', 'Quarta-feira', '10:00', '12:00'),
(3, 2, 'Sala 201', 'Terça-feira', '14:00', '16:00'),
(4, 2, 'Sala 202', 'Quinta-feira', '16:00', '18:00');

