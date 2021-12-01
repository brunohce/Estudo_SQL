# Estudo SQL utilizando PostgreSQL

## SQL básico
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
|enrollment_no|name|science_marks|
|-------------|----|-------------|
|1|Ana|90|
|2|Bruno|100|
|3|Carlos|84|
|4|Daniela|95|

Selecionar alunos com nota maior que 90 usando where:
```
select * from science_class where science_marks>90;
```
	
|enrollment_no|name|science_marks|
|-------------|----|-------------|
|2|Bruno|100|
|4|Daniela|95|
  
Selecionar somente o nome dos alunos com nota maior que 90 usando where:
```
select name from science_class where science_marks>90;
```
|name|
|----|
|Bruno|
|Daniela|



#### Alterar dados
```
update science_class set  science_marks = 110 WHERE name = 'Bruno';
  select * from science_class
```
|enrollment_no|name|science_marks|
|-------------|----|-------------|
|1|Ana|90|
|3|Carlos|84|
|4|Daniela|95|
|2|Bruno|110|

#### Deletar linhas
```
insert into science_class values (5, 'Evandro', 30);
delete from science_class where name = 'Evandro';
```
#### Alterar propriedade da coluna
```
alter table science_class rename column name to student_name;
```
|enrollment_no|student_name|science_marks|
|-------------|------------|-------------|
|1|Ana|90|
|3|Carlos|84|
|4|Daniela|95|
|2|Bruno|110|

</details>

## SQL Intermediário
<details>
	<summary>Utilizando db Supermart com tabelas customer, sales e products.</summary>

#### WHERE e IN

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

#### WHERE e BETWEEN e NOT

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

#### Wildcards
Wildcards são utilizados para substituir caracteres em uma string, sendo que:
	
	
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

#### ORDER

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

#### ORDER e LIMIT

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


#### COUNT e AS

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


#### SUM

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

#### AVG

Para calcular um valor médio
```
select avg(age) "Average Customer Age" from customer c
```
|Average Customer Age|
|--------------------|
|44.4678436317780580|

Para encontrar os estados com consumidores em média mais jovens
```
select state, avg(age) as "Average Customer Age" from customer c group by state order by 2
```
|state|Average Customer Age|
|-----|--------------------|
|Kansas|20.0000000000000000|
|District of Columbia|24.0000000000000000|
|Arkansas|30.0000000000000000|

Valor médio pago em comissões considerando comissão de 10%
```
select avg(sales * 0.10) as "Average Comission Value" from sales
```
|Average Comission Value|
|-----------------------|
|22.985800083049867|


#### MAX e MIN

Para encontrar o valor da menor venda do mês de Junho de 2015
```
select min(sales) as "Minimum Sales Value from June 2015" from sales where order_date between '2015-06-01' and '2015-06-30'
```
|Minimum Sales Value from June 2015|
|----------------------------------|
|0.984|

Para encontrar o valor da maior venda do mês de Junho de 2015

```
select max(sales) as "Maximum Sales Value from June 2015" from sales where order_date between '2015-06-01' and '2015-06-30'
```
|Maximum Sales Value from June 2015|
|----------------------------------|
|3050.376|


#### Exercícios

Calcular o total de sales
```
select sum(sales) as "Sum of Sales" from sales
```
|Sum of Sales|
|------------|
|2297200.860299955|

Calcular o total de clientes da região norte com idade entre 20 e 30
```
select count(customer_id) from customer where region = 'North' and age between 20 and 30
```
|count|
|-----|
|0|

Calcular a idade média de clientes da região Leste
```
select avg(age) as "Average Customer Age from East Region" from customer c where region = 'East'
```
|Average Customer Age from East Region|
|-------------------------------------|
|44.3363636363636364|

Calcular a idade mínima e máxima de clientes da Filadélfia
```
select min(age) as "Minimum Customer Age from Philadelphia", max(age) as "Maximum Customer Age from Philadelphia" from customer c where city = 'Philadelphia'
```
|Minimum Customer Age from Philadelphia|Maximum Customer Age from Philadelphia|
|--------------------------------------|--------------------------------------|
|18|70|

#### Group by
(Já foi usado mas reforçado aqui)

Calcular o número de clientes em cada região
```
select region, count(distinct customer_id) as "Customer Count" from customer c group by region order by 2 desc
```
|region|Customer Count|
|------|--------------|
|West|255|
|East|220|
|Central|184|
|South|134|

Calcular a quantidade de itens vendidos por produto
```
select product_id, sum(quantity) as "Quantity Sold" from sales group by product_id order by 2 desc
```
|product_id|Quantity Sold|
|----------|-------------|
|TEC-AC-10003832|75|
|OFF-PA-10001970|70|
|OFF-BI-10001524|67|
|.
|.

