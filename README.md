# Estudo_SQL

Algumas queries que estou rodando no estudo de SQL utilizando tabelas criadas manualmente e db Supermart.

## Criar tabela

Criar uma tabela com o nome science_class com as colunas enrollment_no, name e science marks

create table science_class (enrollment_no INT, name VARCHAR, science_Marks INT);

## Inserir dados

insert into science_class values (1, 'Ana', 90), (2, 'Bruno',100), (3,'Carlos',84),(4,'Daniela',95);

## Selecionar 

Selecionar todos
select * from science_class;

Selecionar melhores alunos
select * from science_class where science_marks>90;

## Alterar dados

update science_class set  science_marks = 110 WHERE name = 'Bruno';

## Deletar linhas

insert into science_class values (5, 'Evandro', 30);
delete from science_class where name = 'Evandro';

## Alterar propriedade da coluna

alter table science_class rename column name to student_name;
