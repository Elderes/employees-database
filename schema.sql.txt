-- Criação da tabela Funcionário
CREATE TABLE Funcionario (
    id SERIAL PRIMARY KEY, -- SERIAL substitui AUTO_INCREMENT no PostgreSQL
    nome VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    data_ingresso DATE NOT NULL,
    cargo VARCHAR(50) NOT NULL,
    salario NUMERIC(10, 2) NOT NULL -- NUMERIC é preferido em PostgreSQL para precisão em decimais
);

-- Criação da tabela Fornecedor
CREATE TABLE Fornecedor (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    categoria_fornecida VARCHAR(50) NOT NULL,
    validade_contrato DATE NOT NULL
);

-- Criação da tabela Produto
CREATE TABLE Produto (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    categoria VARCHAR(50) NOT NULL,
    validade DATE,
    quantidade INT NOT NULL
);

-- Relacionamento entre Fornecedor e Produto (Fornece)
-- Um fornecedor pode fornecer muitos produtos e um produto tem um único fornecedor
ALTER TABLE Produto
ADD fornecedor_id INT,
ADD CONSTRAINT fk_fornecedor FOREIGN KEY (fornecedor_id) REFERENCES Fornecedor(id);

-- Criação da tabela Calendário de Eventos
CREATE TYPE convocacao_enum AS ENUM ('Obrigatória', 'Opcional'); -- PostgreSQL usa ENUM como tipo de dado
CREATE TABLE CalendarioDeEventos (
    id SERIAL PRIMARY KEY,
    data DATE NOT NULL,
    tipo VARCHAR(50) NOT NULL,
    convocacao convocacao_enum NOT NULL
);