Encontrar os clientes que mais gastam (total de compras)
```
select customer_id, count(distinct order_line) as "Number of Purchases", min(sales) as "Minimum Sales Value", 
avg(sales) as "Average Sales Value", max(sales) as "Maximum Sales Value", sum(sales) as "Total Sales Value"   
from sales group by customer_id order by 6 desc limit 5
```
|customer_id|Number of Purchases|Minimum Sales Value|Average Sales Value|Maximum Sales Value|Total Sales Value|
|-----------|-------------------|-------------------|-------------------|-------------------|-----------------|
|SM-20320|15|3.488|1669.5366666666666|22638.48|25043.05|
|TC-20980|12|7.312|1587.684833333333|17499.95|19052.217999999997|
|RB-19360|18|4.448|839.8521666666667|13999.96|15117.339|
|TA-21385|10|7.04|1459.562|11199.968|14595.619999999999|
|HL-15040|11|6.63|1170.2998181818182|10499.97|12873.297999999999|

#### HAVING

HAVING é usada para colunas agregadas e WHERE em colunas não agregadas.


Contar número de clientes por cidade e região e selecionar somente aquelas com mais de 10 clientes
```
select city, region, count(distinct customer_id) as "Customer Count" from customer c group by city, region having count(3) > 10 order by 3 desc 
```
|city|region|Customer Count|
|----|------|--------------|
|New York City|East|68|
|Los Angeles|West|58|
|Philadelphia|East|46|
|San Francisco|West|41|
|Seattle|West|31|
|Houston|Central|28|
|Chicago|Central|19|
|San Diego|West|13|
|Dallas|Central|13|
|Jacksonville|South|11|

#### Exercícios

Tabela com valor total em vendas $, total de itens vendidos, número de pedidos, menor valor de venda, média do valor de venda, maior valor de venda
```
select sum(sales) as "Total Sales in $", sum(quantity) as "Total Quantity", count(distinct order_id) as "Number of Orders",
min(sales) as "Minimum Sales Value", avg(sales) as "Average Sales Value", max(sales) as "Maximum Sales Value" from sales
```
|Total Sales in $|Total Quantity|Number of Orders|Minimum Sales Value|Average Sales Value|Maximum Sales Value|
|----------------|--------------|----------------|-------------------|-------------------|-------------------|
|2297200.860299955|37873|5009|0.444|229.8580008304938|22638.48|

Listar produtos com menos de 10 itens vendidos em ordem crescente
```
select product_id, sum(quantity) as "By Product Sales Quantity" from sales group by product_id having sum(quantity) < 10 order by 2 asc
```

|product_id|By Product Sales Quantity|
|----------|-------------------------|
|OFF-PA-10000048|1|
|TEC-MA-10003493|1|
|FUR-BO-10002206|1|
|.
|.

#### CASE WHEN

Funciona basicamente como o IF e ELSE.
Para classificar categoricamente a idade dos clientes
```
select customer_id, customer_name, age , case 
			when age<21 then 'Young'	
			when age>60 then 'Elderly' 
			else 'Adult'	
		end as Age_category	from customer;
```

|customer_id|customer_name|age|age_category|
|-----------|-------------|---|------------|
|CG-12520|Claire Gute|67|Elderly|
|DV-13045|Darrin Van Huff|31|Adult|
|SO-20335|Sean O'Donnell|65|Elderly|
|BH-11710|Brosina Hoffman|20|Young|
|.

Dá para contar o número de clientes em cada categoria
```
select count(case when age<=21 then 'Young' else null end) as "Young",
	   count(case when age between 22 and 59 then 'Adult' else null end) as "Adult",
	   count(case when age>=60 then 'Elderly' else null end) as "Elderly"
	  from customer;
```
|Young|Adult|Elderly|
|-----|-----|-------|
|66|546|181|
	
</details>

	
## SQL Avançado
<details>
	<summary>Utilizando db Supermart com tabelas customer, sales e products. </summary>



<br/>	
Criando tabelas com registros exclusivos
	
```
/*Creating sales table of year 2015*/

Create table sales_2015 as select * from sales where ship_date between '2015-01-01' and '2015-12-31';
select count(*) from sales_2015; --2131
select count(distinct customer_id) from sales_2015;--578

/* Customers with age between 20 and 60 */
create table customer_20_60 as select * from customer where age between 20 and 60;
select count (*) from customer_20_60;--597
```

#### Inner Join
Selecionar os clientes que estão em ambas tabelas. Tem de estar tanto na customer quanto sales.

```
select distinct customer_name from customer_20_60 c inner join sales_2015 s on c.customer_id = s.customer_id order by customer_name  
```
	
