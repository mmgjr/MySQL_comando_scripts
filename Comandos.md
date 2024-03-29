

create database Cadastro
	default character set utf8
	default collate utf8_general_ci;


create table pessoas(
id int not null auto_increment,
nome varchar(30) not null,
nascimento date,
sexo enum('M','F'),
peso decimal(5,2),
altura decimal(3,2),
nacionalidade varchar(20) default 'Brasil',
primary key (id)
)default charset = utf8;



insert into pessoas(
nome,nascimento,sexo,peso,altura,nacionalidade)
values(
'Godofredo','1984-01-02','M','78.5','1.83','Brasil');
insert into pessoas(
nome,nascimento,sexo,peso,altura,nacionalidade)
values(
'Maria','1999-12-02','F','55.5','1.63','Portugal');
insert into pessoas(
nome,nascimento,sexo,peso,altura,nacionalidade)
values(
'Creauza','1920-12-30','F','50.2','1.65',default);
insert into pessoas(
nome,nascimento,sexo,peso,altura,nacionalidade)
values(
'Adalgiza','1930-11-02','F','63.2','1.75','Irlanda');

insert into pessoas(
nome,nascimento,sexo,peso,altura,nacionalidade)
values(
'Ana','1986-01-02','F','63.2','1.75','Brasil'),
(
'Pedro','1930-06-12','M','83.2','1.89',default),
(
'Janaína','1988-05-22','F','53.2','1.65','EUA');

/*Mudando o nome da coluna de uma tabela*/
ALTER TABLE nomes_clientes 
    CHANGE primeiro_nome nome VARCHAR(255) NOT NULL;

alter table pessoas add column profissao varchar(10);

alter table pessoas drop column profissao;

alter table pessoas add column profissao varchar(10) after nome;
alter table pessoas add column codigo int first;

desc pessoas; /*confirmando a valor de profissão*/
alter table pessoas modify column profissao varchar(20) not null default '';
desc pessoas; /*verificando a modificação*/

alter table pessoas change column profissao prof varchar(20) not null default '';
alter table pessoas change column prof profissao varchar(20) not null default '';


alter table pessoas rename to gafanhotos; /*Renomear o nome da tabela*/

ALTER TABLE SuaTabela
ADD CONSTRAINT suaConstraint UNIQUE (campo(os));

create table if not exists cursos (
nome varchar(30) not null unique,
descricao text,
carga int unsigned,
totalaulas int,
ano year default '2019'
)default charset = utf8;

alter table cursos add column idcurso int first;
alter table cursos add primary key (idcursos);

insert into cursos values
('1','HTML4','Curso de HTML5','40','37','2014'),
('2','Algoritmos','Lógica de Programação','20','15','2014'),
('3','Photoshop','Dicas de Photoshop CC','10','8','2014'),
('4','PGP','Curso de PHP para iniciantes','40','20','2010'),
('5','Jarva','Introdução à Linguagem Java','10','29','2000'),
('6','MySQL','Banco de Dados MySQL','30','15','2016'),
('7','Word','Curso Completo de Word','40','30','2018'),
('8','Sapateado','Danças Rítmicas','40','30','2018'),
('9','Cozinha Árabe','Aprenda a fazer Kibe','40','30','2018'),
('10','YouTuber','Gerar polêmica e ganhar inscritos','5','2','2018');


update cursos set nome = 'HTML5' where idcurso = '1';
update cursos set nome = 'PHP', ano = '2015' where idcurso = '4'; 
update cursos set nome = 'Java', carga = '40', ano = '2015' where idcurso = '5' limit 1;

/*apagando linha do banco*/
delete from cursos where idcurso = '8';

/*Apagar todos os dados da tabela*/
truncate table cursos;


/*Mostrar os comando usados para criar a tabela*/
show create table amigos; /*mostra todos os comando usados para criar a tabela amigos*/
show create database exemplo;/*Mesma coisa mas mostrando os comando que criaram o banco de dados*/

/*Tipos de buscas*/

select * from cursos order by nome desc; /*decrescente*/
select * from cursos order by nome asc; /*crescente*/

select nome,carga,ano from cursos order by nome;

desc cursos; /*olhar a descrição da tabela*/

select * from cursos where ano = '2016' order by nome;

select nome,descricao from cursos where ano <= '2015' order by nome;

select nome,ano from cursos where ano between 2014 and 2016;

select nome,ano from cursos where ano between 2014 and 2016 order by ano desc,nome asc;

select * from cursos where carga > 35 and totalaulas < 30 order by nome;


select * from cursos where nome like 'P%';/*Traz todos os cursos com nome que começam com 'P'*/
select * from cursos where nome like '%A';/*Terminam com a letra A*/
select * from cursos where nome like '%A%';/*com A em qualquer lugar*/
select * from cursos where nome not like '%A%';/* traz todos os cursos onde não tenha a palavra A*/

