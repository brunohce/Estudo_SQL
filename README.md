# Estudo SQL utilizando PostgreSQL

## Comandos básicos SQL
<details>
<summary>Alguns comandos básicos que estou rodando no estudo de SQL utilizando tabelas criadas manualmente</summary>

#### Criar tabela

Para criar uma tabela com o nome science_class com as colunas enrollment_no, name e science marks
```
create table science_class (enrollment_no INT, name VARCHAR, science_Marks INT);
  ```
#### Inserir dados
```
insert into science_class values (1, 'Ana', 90), (2, 'Bruno',100), (3,'Carlos',84),(4,'Daniela',95);
```
#### Selecionar 

Selecionar todas as colunas usando o *:
```
select * from science_class;
```
Selecionar alunos com nota maior que 90 usando where:
```
select * from science_class where science_marks>90;
```
Selecionar somente o nome dos alunos com nota maior que 90 usando where:
```
select name from science_class where science_marks>90;
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
```
```
select * from customer where city in ('Seattle', 'New York City', 'Fresno', 'Chicado') ;
```
|customer_id|customer_name|segment|age|country|city|state|postal_code|region|
|-----------|-------------|-------|---|-------|----|-----|-----------|------|
|IM-15070|Irene Maddox|Consumer|66|United States|Seattle|Washington|98103|West|
|JM-15265|Janet Molinari|Corporate|23|United States|New York City|New York|10024|East|
|HM-14980|Henry MacAllister|Consumer|35|United States|New York City|New York|10009|East|
|.
|.

#### Selecionar clientes por idade usando WHERE e BETWEEN e NOT

Idade entre 20 e 50<br/>
```
select * from customer where age between 20 and 50  order by age asc ;
```
|customer_id|customer_name|segment|age|country|city|state|postal_code|region|
|-----------|-------------|-------|---|-------|----|-----|-----------|------|
|BE-11335|Bill Eplett|Home Office|20|United States|Jackson|Michigan|49201|Central|
|DK-13150|David Kendrick|Corporate|20|United States|Decatur|Illinois|62521|Central|
|FP-14320|Frank Preis|Consumer|20|United States|Los Angeles|California|90008|West|
|.
|.

Idade não está entre 20 e 30<br/>
```
select * from customer where age not between 20 and 30  order by age asc ;
```
|customer_id|customer_name|segment|age|country|city|state|postal_code|region|
|-----------|-------------|-------|---|-------|----|-----|-----------|------|
|CC-12610|Corey Catlett|Corporate|18|United States|Philadelphia|Pennsylvania|19134|East|
|DM-13525|Don Miller|Corporate|18|United States|Houston|Texas|77070|Central|
|CC-12220|Chris Cortes|Consumer|18|United States|La Porte|Indiana|46350|Central|
|.
|.

#### Usando wildcards
_  Representa um caractere<br/>
% Representa zero ou mais caractereres


Clientes que o primeiro nome tem cinco letras e a cidade começa com L <br/>
```
select * from customer where customer_name like '_____ %' AND city like 'L%' order by customer_name asc
```
|customer_id|customer_name|segment|age|country|city|state|postal_code|region|
|-----------|-------------|-------|---|-------|----|-----|-----------|------|
|AB-10150|Aimee Bixby|Consumer|65|United States|Long Beach|New York|11561|East|
|BE-11410|Bobby Elias|Consumer|54|United States|Lancaster|Ohio|43130|East|
|BT-11440|Bobby Trafton|Consumer|20|United States|Littleton|Colorado|80122|West|
|.
|.


Clientes que o primeiro nome tem cinco letras e a cidade não começa com A <br/>
```
select * from customer where customer_name like '_____ %' AND city not like 'A%' order by city asc
```
|customer_id|customer_name|segment|age|country|city|state|postal_code|region|
|-----------|-------------|-------|---|-------|----|-----|-----------|------|
|CS-12250|Chris Selesnick|Corporate|59|United States|Bossier City|Louisiana|71111|South|
|BD-11635|Brian Derr|Consumer|42|United States|Bowling Green|Kentucky|42104|South|
|GT-14635|Grant Thornton|Corporate|19|United States|Burlington|North Carolina|27217|South|
|.
|.


Clientes que o primeiro nome tem cinco letras, a cidade começa com L e são dos estados de Ohio e Colorado <br/>
```
select * from customer where customer_name like '_____ %' AND 
city like 'L%' and state in ('Ohio', 'Colorado') order by customer_name asc;
```
|customer_id|customer_name|segment|age|country|city|state|postal_code|region|
|-----------|-------------|-------|---|-------|----|-----|-----------|------|
|BE-11410|Bobby Elias|Consumer|54|United States|Lancaster|Ohio|43130|East|
|BT-11440|Bobby Trafton|Consumer|20|United States|Littleton|Colorado|80122|West|
|FC-14245|Frank Carlisle|Home Office|20|United States|Lakewood|Ohio|44107|East|
|TZ-21580|Tracy Zic|Consumer|65|United States|Louisville|Colorado|80027|West|


#### Exercícios

Selecionar clientes distintos de cidades que são da região norte e sul<br/>
```
select distinct customer_name, city, region from customer where region in('North', 'East')
```
|customer_name|city|region|
|-------------|----|------|
|Gene McClure|Providence|East|
|Toby Braunhardt|Washington|East|
|Alejandro Ballentine|Lorain|East|
|.
|.


