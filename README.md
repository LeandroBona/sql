# sql

-- Criando o banco de dados (se ainda não existir)

CREATE DATABASE IF NOT EXISTS escola;

-- Usando o banco de dados criado

USE escola;

-- Tabela Estudantes

CREATE TABLE Estudantes (
    id_estudante INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    data_nascimento DATE NOT NULL,
    endereco_completo VARCHAR(200),
    telefone VARCHAR(20),
    email VARCHAR(100),
   cpf varchar(11) not null
);

-- Tabela Cursos

CREATE TABLE Cursos (
    id_curso INT AUTO_INCREMENT PRIMARY KEY,
    nome_curso VARCHAR(100) NOT NULL,
    descricao TEXT,
    duracao VARCHAR(50),
    data_conclusao date,
    coordenador varchar(30) not null
);

-- Tabela Professores

CREATE TABLE Professores (
    id_professor INT AUTO_INCREMENT PRIMARY KEY,
    nome_professor VARCHAR(100) NOT NULL,
    email VARCHAR(100),
    telefone VARCHAR(20),
    departamento VARCHAR(100)
);


-- Tabela Matrículas

CREATE TABLE Matriculas (
    id_matricula INT AUTO_INCREMENT PRIMARY KEY,
    id_estudante INT NOT NULL,
    id_curso INT NOT NULL,
    data_matricula DATE NOT NULL,
    FOREIGN KEY (id_estudante) REFERENCES Estudantes(id_estudante),
    FOREIGN KEY (id_curso) REFERENCES Cursos(id_curso)
);

-- Tabela Disciplinas

CREATE TABLE Disciplinas (
    id_disciplina INT AUTO_INCREMENT PRIMARY KEY,
    nome_disciplina VARCHAR(100) NOT NULL,
    descricao TEXT,
    id_curso INT NOT NULL,
    id_professor int(11),
    FOREIGN KEY (id_professor) REFERENCES Professores(id_professor),
    FOREIGN KEY (id_curso) REFERENCES Cursos(id_curso)
);


-- Tabela Boletim Escolar

CREATE TABLE Boletim_Escolar (
    id_boletim INT AUTO_INCREMENT PRIMARY KEY,
    id_estudante INT NOT NULL,
    id_disciplina INT NOT NULL,
    nota DECIMAL(5, 2),
    ano INT,
    semestre INT,
    observacoes text,
    FOREIGN KEY (id_estudante) REFERENCES Estudantes(id_estudante),
    FOREIGN KEY (id_disciplina) REFERENCES Disciplinas(id_disciplina)
);

-- Tabela Agenda

CREATE TABLE Agenda (
    id_agenda INT AUTO_INCREMENT PRIMARY KEY,
    id_estudante INT NOT NULL,
    data DATE NOT NULL,
    descricao VARCHAR(200),
    id_evento int(11) not null,
   FOREIGN KEY (id_evento) REFERENCES Eventos(id_evento),
    FOREIGN KEY (id_estudante) REFERENCES Estudantes(id_estudante)
);



-- Tabela Eventos

CREATE TABLE Eventos (
    id_evento INT AUTO_INCREMENT PRIMARY KEY,
    nome_evento VARCHAR(100) NOT NULL,
    data_evento DATE NOT NULL,
    local VARCHAR(100),
    descricao TEXT,
    id_curso INT,
    FOREIGN KEY (id_curso) REFERENCES Cursos(id_curso)
);


INSERT INTO Estudantes (nome, data_nascimento, endereco_completo, telefone, email, cpf) VALUES
('João da Silva', '2001-05-12', 'Rua A, 123, Bairro Centro, Cidade X', '1234567890', 'joao.silva@email.com', '11122233344'),
('Maria Oliveira', '2002-08-25', 'Av. B, 456, Bairro Sul, Cidade Y', '0987654321', 'maria.oliveira@email.com', '22233344455'),
('Pedro Santos', '1999-11-30', 'Rua C, 789, Bairro Norte, Cidade Z', '1122334455', 'pedro.santos@email.com', '33344455566'),
('Ana Costa', '2000-02-15', 'Av. D, 321, Bairro Leste, Cidade W', '2233445566', 'ana.costa@email.com', '44455566677');


INSERT INTO Cursos (nome_curso, descricao, duracao, data_conclusao, coordenador) VALUES
('Engenharia de Software', 'Curso voltado para desenvolvimento de sistemas', '4 anos', '2024-12-20', 'Dr. Carlos Mendes'),
('Ciência da Computação', 'Curso de estudo profundo de computação e algoritmos', '4 anos', '2024-12-20', 'Dra. Helena Silva'),
('Análise e Desenvolvimento de Sistemas', 'Curso focado em análise e desenvolvimento de software', '3 anos', '2023-12-15', 'Prof. João Pereira');


INSERT INTO Professores (nome_professor, email, telefone, departamento) VALUES
('Carlos Mendes', 'carlos.mendes@email.com', '3344556677', 'Departamento de Computação'),
('Helena Silva', 'helena.silva@email.com', '4455667788', 'Departamento de Computação'),
('João Pereira', 'joao.pereira@email.com', '5566778899', 'Departamento de Sistemas');


INSERT INTO Disciplinas (nome_disciplina, descricao, id_curso, id_professor) VALUES
('Algoritmos', 'Estudo de algoritmos e estruturas de dados', 1, 1),
('Banco de Dados', 'Conceitos e práticas de banco de dados', 2, 2),
('Engenharia de Requisitos', 'Especificação e análise de requisitos de software', 1, 3);


INSERT INTO Matriculas (id_estudante, id_curso, data_matricula) VALUES
(1, 1, '2022-03-01'),
(2, 2, '2023-02-15'),
(3, 1, '2021-08-20'),
(4, 3, '2023-01-10');


INSERT INTO Boletim_Escolar (id_estudante, id_disciplina, nota, ano, semestre, observacoes) VALUES
(1, 1, 8.5, 2023, 1, 'Bom desempenho'),
(2, 2, 7.0, 2023, 1, 'Atenção nas próximas avaliações'),
(3, 1, 9.0, 2022, 2, 'Excelente'),
(4, 3, 6.5, 2023, 1, 'Precisa melhorar');


INSERT INTO Agenda (id_estudante, data, descricao, id_evento) VALUES
(1, '2023-09-10', 'Reunião de projeto final', 1),
(2, '2023-09-15', 'Apresentação de trabalho', 2),
(3, '2023-09-20', 'Entrega de relatório', 3),
(4, '2023-09-25', 'Prova final', 1);


INSERT INTO Eventos (nome_evento, data_evento, local, descricao, id_curso) VALUES
('Semana Acadêmica', '2023-09-10', 'Auditório A', 'Palestras e workshops para alunos de computação', 1),
('Hackathon', '2023-09-15', 'Laboratório B', 'Competição de desenvolvimento de software', 2),
('Seminário de Pesquisa', '2023-09-20', 'Sala de Conferências', 'Apresentação de pesquisas recentes', 3);

s9
