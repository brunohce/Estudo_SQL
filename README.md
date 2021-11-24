# Comandos básicos SQL

Algumas queries que estou rodando no estudo de SQL utilizando tabelas criadas manualmente

#### Criar tabela

Criar uma tabela com o nome science_class com as colunas enrollment_no, name e science marks

create table science_class (enrollment_no INT, name VARCHAR, science_Marks INT);

#### Inserir dados

insert into science_class values (1, 'Ana', 90), (2, 'Bruno',100), (3,'Carlos',84),(4,'Daniela',95);

#### Selecionar 

Selecionar todos:

select * from science_class;

Selecionar melhores alunos usando where:

select * from science_class where science_marks>90;

#### Alterar dados

update science_class set  science_marks = 110 WHERE name = 'Bruno';

#### Deletar linhas

insert into science_class values (5, 'Evandro', 30);

delete from science_class where name = 'Evandro';

#### Alterar propriedade da coluna

alter table science_class rename column name to student_name;

#  Utilizando db Supermart <br/>Contêm tabelas customer, sales e products.

#### Selecionar clientes da Califórnia e NY
select * from customer where state in ('California', 'New York');

#### Selecionar clientes com idades entre 20 e 50 ordenando por idade
select * from customer where age between 20 and 50  order by age asc ;