Selecionar todos os pedidos com valor entre 100 e 500<br/>
```
select * from sales where sales between 100 and 500
```

|order_line|order_id|order_date|ship_date|ship_mode|customer_id|product_id|sales|quantity|discount|profit|
|----------|--------|----------|---------|---------|-----------|----------|-----|--------|--------|------|
|1|CA-2016-152156|2016-11-08|2016-11-11|Second Class|CG-12520|FUR-BO-10001798|261.96|2|0.0|41.9136|
|10|CA-2014-115812|2014-06-09|2014-06-14|Standard Class|BH-11710|OFF-AP-10002892|114.9|5|0.0|34.47|
|14|CA-2016-161389|2016-12-05|2016-12-10|Standard Class|IM-15070|OFF-BI-10003656|407.976|3|0.2|132.5922|
|.
|.

Selecionar todos os clientes que o último nome tem 4 caracteres<br/>
```
select * from customer where customer_name like '% ____';
```
|customer_id|customer_name|segment|age|country|city|state|postal_code|region|
|-----------|-------------|-------|---|-------|----|-----|-----------|------|
|CG-12520|Claire Gute|Consumer|67|United States|Henderson|Kentucky|42420|South|
|DV-13045|Darrin Van Huff|Corporate|31|United States|Los Angeles|California|90036|West|
|PK-19075|Pete Kriz|Consumer|46|United States|Madison|Wisconsin|53711|Central|
|.
|.

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
|customer_id|customer_name|segment|age|country|city|state|postal_code|region|
|-----------|-------------|-------|---|-------|----|-----|-----------|------|
|AH-10195|Alan Haines|Corporate|67|United States|Tamarac|Florida|33319|South|
|AS-10240|Alan Shonely|Consumer|68|United States|Tampa|Florida|33614|South|
|AG-10525|Andy Gerbode|Corporate|69|United States|Saint Petersburg|Florida|33710|South|
|.
|.

#### Usando ORDER e LIMIT

O limit define quantas linhas vão ser retornadas. No exemplo usei a coluna age para ordenar. Os clientes com menores idades serão selecionados se usar a ordem asc. Os clientes com maiores idades serão selecionados se usar a ordem desc.
```
select * from customer where segment = 'Corporate' order by 4 asc limit 3
```
|customer_id|customer_name|segment|age|country|city|state|postal_code|region|
|-----------|-------------|-------|---|-------|----|-----|-----------|------|
|SP-20650|Stephanie Phelps|Corporate|18|United States|San Jose|California|95123|West|
|SC-20770|Stewart Carmichael|Corporate|18|United States|Decatur|Alabama|35601|South|
|MP-17965|Michael Paige|Corporate|18|United States|Lawrence|Massachusetts|1841|East|


#### Exercícios

Selecionar todas as vendas com desconto maior que zero ordenando por ordem decrescente de desconto
```
select * from sales where discount > 0 order by discount desc 
```

Selecionar as 3 primeiras linhas de vendas com desconto maior que zero ordenando por ordem decrescente de desconto
```
select * from sales where discount > 0 order by discount desc limit 3
```
|order_line|order_id|order_date|ship_date|ship_mode|customer_id|product_id|sales|quantity|discount|profit|
|----------|--------|----------|---------|---------|-----------|----------|-----|--------|--------|------|
|16|US-2015-118983|2015-11-22|2015-11-26|Standard Class|HP-14815|OFF-BI-10000756|2.544|3|0.8|-3.816|
|15|US-2015-118983|2015-11-22|2015-11-26|Standard Class|HP-14815|OFF-AP-10002311|68.81|5|0.8|-123.858|
|76|US-2017-118038|2017-12-09|2017-12-11|First Class|KB-16600|OFF-BI-10004182|1.248|3|0.8|-1.9344|


#### Usando COUNT e AS

AS é o nome que vai ser dado para a coluna ou tabela<br/>
Para contar o número de produtos vendidos e 
```
select count(*) as "Number of Products Sold" from sales
```
|Number of Products Sold|
|-----------------------|
|9994|


Para contar o número de produtos e de vendas (pode ter mais de um produto em uma venda)
```
select count(order_line) as "Number of Products Sold", count(distinct order_id) as "Number of Sales" from sales
```
|Number of Products Sold|Number of Sales|
|-----------------------|---------------|
|9994|5009|


Para ver qual cliente fez mais compras
```
select customer_id , count(distinct order_id) as "Number of Sales by Customer" from sales group by customer_id order by 2 desc
```
|customer_id|Number of Sales by Customer|
|-----------|---------------------------|
|EP-13915|17|
|EA-14035|13|
|CK-12205|13|


#### Usando SUM

Para calcular o lucro total
```
select sum(Profit) as "Total Profit" from sales
```
|Total Profit|
|------------|
|286397.0217000013|


Para calcular o lucro total de um produto específico
```
select sum(Profit) as "Total Profit" from sales where product_id = 'FUR-CH-10000454'
```
|product_id|Total Profit|
|----------|------------|
|FUR-CH-10000454|1927.442|

Para calcular o total de vendas um produto específico
```
select  product_id, sum(quantity) as "Total Quantity" from sales where product_id = 'FUR-CH-10000454' group by product_id 
```
|product_id|Total Quantity|
|----------|--------------|
|FUR-CH-10000454|51|




