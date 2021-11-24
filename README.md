# Estudo SQL utilizando PostgreSQL

## Comandos básicos SQL
<details>
<summary>Alguns comandos básicos que estou rodando no estudo de SQL utilizando tabelas criadas manualmente</summary>

#### Criar tabela

Criar uma tabela com o nome science_class com as colunas enrollment_no, name e science marks
```
create table science_class (enrollment_no INT, name VARCHAR, science_Marks INT);
  ```
#### Inserir dados
```
insert into science_class values (1, 'Ana', 90), (2, 'Bruno',100), (3,'Carlos',84),(4,'Daniela',95);
```
#### Selecionar 

Selecionar todos:
```
select * from science_class;
```
Selecionar melhores alunos usando where:
```
select * from science_class where science_marks>90;
```
#### Alterar dados
```
update science_class set  science_marks = 110 WHERE name = 'Bruno';
```
#### Deletar linhas
```
insert into science_class values (5, 'Evandro', 30);
delete from science_class where name = 'Evandro';
```
#### Alterar propriedade da coluna
```
alter table science_class rename column name to student_name;
```
</details>

#  Utilizando db Supermart com tabelas customer, sales e products.

#### Selecionar clientes por localidade usando WHERE e IN
```
select * from customer where state in ('California', 'New York');

select * from customer where city in ('Seattle', 'New York City', 'Fresno', 'Chicado') ;
```


#### Selecionar clientes por idade usando WHERE e BETWEEN e NOT

Idade entre 20 e 50<br/>
```
select * from customer where age between 20 and 50  order by age asc ;
```

Idade não está entre 20 e 30<br/>
```
select * from customer where age not between 20 and 30  order by age asc ;
```


#### Usando wildcards
_  Representa um caractere<br/>
% Representa zero ou mais caractereres


Clientes que o primeiro nome tem cinco letras e a cidade começa com L <br/>
```
select * from customer where customer_name like '_____ %' AND city like 'L%' order by customer_name asc
```

Clientes que o primeiro nome tem cinco letras e a cidade não começa com A <br/>
```
select * from customer where customer_name like '_____ %' AND city not like 'A%' order by city asc
```


Clientes que o primeiro nome tem cinco letras, a cidade começa com L e são dos estados de Ohio e Colorado <br/>
```
select * from customer where customer_name like '_____ %' AND 
city like 'L%' and state in ('Ohio', 'Colorado') order by customer_name asc;
```

#### Exercícios

Selecionar clientes distintos de cidades que são da região norte e sul<br/>
```
select distinct customer_name, city, region from customer where region in('North', 'East')
```

Selecionar todos os pedidos com valor entre 100 e 500<br/>
```
select * from sales where sales between 100 and 500
```

Selecionar todos os clientes que o último nome tem 4 caracteres<br/>
```
select * from customer where customer_name like '% ____';
```

#### Ordenamento

Pode ser feito ordem ascendente (ASC) ou descendente (desc) e utilizando um ou mais parâmetros<br/>

```
select * from customer where state = 'Florida' order by age asc ;

select * from customer where state = 'Florida'  order by customer_name asc, segment asc, age desc
```

Também é possível usar um index das colunas no lugar do nome da coluna. Nesse caso customer_name é a 2a coluna, segment a 3a e age a 4a, produzindo o mesmo resultado da query anterior
```
select * from customer where state = 'Florida'  order by 2 asc, 3 asc, 4 desc
```