|customer_name|
|-------------|
|Aaron Hawkins|
|Adam Bellavance|
|Adam Hart|
|.
|.

Encontrar clientes cadastrados que mais gastaram $ 

```
select customer_name, sum(sales) as "$ Spent" from customer_20_60 c 
inner join sales_2015 s on c.customer_id = s.customer_id group by customer_name order by 2 desc
```

|customer_name|$ Spent|
|-------------|-------|
|Peter Fuller|9022.323999999999|
|Fred Hopkins|6056.089999999999|
|Natalie Webber|5511.316|
|.
|.

Selecionar vendas por cliente contendo ID, nome e idade do cliente, e ordem, id e valor do pedido
```
select s.customer_id, c.customer_name, c.age, s.order_line, s.product_id , s.sales  from sales_2015 s 
inner join customer_20_60 c on s.customer_id = c.customer_id  
```

|customer_id|customer_name|age|order_line|product_id|sales|
|-----------|-------------|---|----------|----------|-----|
|HP-14815|Harold Pawlan|20|15|OFF-AP-10002311|68.81|
|HP-14815|Harold Pawlan|20|16|OFF-BI-10000756|2.544|
|EB-13870|Emily Burns|34|25|FUR-TA-10000577|1044.63|
|.
|.
	
Join múltiplo selecionando nome e idade do cliente (tabela customer), nome do produto (tabela product), e valor e data da venda (tabela sales)
```
select c.customer_name, c.age, p.product_name ,  s.sales, s.order_date  from sales_2015 s 
inner join customer_20_60 c on s.customer_id = c.customer_id inner join product p on s.product_id = p.product_id order by s.order_date desc
```
|customer_name|age|product_name|sales|order_date|
|-------------|---|------------|-----|----------|
|Eric Murdock|46|Lenovo 17-Key USB Numeric Keypad|54.384|2015-12-28|
|Richard Eichhorn|30|Cisco SPA 502G IP Phone|239.9|2015-12-27|
|Arthur Gainer|56|Avery 497|21.56|2015-12-27|
|.
|.
	
	
#### LEFT JOIN

Selecionar todas as vendas independente de ter informação da customer table
```	
select s.customer_id , c.customer_name, c.age, p.product_name ,  s.sales, s.order_date  from sales_2015 s  left join customer_20_60 c on s.customer_id = c.customer_id 		inner join product p on s.product_id = p.product_id 
```

|customer_id|customer_name|age|product_name|sales|order_date|
|-----------|-------------|---|------------|-----|----------|
|SO-20335|||Bretford CR4500 Series Slim Rectangular Table|957.5775|2015-10-11|
|SO-20335|||Eldon Fold N Roll Cart System|22.368|2015-10-11|
|HP-14815|Harold Pawlan|20|Holmes Replacement Filter for HEPA Air Cleaner  Very Large Room  HEPA Filter|68.81|2015-11-22|
|.
|.
        

#### RIGHT JOIN 

Selecionar todos os clientes mesmo que não tenha venda
```
select s.order_line,s.product_id,c.customer_id ,s.sales ,c.customer_name , c.age 
	from sales_2015 s right join customer_20_60 c on s.customer_id = c.customer_id  order by customer_id
```
	
|order_line|product_id|customer_id|sales|customer_name|age|
|----------|----------|-----------|-----|-------------|---|
|1979|OFF-AR-10000127|AA-10375|5.248|Allen Armold|22|
|||AA-10480||Andrew Allen|50|
|8009|OFF-PA-10000474|AA-10645|106.32|Anna Andreadi|32|
	
#### FULL JOIN
	
Seleciona registros das duas tabelas, aparecendo registros sem vendas ou sem dados do cliente
```
select s.order_line,s.product_id,c.customer_id ,s.sales ,c.customer_name , c.age 
	from sales_2015 s full join customer_20_60 c on s.customer_id = c.customer_id order by sales desc
```	
	
|order_line|product_id|customer_id|sales|customer_name|age|
|----------|----------|-----------|-----|-------------|---|
|||AR-10570||Anemone Ratner|36|
|||VM-21835||Vivian Mathis|60|
|510|OFF-BI-10003527||6354.95|||
|.
|.
	
#### CROSS JOIN
	
Basicamente faz a combinação de todos as linhas de uma tabela com todos os valores de outra tabela

```
create table letter (letter "varchar");
insert into letter values ('a'),('b'),('c');
select * from letter;
create table number (number int);
insert into number values (1),(2),(3);
select * from letter;
select letter.letter, number.number from letter, number;
```
	
|letter|number|
|------|------|
|a|1|
|b|1|
|c|1|
|a|2|
|b|2|
|c|2|
|a|3|
|b|3|
|c|3|

</details>