update cursos set nome = 'PáOO' where idcruso = '9';

select * from cursos where nome like 'ph%p%';	
select * from cursos where nome like 'ph%p_';
select * from cursos where nome like 'p_p%';

select distinct nacionalidade from gafanhotos order by nacionalidade; /*traz apenas uma nacionalidade de cada*/
select count(*) from cursos;
select count(*) from cursos where carga > 40;

select max(carga) from cursos;


select max(totaulas) from cursos where ano='2016';
select nome,min(totaulas) from cursos where ano='2016';

select avg(totaulas) from cursos where ano = '2016';

select carga from cursos group by carga;

select carga,count(nome) from cursos group by carga;

select totaulas,count(*) from cursos GROUP by totaulas ORDER by totaulas;

select carga,count(nome) from cursos where totaulas = 30 GROUP by carga;

select carga,count(nome) from cursos where carga GROUP by (nome) > 3;
select ano,count(*) from cursos GROUP by ano order by count(*) desc;
select ano,count(*) from cursos GROUP by ano HAVING count(ano) >=5 order by count(*) desc;

select ano, count(*) from cursos where totaulas > 30 group by ano HAVING ano > 2013 order by count(*) desc;

select avg(carga) from cursos;

select carga,count(*) from cursos where ano > 2015 group by carga having carga > (select avg(carga) from cursos);

select sexo,count(*) from gafanhotos where nascimento > '2005-01-01' group by sexo;

select nacionalidade,count(*) as quantidade from gafanhotos where nacionalidade not like 'Brasil' group by nacionalidade having quantidade > 3 ORDER by quantidade;

/*Média altura das pessoas*/
SELECT AVG(altura) from gafanhotos; /*MÉDIA=1.664918*/
/*Buscando todas as pessoas que tem altura acima da média*/
select altura from gafanhotos where altura > (SELECT AVG(altura) from gafanhotos);
/*Quantidade de pessoas com altura acima da média*/
select count(altura) from gafanhotos where altura > (SELECT AVG(altura) from gafanhotos);
/*Busca quantidade de pessoas por altura com média acima de 1.6 que foi a média achada*/
select altura,count(*) from gafanhotos where altura > (SELECT AVG(altura) from gafanhotos) GROUP by altura;

/*Um lista agrupada pela altura dos gafanhotos,mostrando quantas pessoas pesam mais de 100KG
e que estão acima da média de altura de todos os cadastrados*/
select altura,count(*) from gafanhotos where peso > 100 and altura > (SELECT AVG(altura) from gafanhotos) GROUP by altura;


/*Adicionado Chave estrangeira*/
alter table gafanhotos add COLUMN cursopreferido int;
alter table gafanhotos add foreign key (cursopreferido) references cursos(idcurso);

/*Atribuindo os campos*/
update gafanhotos set cursopreferido='6' where id='1';

/*Iniciando JOIN*/
select nome, cursopreferido from gafanhotos;
select nome, ano from cursos;

select gafanhotos.nome,gafanhotos.cursopreferido,cursos.nome,cursos.ano 
from gafanhotos join cursos on cursos.idcurso=gafanhotos.cursopreferido 
order by gafanhotos.nome;

/*INNER JOIN pega todas as relações e ignora os casos sem relação*/
select g.nome,c.nome,c.ano from gafanhotos as g inner join cursos as c
on c.idcurso = g.cursopreferido order by g.nome;

/*OUTER JOIN pega todos os casos*/
select gafanhotos.nome,gafanhotos.cursopreferido,cursos.nome,
cursos.ano from gafanhotos outer join cursos on cursos.idcurso=gafanhotos.cursopreferido
order by gafanhotos.nome;

/*LEFT JOIN-> dá preferência à tabela da esquerda*/
/*RIGHT JOIN-> dá preferência à tabela da direita*/


/*Criando tabela intermediária para relação de N->N*/
create table gafanhotos_assiste_curso(
id int not null auto_increment,
data date,
idgafanhoto int,
idcurso int,
primary key (id),
foreign key (idgafanhoto) references gafanhotos(id),
foreign key (idcurso) references cursos(idcurso)
)default charset = utf8;

insert into gafanhotos_assiste_curso values (
default,'2014-03-01','1','2'),(default,'2015-12-22','3','6'),
(default,'2014-01-01','22','12'),(default,'2016-05-12','1','19');

select * from gafanhotos as g join gafanhotos_assiste_curso a
on g.id=a.idgafanhoto;

select g.nome,c.nome from gafanhotos as g join gafanhotos_assiste_curso a
on g.id=a.idgafanhoto join cursos c on c.idcurso=a.idcurso
order by g.nome;
