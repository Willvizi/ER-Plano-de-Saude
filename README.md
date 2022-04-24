# ER-Plano-de-Saude
Projeto Let's Code plano de saude, modelagem de banco





CREATE TABLE produto (
    id int not null primary key identity generated always as identity,
    cod_ans int not null unique,
    descricao varchar(100),
    valor money
)

CREATE TABLE contrato (
    id int not null primary key identity generated always as identity,
    data_inicio date not null
)

CREATE TABLE cliente (
    id int not null primary key generated always as identity,
    nome varchar(100), 
    data_nascimento date,
    email varchar(100)
)

CREATE TABLE produto_contrato (
    id int not null primary key identity generated always as identity,
    contrato_id int not null,
    produto_id int not null
    constraint contrato_fk foreign key (contrato_id) references contrato(id),
    constraint produto_fk foreign key (produto_id) references produto(id)
)

CREATE TABLE contrato_cliente (
    id int not null primary key identity generated always as identity,
    contrato_id int not null,
    cliente_id int not null,
    constraint contrato_fk foreign key (contrato_id) references contrato(id),
    constraint cliente_fk foreign key (cliente_id) references cliente(id)
)

CREATE TABLE dependente (
    id int not null primary key identity generated always as identity,
    titular int not null,
    dependente int not null,
    contrato_id int not null,
    constraint titular_fk foreign key (titular) references cliente(id),
    constraint dependente_fk foreign key (dependente) references cliente(id),
    constraint contrato_fk foreign key (contrato_id) references contrato(id),
    constraint dependente_unique unique(titular, dependente)
)
