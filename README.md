# Projeto Lógico de Banco de Dados - E-commerce

## Descrição
Este projeto cria um banco de dados lógico para um cenário de e-commerce utilizando MySQL.

## Script SQL

```sql
-- Criando banco de dados
CREATE DATABASE Ecommerce;
USE Ecommerce;

-- Tabela Cliente
CREATE TABLE Cliente (
    id_cliente INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(255) NOT NULL,
    tipo_cliente ENUM('PJ', 'PF') NOT NULL,
    cpf_cnpj VARCHAR(20) UNIQUE NOT NULL
);

-- Tabela Pedido
CREATE TABLE Pedido (
    id_pedido INT AUTO_INCREMENT PRIMARY KEY,
    id_cliente INT NOT NULL,
    data_pedido DATETIME DEFAULT CURRENT_TIMESTAMP,
    valor_total DECIMAL(10, 2),
    FOREIGN KEY (id_cliente) REFERENCES Cliente(id_cliente)
);

-- Tabela Produto
CREATE TABLE Produto (
    id_produto INT AUTO_INCREMENT PRIMARY KEY,
    nome_produto VARCHAR(255) NOT NULL,
    preco DECIMAL(10, 2) NOT NULL
);

-- Tabela Estoque
CREATE TABLE Estoque (
    id_estoque INT AUTO_INCREMENT PRIMARY KEY,
    id_produto INT NOT NULL,
    quantidade INT NOT NULL,
    FOREIGN KEY (id_produto) REFERENCES Produto(id_produto)
);

-- Tabela Fornecedor
CREATE TABLE Fornecedor (
    id_fornecedor INT AUTO_INCREMENT PRIMARY KEY,
    nome_fornecedor VARCHAR(255) NOT NULL,
    contato VARCHAR(255)
);

-- Tabela Fornecedor_Produto
CREATE TABLE Fornecedor_Produto (
    id_fornecedor INT,
    id_produto INT,
    PRIMARY KEY (id_fornecedor, id_produto),
    FOREIGN KEY (id_fornecedor) REFERENCES Fornecedor(id_fornecedor),
    FOREIGN KEY (id_produto) REFERENCES Produto(id_produto)
);

-- Tabela Pagamento
CREATE TABLE Pagamento (
    id_pagamento INT AUTO_INCREMENT PRIMARY KEY,
    id_pedido INT NOT NULL,
    forma_pagamento ENUM('Cartão', 'Boleto', 'Pix', 'Transferência') NOT NULL,
    valor_pagamento DECIMAL(10, 2) NOT NULL,
    FOREIGN KEY (id_pedido) REFERENCES Pedido(id_pedido)
);

-- Tabela Entrega
CREATE TABLE Entrega (
    id_entrega INT AUTO_INCREMENT PRIMARY KEY,
    id_pedido INT NOT NULL,
    status_entrega ENUM('Pendente', 'Em Transporte', 'Entregue') NOT NULL,
    codigo_rastreio VARCHAR(255),
    FOREIGN KEY (id_pedido) REFERENCES Pedido(id_pedido)
);
