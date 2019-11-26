# postgressql # pequenos testes realizados


# https://drive.google.com/open?id=1yswipZBabpn6nQjUu-r9XunhxHmzR-52


--CRIAÇÃO DA TABELA CATEGORIA_EVENTOS
CREATE TABLE CATEGORIA_EVENTOS
(
COD_CATEVEN SERIAL,
NOME_CATEVEN VARCHAR(40) NOT NULL,
PRIMARY KEY (COD_CATEVEN)
)


--CRIAÇÃO DA TABELA EVENTOS
CREATE TABLE EVENTOS
(
COD_EVENTO SERIAL,
NOME_EVENTO VARCHAR(60) NOT NULL,
AV_RUA_EVENTO VARCHAR(40) NOT NULL,
NUM_EVENTO SMALLINT NOT NULL,
CEP_EVENTO VARCHAR(10) NULL,
COMPLEMENTO_EVENTO VARCHAR(60) NULL,
BAIRRO_EVENTO VARCHAR(45) NOT NULL,
CIDADE_EVENTO VARCHAR(30) NOT NULL,
ESTADO_EVENTO VARCHAR(20) NOT NULL,
DATA_INICIO_EVENTO DATE NOT NULL,
HORA_INICIO_EVENTO TIME NOT NULL,
DATA_FIM_EVENTO DATE NOT NULL,
HORA_FIM_EVENTO TIME NULL,
COD_CATEVEN SMALLINT,
PRIMARY KEY (COD_EVENTO)
)


--ALTER TABLE NA TABELA EVENTOS
ALTER TABLE EVENTOS
ADD
FOREIGN KEY (COD_CATEVEN) REFERENCES CATEGORIA_EVENTOS(COD_CATEVEN)
ON UPDATE CASCADE
ON DELETE CASCADE


--CRIAÇÃO DA TABELA TIPO_PRODUTOS
CREATE TABLE TIPO_PRODUTOS
(
COD_TIPO SERIAL,
NOME_TIPO VARCHAR(30) NOT NULL,
PRIMARY KEY (COD_TIPO)
)


--CRIAÇÃO DA TABELA CATEGORIA_PRODUTOS
CREATE TABLE CATEGORIA_PRODUTOS
(
COD_CATPROD SERIAL,
NOME_CATPROD VARCHAR(30) NOT NULL,
PRIMARY KEY (COD_CATPROD)
)



--CRIAÇÃO DA TABELA PRODUTOS
CREATE TABLE PRODUTOS
(
COD_PROD SERIAL,
DESC_PROD VARCHAR(30) NOT NULL,
QTD_PROD SMALLINT NOT NULL,
UNID_PROD VARCHAR(3) NOT NULL,
PRECO_PROD FLOAT NOT NULL,
COD_TIPO SMALLINT,
COD_CATPROD SMALLINT,
PRIMARY KEY (COD_PROD)
)


--ALTER TABLE DA TABELA PRODUTOS
ALTER TABLE PRODUTOS
ADD
FOREIGN KEY (COD_TIPO) REFERENCES TIPO_PRODUTOS(COD_TIPO)
ON UPDATE CASCADE
ON DELETE CASCADE


--ALTER TABLE DA TABELA PRODUTOS
ALTER TABLE PRODUTOS
ADD
FOREIGN KEY (COD_CATPROD) REFERENCES CATEGORIA_PRODUTOS(COD_CATPROD)
ON UPDATE CASCADE
ON DELETE CASCADE



--CRIAÇÃO DA TABELA PRODUTOSxEVENTOS
CREATE TABLE PRODUTOS_EVENTOS
(
QTD_PRODEVEN SERIAL,
COD_PROD SMALLINT,
COD_EVENTO SMALLINT
)


--ALTER TABLE DA TABELA PRODUTOSxEVENTOS
ALTER TABLE PRODUTOS_EVENTOS
ADD
FOREIGN KEY (COD_PROD) REFERENCES PRODUTOS(COD_PROD)
ON UPDATE CASCADE
ON DELETE CASCADE


--ALTER TABLE DA TABELA PRODUTOSxEVENTOS
ALTER TABLE PRODUTOS_EVENTOS
ADD
FOREIGN KEY (COD_EVENTO) REFERENCES EVENTOS(COD_EVENTO)
ON UPDATE CASCADE
ON DELETE CASCADE



INSERT INTO TIPO_PRODUTOS VALUES (1, 'ALUGADO')
INSERT INTO TIPO_PRODUTOS VALUES (2, 'COMPRADO')

SELECT * FROM TIPO_PRODUTOS


--INSERT INTO NA TABELA CATEGORIA_PRODUTOS
INSERT INTO CATEGORIA_PRODUTOS VALUES (1, 'INFORMÁTICA')
INSERT INTO CATEGORIA_PRODUTOS VALUES (3, 'ELETRONICA')

SELECT * FROM CATEGORIA_PRODUTOS


--INSERT INTO NA TABELA PRODUTOS
INSERT INTO PRODUTOS VALUES (1, 'TEST', 13, 'KG', 3.99, 1, 1)
INSERT INTO PRODUTOS VALUES (4, 'TEST 1', 13, 'KG', 3.99, 2, 2)

SELECT * FROM PRODUTOS


--ALTER TABLE (COLUNA – TIPO DE DADOS)

-- ALTER TABLE PRODUTOS ALTER COLUMN COD_PROD TYPE SMALLINT

-- ALTER TABLE (nome da tabela) ALTER COLUMN (nome da coluna) (tipo de dados)



--ALTER TABLE (EXCLUIR CHAVE ESTRANGEIRA – DROP CONSTRAINT)

-- ALTER TABLE PRODUTOS DROP CONSTRAINT PRODUTOS_COD_CATPROD_FKEY

-- ALTER TABLE (nome da tabela) DROP CONSTRAINT (nome da chave estrangeira)
