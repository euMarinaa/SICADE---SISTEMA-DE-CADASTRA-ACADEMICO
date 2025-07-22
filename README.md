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

## 📌 Exemplo de entidades

```sql
-- Exemplo: criar tabela de Departamentos
CREATE TABLE Departamentos (
    departamento_id INT PRIMARY KEY IDENTITY(1,1),
    nome VARCHAR(100) NOT NULL,
    sigla VARCHAR(10),
    descricao TEXT,
    email_contato VARCHAR(100),
    telefone VARCHAR(20),
    campus VARCHAR(100)
);
