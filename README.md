# greenfarm
CREATE TABLE fazenda (
    id_fazenda INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    localizacao VARCHAR(100),
    tamanho DECIMAL(10,2),
    numero_resp VARCHAR(50),
    id_funcionario INT
);

-- Tabela: funcionario
CREATE TABLE funcionario (
    id_funcionario INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    funcao VARCHAR(50),
    status VARCHAR(20),
    id_fazenda INT NOT NULL,
    data_admissao DATE
);

-- Tabela: plantacao
CREATE TABLE plantacao (
    id_plantacao INT AUTO_INCREMENT PRIMARY KEY,
    tipo VARCHAR(50),
    area_plantada DECIMAL(10,2),
    status VARCHAR(20),
    id_fazenda INT NOT NULL
);

-- Tabela: equipamento
CREATE TABLE equipamento (
    id_equipamento INT AUTO_INCREMENT PRIMARY KEY,
    nome_equip VARCHAR(100),
    tipo_equip VARCHAR(50),
    data_aquisicao DATE,
    status_equip VARCHAR(20),
    local_equip VARCHAR(100),
    id_fazenda INT
);

-- Tabela: safra
CREATE TABLE safra (
    id_safra INT AUTO_INCREMENT PRIMARY KEY,
    rastreamento VARCHAR(100),
    quant_colhida DECIMAL(10,2),
    quantidade DECIMAL(10,2),
    data_plantio DATE,
    data_colheita DATE,
    id_equipamento INT,
    id_plantacao INT
);

-- Adição das chaves estrangeiras

-- funcionario -> fazenda
ALTER TABLE funcionario
ADD CONSTRAINT fk_funcionario_fazenda
FOREIGN KEY (id_fazenda) REFERENCES fazenda(id_fazenda);

-- fazenda -> funcionario (responsável)
ALTER TABLE fazenda
ADD CONSTRAINT fk_fazenda_funcionario
FOREIGN KEY (id_funcionario) REFERENCES funcionario(id_funcionario);

-- plantacao -> fazenda
ALTER TABLE plantacao
ADD CONSTRAINT fk_plantacao_fazenda
FOREIGN KEY (id_fazenda) REFERENCES fazenda(id_fazenda);

-- equipamento -> fazenda
ALTER TABLE equipamento
ADD CONSTRAINT fk_equipamento_fazenda
FOREIGN KEY (id_fazenda) REFERENCES fazenda(id_fazenda);

-- safra -> equipamento
ALTER TABLE safra
ADD CONSTRAINT fk_safra_equipamento
FOREIGN KEY (id_equipamento) REFERENCES equipamento(id_equipamento);

-- safra -> plantacao
ALTER TABLE safra
ADD CONSTRAINT fk_safra_plantacao
FOREIGN KEY (id_plantacao) REFERENCES plantacao(id_plantacao);
