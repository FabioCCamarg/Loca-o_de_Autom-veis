# EXERCÍCIOS BANCO DE DADOS  
## Descrição

/*Observe a tabela não normalizada de uma locadora de veículos e aplique a 3ª Forma normal;*/
	-- criando um banco de dados:
 
	create database bd;
	
-- tabela não normalizada :

	create table veiculos(
		cod_Locacao int auto_increment primary key,
		veiculo	varchar (50),
		cor	varchar(50),
		placa varchar (10),
		diaria decimal(9,2),	
		cliente varchar(50),
		cpf varchar(50),
		nascimento date,
		dia int,
		total decimal(9,2)
	);
    
  /*Faça o modelo lógico de banco de dados relacional;*/

  ![exer1](https://raw.githubusercontent.com/FabioCCamarg/Loca-o_de_Autom-veis/main/Loca%C3%A7%C3%A3o%20de%20Autom%C3%B3veis.png)
    
-- tabela normalizada: cliente

	create table cliente(
		cpf varchar(50) primary key,
		nome varchar(50) not null,
		nascimento date 
	);
    
-- tabela veiculo.

	create table veiculo(
		cod_locacao int auto_increment primary key,
		veiculo varchar(50),
		cor varchar(50),
		placa varchar(50),
		diaria decimal(9,2),
		cpf_cliente varchar(50),
		dia int,
		total decimal(9,2),
		foreign key (cpf_cliente) references cliente(cpf)
	);
    
-- inserindo registros na tabela cliente:

	insert into cliente (cpf, nome, nascimento)values
	('123.456.789-01','Ariano Sussuna','2022-05-21'),
	('543.765.987-23','Grace Hopper','2002-04-29'),
	('987.654.321-90','Richard Feynman','2001-10-12'),
	('432.765.678-67','Edgar Poe','1998-12-14'),
	('927.384.284-44','Gordon Freeman','1984-11-26');
    
-- verificando registros da tabela.

	select* from cliente;
    
-- inserindo registro na tabela veiculo.

	insert into veiculo (veiculo, cor , placa , diaria, cpf_cliente,dia, total) values
	('Fusca','Preto', 'WER-3456',30.00, '123.456.789-01',3, 90.00),
	('Variante','Rosa', 'FDS-8384',60.00, '543.765.987-23',7, 420.00),
	('Comodoro','Preto', 'CVB-9933',20.00, '987.654.321-90',1, 20.00),
	('Deloriam','Azul', 'FGH-2256',30.00, '123.456.789-01',3, 90.00),
	('Brasilia','amarela', 'DDI-3948',45.00, '927.384.284-44',7, 315.00);

-- verificando registro tabela veiculo.

	select *from veiculo;
    
/*Crie uma view que seleciona todas as locações e seus respectivos veículos e clientes.*/

	create view Todas_locacoes as
	select*from veiculo
	join cliente on cliente.cpf = veiculo.cpf_cliente;
    
    select * from Todas_locacoes;

-- Detalhes da View:

![exer1](https://raw.githubusercontent.com/FabioCCamarg/Loca-o_de_Autom-veis/main/detalhes_View.png)
