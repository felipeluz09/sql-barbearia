DROP DATABASE IF EXISTS barbearia;
CREATE DATABASE barbearia;
USE barbearia;



USE barbearia;

--
DROP TABLE IF EXISTS Itens_Agendamento;
DROP TABLE IF EXISTS Agendamentos;
DROP TABLE IF EXISTS Servicos;
DROP TABLE IF EXISTS Profissionais;


USE barbearia;STS Clientes;

-- 
CREATE TABLE Clientes (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    cpf VARCHAR(14) UNIQUE NOT NULL,
    celular VARCHAR(20),
    email VARCHAR(100) UNIQUE NOT NULL,
    senha VARCHAR(255) NOT NULL
);

CREATE TABLE Profissionais (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    cpf VARCHAR(14) UNIQUE,
    celular VARCHAR(20),
    especialidade VARCHAR(50),
    comissao_percentual DECIMAL(5, 2) DEFAULT 0.00
);

CREATE TABLE Servicos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome_servico VARCHAR(80) NOT NULL,
    descricao TEXT,
    preco DECIMAL(10, 2) NOT NULL,
    duracao_minutos INT NOT NULL
);

CREATE TABLE Agendamentos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    id_cliente INT NOT NULL,
    id_profissional INT NOT NULL,
    data_hora DATETIME NOT NULL,
    status VARCHAR(20) DEFAULT 'Agendado',
    valor_total DECIMAL(10, 2) DEFAULT 0.00,
    CONSTRAINT fk_agendamentos_cliente FOREIGN KEY (id_cliente) REFERENCES Clientes(id) ON DELETE RESTRICT,
    CONSTRAINT fk_agendamentos_profissional FOREIGN KEY (id_profissional) REFERENCES Profissionais(id) ON DELETE RESTRICT
);

CREATE TABLE Itens_Agendamento (
    id INT AUTO_INCREMENT PRIMARY KEY,
    id_agendamento INT NOT NULL,
    id_servico INT NOT NULL,
    preco_unitario DECIMAL(10, 2) NOT NULL,
    quantidade INT DEFAULT 1,
    CONSTRAINT fk_itens_agendamento FOREIGN KEY (id_agendamento) REFERENCES Agendamentos(id) ON DELETE CASCADE,
    CONSTRAINT fk_itens_servico FOREIGN KEY (id_servico) REFERENCES Servicos(id) ON DELETE RESTRICT
);

-- 4. INSERIR DADOS NAS TABELAS (DML)
INSERT INTO Clientes (nome, cpf, celular, email, senha) VALUES 
('FELIPE', '155.455.766-55', '(42)889988767', 'FELIPE@GMAIL.COM', 'RHCUTYCUGYG'),
('MARTA', '244.566.877-66', '(41)998877665', 'MARTA@GMAIL.COM', 'ABXUTYCUGYG'),
('THIAGO', '355.677.988-77', '(11)987654321', 'THIAGO@GMAIL.COM', 'PLKUTYCUGYG'),
('AMANDA', '466.788.099-88', '(21)976543210', 'AMANDA@GMAIL.COM', 'QWEUTYCUGYG'),
('RODRIGO', '577.899.100-99', '(31)965432109', 'RODRIGO@GMAIL.COM', 'ZXCUTYCUGYG'),
('JULIANA', '688.900.211-00', '(51)954321098', 'JULIANA@GMAIL.COM', 'MNBUTYCUGYG'),
('LUCAS', '799.011.322-11', '(19)943210987', 'LUCAS@GMAIL.COM', 'POIUTYCUGYG'),
('BEATRIZ', '811.122.433-22', '(43)932109876', 'BEATRIZ@GMAIL.COM', 'LKJUTYCUGYG'),
('GABRIEL', '922.233.544-33', '(47)921098765', 'GABRIEL@GMAIL.COM', 'HGFUTYCUGYG'),
('LARISSA', '133.344.655-44', '(48)910987654', 'LARISSA@GMAIL.COM', 'DSAUTYCUGYG'),
('BRUNO', '244.455.766-55', '(42)909876543', 'BRUNO@GMAIL.COM', 'REWUTYCUGYG');

INSERT INTO Profissionais (nome, cpf, celular, especialidade, comissao_percentual) VALUES
('Carlos Andrade', '111.222.333-44', '(41)988112233', 'Barbeiro Master', 50.00),
('Eduardo Silva', '222.333.444-55', '(41)988223344', 'Especialista em Barba', 45.00),
('Marcos Paulo', '333.444.555-66', '(41)988334455', 'Cabeleireiro / Visagista', 50.00);

INSERT INTO Servicos (nome_servico, descricao, preco, duracao_minutos) VALUES
('Corte Masculino', 'Corte moderno com lavagem e finalização', 50.00, 30),
('Barba Completa', 'Modelagem de barba com toalha quente e óleo', 40.00, 30),
('Combo Corte + Barba', 'Serviço completo de corte e barba', 80.00, 50);

INSERT INTO Agendamentos (id_cliente, id_profissional, data_hora, status, valor_total) VALUES
(1, 1, '2026-08-26 10:00:00', 'Concluido', 80.00),
(2, 2, '2026-08-26 11:00:00', 'Agendado', 40.00);

INSERT INTO Itens_Agendamento (id_agendamento, id_servico, preco_unitario, quantidade) VALUES
(1, 3, 80.00, 1),
(2, 2, 40.00, 1);

-- 5. CONSULTAS E TESTES (DML)
SELECT * FROM Clientes;
SELECT email, senha FROM Clientes WHERE email = 'FELIPE@GMAIL.COM';
SELECT id, nome FROM Clientes WHERE id <= 5;

UPDATE Clientes
SET nome = 'felipe gabriel', email = 'FELIPE@EMAIL.COM'
WHERE id = 1;
