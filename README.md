# Estudo SQL utilizando PostgreSQL

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
select * from science_class;
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

## Utilizando db Supermart com tabelas customer, sales e products.

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
|...


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
|...


Idade n??o est?? entre 20 e 30<br/>
```
select * from customer where age not between 20 and 30  order by age asc ;
```
|customer_id|customer_name|segment|age|country|city|state|postal_code|region|
|-----------|-------------|-------|---|-------|----|-----|-----------|------|
|CC-12610|Corey Catlett|Corporate|18|United States|Philadelphia|Pennsylvania|19134|East|
|DM-13525|Don Miller|Corporate|18|United States|Houston|Texas|77070|Central|
|CC-12220|Chris Cortes|Consumer|18|United States|La Porte|Indiana|46350|Central|
|...


#### WILDCARDS
Wildcards s??o utilizados para substituir caracteres em uma string, sendo que:
	
	
_  Representa um caractere<br/>
% Representa zero ou mais caractereres


Clientes que o primeiro nome tem cinco letras e a cidade come??a com L <br/>
```
select * from customer where customer_name like '_____ %' AND city like 'L%' order by customer_name asc;
```
|customer_id|customer_name|segment|age|country|city|state|postal_code|region|
|-----------|-------------|-------|---|-------|----|-----|-----------|------|
|AB-10150|Aimee Bixby|Consumer|65|United States|Long Beach|New York|11561|East|
|BE-11410|Bobby Elias|Consumer|54|United States|Lancaster|Ohio|43130|East|
|BT-11440|Bobby Trafton|Consumer|20|United States|Littleton|Colorado|80122|West|
|...



Clientes que o primeiro nome tem cinco letras e a cidade n??o come??a com A <br/>
```
select * from customer where customer_name like '_____ %' AND city not like 'A%' order by city asc
```
|customer_id|customer_name|segment|age|country|city|state|postal_code|region|
|-----------|-------------|-------|---|-------|----|-----|-----------|------|
|CS-12250|Chris Selesnick|Corporate|59|United States|Bossier City|Louisiana|71111|South|
|BD-11635|Brian Derr|Consumer|42|United States|Bowling Green|Kentucky|42104|South|
|GT-14635|Grant Thornton|Corporate|19|United States|Burlington|North Carolina|27217|South|
|...



Clientes que o primeiro nome tem cinco letras, a cidade come??a com L e s??o dos estados de Ohio e Colorado <br/>
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


#### EXERC??CIOS

Obtenha a lista de todas as cidades onde a regi??o ?? Sul ou Leste sem nenhum duplicatas usando instru????o IN

```
select distinct customer_name, city, region from customer where region in('North', 'East');
```
|customer_name|city|region|
|-------------|----|------|
|Gene McClure|Providence|East|
|Toby Braunhardt|Washington|East|
|Alejandro Ballentine|Lorain|East|
|...



Obtenha a lista de todos os pedidos em que o valor de 'vendas' est?? entre 100 e 500 usando o operador BETWEEN
```
select * from sales where sales between 100 and 500;
```

|order_line|order_id|order_date|ship_date|ship_mode|customer_id|product_id|sales|quantity|discount|profit|
|----------|--------|----------|---------|---------|-----------|----------|-----|--------|--------|------|
|1|CA-2016-152156|2016-11-08|2016-11-11|Second Class|CG-12520|FUR-BO-10001798|261.96|2|0.0|41.9136|
|10|CA-2014-115812|2014-06-09|2014-06-14|Standard Class|BH-11710|OFF-AP-10002892|114.9|5|0.0|34.47|
|14|CA-2016-161389|2016-12-05|2016-12-10|Standard Class|IM-15070|OFF-BI-10003656|407.976|3|0.2|132.5922|
|...


Obtenha a lista de clientes cujo sobrenome cont??m apenas 4 caracteres usando LIKE
```
select * from customer where customer_name like '% ____';
```
|customer_id|customer_name|segment|age|country|city|state|postal_code|region|
|-----------|-------------|-------|---|-------|----|-----|-----------|------|
|CG-12520|Claire Gute|Consumer|67|United States|Henderson|Kentucky|42420|South|
|DV-13045|Darrin Van Huff|Corporate|31|United States|Los Angeles|California|90036|West|
|PK-19075|Pete Kriz|Consumer|46|United States|Madison|Wisconsin|53711|Central|
|...


#### ORDER

Pode ser feito ordem ascendente (ASC) ou descendente (desc) e utilizando um ou mais par??metros<br/>

```
select * from customer where state = 'Florida' order by age asc ;

select * from customer where state = 'Florida'  order by customer_name asc, segment asc, age desc
```

Tamb??m ?? poss??vel usar um index das colunas no lugar do nome da coluna. Nesse caso customer_name ?? a 2a coluna, segment a 3a e age a 4a, produzindo o mesmo resultado da query anterior
```
select * from customer where state = 'Florida'  order by 2 asc, 3 asc, 4 desc 
```
|customer_id|customer_name|segment|age|country|city|state|postal_code|region|
|-----------|-------------|-------|---|-------|----|-----|-----------|------|
|AH-10195|Alan Haines|Corporate|67|United States|Tamarac|Florida|33319|South|
|AS-10240|Alan Shonely|Consumer|68|United States|Tampa|Florida|33614|South|
|AG-10525|Andy Gerbode|Corporate|69|United States|Saint Petersburg|Florida|33710|South|
|...


#### ORDER e LIMIT

O limit define quantas linhas v??o ser retornadas. No exemplo usei a coluna age para ordenar. Os clientes com menores idades ser??o selecionados se usar a ordem asc. Os clientes com maiores idades ser??o selecionados se usar a ordem desc.
```
select * from customer where segment = 'Corporate' order by 4 asc limit 3
```
|customer_id|customer_name|segment|age|country|city|state|postal_code|region|
|-----------|-------------|-------|---|-------|----|-----|-----------|------|
|SP-20650|Stephanie Phelps|Corporate|18|United States|San Jose|California|95123|West|
|SC-20770|Stewart Carmichael|Corporate|18|United States|Decatur|Alabama|35601|South|
|MP-17965|Michael Paige|Corporate|18|United States|Lawrence|Massachusetts|1841|East|


#### EXERC??CIOS

Recupere todos os pedidos em que o valor do 'desconto' seja maior que zero ordernado pelo valor de 'desconto' de base de ordem decrescente
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

AS ?? o nome que vai ser dado para a coluna ou tabela<br/>
Para contar o n??mero de produtos vendidos e 
```
select count(*) as "Number of Products Sold" from sales
```
|Number of Products Sold|
|-----------------------|
|9994|


Para contar o n??mero de produtos e de vendas (pode ter mais de um produto em uma venda)
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


Para calcular o lucro total de um produto espec??fico
```
select sum(Profit) as "Total Profit" from sales where product_id = 'FUR-CH-10000454'
```
|product_id|Total Profit|
|----------|------------|
|FUR-CH-10000454|1927.442|

Para calcular o total de vendas um produto espec??fico
```
select  product_id, sum(quantity) as "Total Quantity" from sales where product_id = 'FUR-CH-10000454' group by product_id 
```
|product_id|Total Quantity|
|----------|--------------|
|FUR-CH-10000454|51|

#### AVG

Para calcular um valor m??dio
```
select avg(age) "Average Customer Age" from customer c
```
|Average Customer Age|
|--------------------|
|44.4678436317780580|

Para encontrar os estados com consumidores em m??dia mais jovens
```
select state, avg(age) as "Average Customer Age" from customer c group by state order by 2
```
|state|Average Customer Age|
|-----|--------------------|
|Kansas|20.0000000000000000|
|District of Columbia|24.0000000000000000|
|Arkansas|30.0000000000000000|

Valor m??dio pago em comiss??es considerando comiss??o de 10%
```
select avg(sales * 0.10) as "Average Comission Value" from sales
```
|Average Comission Value|
|-----------------------|
|22.985800083049867|


#### MAX e MIN

Para encontrar o valor da menor venda do m??s de Junho de 2015
```
select min(sales) as "Minimum Sales Value from June 2015" from sales where order_date between '2015-06-01' and '2015-06-30'
```
|Minimum Sales Value from June 2015|
|----------------------------------|
|0.984|

Para encontrar o valor da maior venda do m??s de Junho de 2015

```
select max(sales) as "Maximum Sales Value from June 2015" from sales where order_date between '2015-06-01' and '2015-06-30'
```
|Maximum Sales Value from June 2015|
|----------------------------------|
|3050.376|


#### EXERC??CIOS

Encontre a soma de todos os valores de "vendas".
```
select sum(sales) as "Sum of Sales" from sales
```
|Sum of Sales|
|------------|
|2297200.860299955|

Encontre a contagem do n??mero de clientes na regi??o norte com a idade entre 20 e 30
```
select count(customer_id) from customer where region = 'North' and age between 20 and 30
```
|count|
|-----|
|0|

Calcular a idade m??dia de clientes da regi??o Leste
```
select avg(age) as "Average Customer Age from East Region" from customer c where region = 'East'
```
|Average Customer Age from East Region|
|-------------------------------------|
|44.3363636363636364|

Calcular a idade m??nima e m??xima de clientes da Filad??lfia
```
select min(age) as "Minimum Customer Age from Philadelphia", max(age) as "Maximum Customer Age from Philadelphia" from customer c where city = 'Philadelphia'
```
|Minimum Customer Age from Philadelphia|Maximum Customer Age from Philadelphia|
|--------------------------------------|--------------------------------------|
|18|70|

#### GROUP BY
(J?? foi usado mas refor??ado aqui)

Calcular o n??mero de clientes em cada regi??o
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
|...


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

HAVING ?? usada para colunas agregadas e WHERE em colunas n??o agregadas.


Contar n??mero de clientes por cidade e regi??o e selecionar somente aquelas com mais de 10 clientes
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

#### EXERC??CIOS

Fa??a um painel mostrando os seguintes n??meros para cada ID de produto: Total de vendas (em $) pedido por esta coluna em ordem decrescente, Quantidade total de vendas, N??mero de pedidos, valor m??ximo de vendas, valor m??nimo de vendas, valor m??dio de vendas
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
|...


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
|...

D?? para contar o n??mero de clientes em cada categoria
```
select count(case when age<=21 then 'Young' else null end) as "Young",
	   count(case when age between 22 and 59 then 'Adult' else null end) as "Adult",
	   count(case when age>=60 then 'Elderly' else null end) as "Elderly"
	  from customer;
```
|Young|Adult|Elderly|
|-----|-----|-------|
|66|546|181|
		

## Criando tabelas com registros exclusivos
	
```
/*Creating sales table of year 2015*/

Create table sales_2015 as select * from sales where ship_date between '2015-01-01' and '2015-12-31';
select count(*) from sales_2015; --2131
select count(distinct customer_id) from sales_2015;--578

/* Customers with age between 20 and 60 */
create table customer_20_60 as select * from customer where age between 20 and 60;
select count (*) from customer_20_60;--597
```

#### INNER JOIN
Selecionar os clientes que est??o em ambas tabelas. Tem de estar tanto na customer quanto sales.

```
select distinct customer_name from customer_20_60 c inner join sales_2015 s on c.customer_id = s.customer_id 
order by customer_name  
```
	
|customer_name|
|-------------|
|Aaron Hawkins|
|Adam Bellavance|
|Adam Hart|
|...


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
|...


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
|...

	
Join m??ltiplo selecionando nome e idade do cliente (tabela customer), nome do produto (tabela product), e valor e data da venda (tabela sales)
```
select c.customer_name, c.age, p.product_name ,  s.sales, s.order_date  from sales_2015 s 
inner join customer_20_60 c on s.customer_id = c.customer_id inner join product p on s.product_id = p.product_id
order by s.order_date desc
```
|customer_name|age|product_name|sales|order_date|
|-------------|---|------------|-----|----------|
|Eric Murdock|46|Lenovo 17-Key USB Numeric Keypad|54.384|2015-12-28|
|Richard Eichhorn|30|Cisco SPA 502G IP Phone|239.9|2015-12-27|
|Arthur Gainer|56|Avery 497|21.56|2015-12-27|
|...

	
	
#### LEFT JOIN

Selecionar todas as vendas independente de ter informa????o da customer table
```	
select s.customer_id , c.customer_name, c.age, p.product_name ,  s.sales, s.order_date  from sales_2015 s  
left join customer_20_60 c on s.customer_id = c.customer_id 
inner join product p on s.product_id = p.product_id 
```

|customer_id|customer_name|age|product_name|sales|order_date|
|-----------|-------------|---|------------|-----|----------|
|SO-20335|||Bretford CR4500 Series Slim Rectangular Table|957.5775|2015-10-11|
|SO-20335|||Eldon Fold N Roll Cart System|22.368|2015-10-11|
|HP-14815|Harold Pawlan|20|Holmes Replacement Filter for HEPA Air Cleaner  Very Large Room  HEPA Filter|68.81|2015-11-22|
|...

        

#### RIGHT JOIN 

Selecionar todos os clientes mesmo que n??o tenha venda
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
|...

	
#### CROSS JOIN
	
Basicamente faz a combina????o de todos as linhas de uma tabela com todos os valores de outra tabela

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
	
#### INTERSECT
	
Para selecionar os customer_id que est??o presentes na tabela de vendas de 2015 e no banco de clientes.
INTERSECT remove duplicatas e INTERSECT ALL mant??m duplicatas. O mesmo conceito vale para UNION e EXCEPT
	
```	
select customer_id from sales_2015 s 
intersect
select customer_id from customer_20_60 c 
```

|customer_id|
|-----------|
|JP-15520|
|CM-11815|
|JD-16150|
|...
	
#### EXCEPT

Para selecionar os customer_id que est??o presentes na tabela de vendas de 2015 mas que N??O est??o presentes no banco de dados de clientes
```
select customer_id from sales_2015 s 
except
select customer_id from customer_20_60 c 
```
	
|customer_id|
|-----------|
|TP-21130|
|JR-15670|
|AB-10105|
|...

#### UNION

Para retornar TODAS as customer_id que est??o presentes no sales_2015 E/OU customer_20_60.
	
```
select customer_id from sales_2015 s 
union
select customer_id from customer_20_60 c 
```
	
|customer_id|
|-----------|
|AZ-10750|
|TP-21130|
|AG-10390|
|...
	
#### EXERC??CIOS 
	
Encontrar o total de vendas por estado das tabelas sales_2015 e customer_20_60
No caso usei a fun????o having para excluir as linhas nulas e ordenei do maior para o menor.
```	
select c.state, sum(s.sales) from customer_20_60 c left join sales_2015 s 
on c.customer_id = s.customer_id  group by state having sum(s.sales) > 0 order by sum desc
```
	
|state|sum|
|-----|---|
|California|72712.49479999999|
|Pennsylvania|36239.77419999999|
|New York|29823.967599999993|
|...
	
Retornar uma tabela com o ID e nome do produto, categoria, total de vendas e quantidade de itens.

```
select p.product_id , p.product_name , p.category , sum(sales) as "Total sales", sum(quantity) as "Total #" 
from product p left join sales_2015 s on p.product_id =s.product_id group by p.product_id 
```
	
|product_id|product_name|category|Total sales|Total #|
|----------|------------|--------|-----------|-------|
|OFF-FA-10000304|Advantus Push Pins|Office Supplies|8.72|5|
|OFF-PA-10003656|Xerox 1935|Office Supplies|184.66|7|
|FUR-TA-10001932|Chromcraft 48 x 96 Racetrack Double Pedestal Table|Furniture|||
|...
	
#### SUBQUERY

?? uma subconsulta dentro de outra consulta dentro do WHERE, FROM ou SELECT. Pode ser usada para fazer uma consulta direta evitando salvar tabelas e uso de joins.

Para retornar as vendas de clientes com mais de 60 anos. (WHERE)
```
select * from sales where customer_id in 
(select distinct customer_id from customer c where age > 60)
```
|order_id|customer_id|product_id|sales|quantity|
|--------|-----------|----------|-----|--------|
|CA-2016-152156|CG-12520|FUR-BO-10001798|261.96|2|
|CA-2016-152156|CG-12520|FUR-CH-10000454|731.94|3|
|US-2015-108966|SO-20335|FUR-TA-10000577|957.5775|5|
|...

	
Aqui vou usar m??ltiplos joins e uma subquery para selecionar atributos das tabelas customer, product e sales de clientes com mais de 60 anos.
```
select order_id , customer_name ,  product_name , sales , quantity from sales s 
left join customer c2 on s.customer_id = c2.customer_id left join product p on s.product_id = p.product_id 
where s.customer_id in (select distinct customer_id from customer c where age > 60)
```
	
|order_id|customer_name|product_name|sales|quantity|
|--------|-------------|------------|-----|--------|
|...
|US-2015-108966|Sean O'Donnell|Eldon Fold N Roll Cart System|22.368|2|
|CA-2016-161389|Irene Maddox|Fellowes PB200 Plastic Comb Binding Machine|407.976|3|
|CA-2014-143336|Zuschuss Donatelli|Newell 341|8.56|2|
|...

Para retornar a quantidade de vendas por produto com o nome e categoria. (FROM)
```
select p.product_id , p.product_name , p.category , s.quantity from product p 
left join (select product_id,sum(quantity) as quantity from sales group by product_id) as s on p.product_id = s.product_id
order by quantity desc
```	
|product_id|product_name|category|quantity|
|----------|------------|--------|--------|
|???FUR-BO-10001798|Bush Somerset Collection Bookcase|Furniture||
|TEC-AC-10003832|Logitech??P710e Mobile Speakerphone|Technology|75|
|OFF-PA-10001970|Xerox 1881|Office Supplies|70|
|...
	
Para retornar a id e nome do cliente e ordem do pedido. Subquery est?? dentro do select e funciona como um left join.
```	
select customer_id, order_line, (select customer_name from customer c where c.customer_id=s.customer_id) 
from sales s order by customer_id 
```
|customer_id|order_line|customer_name|
|-----------|----------|-------------|
|AA-10315|1160|Alex Avila|
|AA-10315|5201|Alex Avila|
|AA-10315|5200|Alex Avila|
|...

#### EXERC??CIO
	
Selecionar todas as colunas da tabela sales, nome e idade do cliente da tabela customer, e nome e categoria do produto da tabela products

D?? pra usar join e subqueries
```	
select c.customer_name , c.age , sp.* from customer as c right join 
(select s.*, p.product_name , p.category from sales as s left join product as p on s.product_id = p.product_id ) as sp
on c.customer_id = sp.customer_id 
```

|customer_name|age|order_line|order_id|order_date|ship_date|ship_mode|customer_id|product_id|sales|quantity|discount|profit|product_name|category|
|-------------|---|----------|--------|----------|---------|---------|-----------|----------|-----|--------|--------|------|------------|--------|
|Claire Gute|67|1|CA-2016-152156|2016-11-08|2016-11-11|Second Class|CG-12520|FUR-BO-10001798|261.96|2|0.0|41.9136|||
|Claire Gute|67|2|CA-2016-152156|2016-11-08|2016-11-11|Second Class|CG-12520|FUR-CH-10000454|731.94|3|0.0|219.582|Hon Deluxe Fabric Upholstered Stacking Chairs  Rounded Back|Furniture|
|Darrin Van Huff|31|3|CA-2016-138688|2016-06-12|2016-06-16|Second Class|DV-13045|OFF-LA-10000240|14.62|2|0.0|6.8714|Self-Adhesive Address Labels for Typewriters by Universal|Office Supplies|
|...

	
Ou somente joins (o que acho mais f??cil)

```	
select c.customer_name, c.age , s.* , p.product_name , p.category from sales s 
left join customer c on s.customer_id = c.customer_id 
left join product p on s.product_id = p.product_id; 
```

|customer_name|age|order_line|order_id|order_date|ship_date|ship_mode|customer_id|product_id|sales|quantity|discount|profit|product_name|category|
|-------------|---|----------|--------|----------|---------|---------|-----------|----------|-----|--------|--------|------|------------|--------|
|Claire Gute|67|1|CA-2016-152156|2016-11-08|2016-11-11|Second Class|CG-12520|FUR-BO-10001798|261.96|2|0.0|41.9136|||
|Claire Gute|67|2|CA-2016-152156|2016-11-08|2016-11-11|Second Class|CG-12520|FUR-CH-10000454|731.94|3|0.0|219.582|Hon Deluxe Fabric Upholstered Stacking Chairs  Rounded Back|Furniture|
|Darrin Van Huff|31|3|CA-2016-138688|2016-06-12|2016-06-16|Second Class|DV-13045|OFF-LA-10000240|14.62|2|0.0|6.8714|Self-Adhesive Address Labels for Typewriters by Universal|Office Supplies|
|...

#### VIEWS 
	
View ?? um resultado originado de uma consulta pr??-definida. Essencialmente ?? um metadado que mapeia uma query para outra, por isto pode ser considerado como uma tabela virtual. 

Para criar a view da mesma tabela anterior
```	
create view viewtest as select c.customer_name, c.age , s.* , p.product_name , p.category from sales s 
left join customer c on s.customer_id = c.customer_id 
left join product p on s.product_id = p.product_id;

select * from viewtest;
```
	
|customer_name|age|order_line|order_id|order_date|ship_date|ship_mode|customer_id|product_id|sales|quantity|discount|profit|product_name|category|
|-------------|---|----------|--------|----------|---------|---------|-----------|----------|-----|--------|--------|------|------------|--------|
|Claire Gute|67|1|CA-2016-152156|2016-11-08|2016-11-11|Second Class|CG-12520|FUR-BO-10001798|261.96|2|0.0|41.9136|||
|Claire Gute|67|2|CA-2016-152156|2016-11-08|2016-11-11|Second Class|CG-12520|FUR-CH-10000454|731.94|3|0.0|219.582|Hon Deluxe Fabric Upholstered Stacking Chairs  Rounded Back|Furniture|
|Darrin Van Huff|31|3|CA-2016-138688|2016-06-12|2016-06-16|Second Class|DV-13045|OFF-LA-10000240|14.62|2|0.0|6.8714|Self-Adhesive Address Labels for Typewriters by Universal|Office Supplies|
|...

Outro exemplo seria criar uma view para a equipe de log??stica com id do pedido e informa????es do endere??o.
```	
create view logistics as select s.order_line , s.order_id , c.customer_name , c.city , c.state , c.country , c.postal_code 
from sales s left join customer c on s.customer_id = c.customer_id order by s.order_line;

select * from logistics

```
	
|order_line|order_id|customer_name|city|state|country|postal_code|
|----------|--------|-------------|----|-----|-------|-----------|
|1|CA-2016-152156|Claire Gute|Henderson|Kentucky|United States|42420|
|2|CA-2016-152156|Claire Gute|Henderson|Kentucky|United States|42420|
|3|CA-2016-138688|Darrin Van Huff|Los Angeles|California|United States|90036|
|...
	

#### EXERC??CIO
	
Criar uma view com ordem, valor, desconto e product id da venda mais antiga, com o nome daily_billing. Depois deletar a view.
```	
create view daily_billing as select order_line , product_id , sales, discount from sales order by order_date asc limit 1;
select * from daily_billing;
drop view daily_billing;
```
	
|order_line|product_id|sales|discount|
|----------|----------|-----|--------|
|7981|OFF-PA-10000174|16.448|0.2|

#### LENGTH

Retorna o tamanho da string. Por exemplo para retornar o tamanho do nome dos clientes com tamanho igual ou maior que 15 chars.
```
select customer_name , length(customer_name) as "Name Size" from customer c where length(customer_name) >= 15
```
|customer_name|Name Size|
|-------------|---------|
|Darrin Van Huff|15|
|Brosina Hoffman|15|
|Alejandro Grove|15|
|...

#### UPPER/LOWER

Muda o texto para caixa alta ou baixa
```
select upper(customer_name) , length(customer_name) as "Name Size" from customer c where length(customer_name) >= 15 
```
|upper|Name Size|
|-----|---------|
|DARRIN VAN HUFF|15|
|BROSINA HOFFMAN|15|
|ALEJANDRO GROVE|15|
|...

```
select lower(customer_name) , length(customer_name) as "Name Size" from customer c where length(customer_name) >= 15 
```
|lower|Name Size|
|-----|---------|
|darrin van huff|15|
|brosina hoffman|15|
|alejandro grove|15|
|...


#### TRIM

Usado para remover caracteres de uma string. Precisa determinar o char (no caso usei a letra 't' mas pode remover espa??os, por exemplo), a dire????o (ambos lados, esquerda ou direita) e a string.)
```
select ('t Bruno Evaldt t') , trim(both 't' from 't Bruno Evaldt t'),  trim(leading 't' from 't Bruno Evaldt t') , 
trim(trailing 't' from 't Bruno Evaldt t')
```

|?column?|btrim|ltrim|rtrim|
|--------|-----|-----|-----|
|t Bruno Evaldt t| Bruno Evaldt | Bruno Evaldt t|t Bruno Evaldt |

#### CONCATENATION

Usada para contatenar duas ou mais strings em uma ??nica coluna. Por exemplo, concatenar todos os dados do endere??o do cliente.
```
select customer_name ,  postal_code || ', ' || city || ', ' || state ||', ' || country as "Address"
from customer c 
```

|customer_name|Address|
|-------------|-------|
|Claire Gute|42420, Henderson, Kentucky, United States|
|Darrin Van Huff|90036, Los Angeles, California, United States|
|Sean O'Donnell|33311, Fort Lauderdale, Florida, United States|
|...

#### SUBSTRING

Serve para extrair uma substring de uma string completa. Por exemplo, separar o customer_id em duas partes (letras e n??meros).
```
select customer_id , customer_name , substring(customer_id for 2) as cust_group , 
substring(customer_id from 4 for 5) as cust_number from customer where substring(customer_id for 2) = 'AB'  
```

|customer_id|customer_name|cust_group|cust_number|
|-----------|-------------|---------|-----------|
|AB-10060|Adam Bellavance|AB|10060|
|AB-10165|Alan Barnes|AB|10165|
|AB-10255|Alejandro Ballentine|AB|10255|
|...

#### String Agg

Serve para agregar valores de diferentes colunas em uma string. Por exemplo: concatenar produtos adquiridos por um cliente
```
select c.customer_name , string_agg(s.product_id, ', ' order by product_id) as "Products Ordered" from sales s 
left join customer c on s.customer_id = c.customer_id group by c.customer_name
```

|customer_name|Products Ordered|
|-------------|----------------|
|Aaron Bergman|FUR-BO-10003966, FUR-CH-10004477, OFF-AR-10001427, OFF-ST-10000321, OFF-ST-10002344, TEC-PH-10000562|
|Aaron Hawkins|FUR-CH-10002439, FUR-FU-10003691, OFF-AR-10003183, OFF-BI-10002353, OFF-BI-10004970, OFF-EN-10004773, OFF-LA-10003148, OFF-PA-10003063, OFF-ST-10000046, TEC-AC-10003614, TEC-PH-10003505|
|Aaron Smayling|FUR-BO-10002613, FUR-TA-10001520, OFF-BI-10000474, OFF-BI-10002931, OFF-BI-10003694, OFF-PA-10002709, OFF-PA-10003729, OFF-ST-10000649, TEC-MA-10000488, TEC-MA-10002178|
|...

#### EXERC??CIOS

Achar o comprimento m??ximo de caracteres em nomes de produtos. Primeiro a op????o mais simples depois uma mais complexa (melhor fazer mais simples :)).
```
select length(product_name) from product p order by 1 desc limit 1
```
OU
```
select max(length) as length from (select product_name , length(product_name) from product p) as foo
```
|length|
|------|
|127|

Recuperar nome do produto, subcategoria, categoria e uma coluna com esses valores concatenados.
```
select product_name , sub_category , category , product_name ||  ', ' || sub_category ||  ', ' || category as "Full Description"
from product p 
```

|product_name|sub_category|category|Full Description|
|------------|------------|--------|----------------|
|Bush Somerset Collection Bookcase|Bookcases|Furniture|Bush Somerset Collection Bookcase, Bookcases, Furniture|
|Hon Deluxe Fabric Upholstered Stacking Chairs  Rounded Back|Chairs|Furniture|Hon Deluxe Fabric Upholstered Stacking Chairs  Rounded Back, Chairs, Furniture|
|Self-Adhesive Address Labels for Typewriters by Universal|Labels|Office Supplies|Self-Adhesive Address Labels for Typewriters by Universal, Labels, Office Supplies|
|...

Decompor o product_id em tr??s partes. O primeiro produto aparentemente tem um caractere a mais no come??o que n??o consegui identificar, mas todo o restante est?? como deveria.
```
select product_name,  product_id , substring(product_id for 3 ) as "CategoryCode" , substring(product_id from 5 for 2) as "SubcategoryCode" 
, substring(product_id from 8) as "NameCode" from product p
```

|product_name|product_id|CategoryCode|SubcategoryCode|NameCode|
|------------|----------|------------|---------------|--------|
|Bush Somerset Collection Bookcase|???FUR-BO-10001798|???FU|-B|-10001798|
|Hon Deluxe Fabric Upholstered Stacking Chairs  Rounded Back|FUR-CH-10000454|FUR|CH|10000454|
|Self-Adhesive Address Labels for Typewriters by Universal|OFF-LA-10000240|OFF|LA|10000240|
|...

Listar de forma agregada o nome dos produtos que a subcategoria ?? chairs ou tables
```
select category , sub_category , string_agg(product_name, ', ') as "Products Names"
from product p where sub_category in ('Chairs','Tables') group by category , sub_category order by sub_category 
```
|category|sub_category|Products Names|
|--------|------------|--------------|
|Furniture|Chairs|Hon Deluxe Fabric Upholstered Stacking Chairs  Rounded Back, Global Deluxe Stacking Chair  Gray, Global Fabric Managers Chair  Dark Gray...|
|Furniture|Tables|Bretford CR4500 Series Slim Rectangular Table, Chromcraft Rectangular Conference Tables, Hon Racetrack Conference Tables...|

#### ROUND, CEIL FLOOR

ROUND ?? o arrendondamento normal, CEIL retorna o primeiro n??mero inteiro maior que o input e FLOOR o primeiro n??mero inteiro menor que o input.
```
select avg(age) as "Average Customer Age", round(avg(age)), ceil(avg(age)), floor(avg(age)) from customer c  
```

|Average Customer Age|round|ceil|floor|
|--------------------|-----|----|-----|
|44.4678436317780580|44|45|44|

#### POWER 

Eleva a pot??ncia N (no caso 2).
```
select age , power(age, 2) from customer c 
```
|age|power|
|---|-----|
|67|4489.0|
|31|961.0|
|65|4225.0|
|...

#### EXERC??CIOS 

Voc?? est?? fazendo uma loteria para seus clientes. Ent??o, escolha uma lista de 5 clientes sortudos de
tabela do cliente usando fun????o aleat??ria
```
select customer_name , random() 
from customer c order by random limit 5
```

|customer_name|random|
|-------------|------|
|Ken Lonsdale|0.0002815495638053|
|Guy Thornton|0.0023412613201827526|
|Skye Norling|0.0035048201775289556|
|Adrian Barton|0.00827872530328122|
|Toby Ritter|0.009957251543074364|


Suponha que voc?? n??o possa cobrar do cliente em pontos de fra????o. Portanto, para um valor de venda de 1,63,
voc?? obter?? 1 ou 2. Nesse cen??rio, descubra
a) Receita total de vendas se voc?? estiver cobrando o valor inteiro inferior das vendas sempre
b) Receita total de vendas se voc?? estiver cobrando o valor inteiro mais alto das vendas sempre
c) A receita total de vendas se voc?? estiver arredondando as vendas sempre
```
select sum(floor(s.sales)) as floor, sum(ceil(s.sales)) as ceil, sum(round(s.sales)) as round
from sales s 
```
|floor|ceil|round|
|-----|----|-----|
|2291304.0|2301170.0|2297340.0|


#### DATE, TIME, TIMESTAMP e AGE

S??o fun????es pra recuperar a data ou hora atual ou ambas.
```
select current_date , current_time , current_timestamp 
```

|current_date|current_time|current_timestamp|
|------------|------------|-----------------|
|2021-12-10|15:56:20 -0300|2021-12-10 15:56:20.013 -0300|


?? poss??vel realizar opera????es com a data e usar esse resultado junto com outras cl??sulas como WHERE. Por exemplo: retornar somente os pedidos feitos nos ??ltimos 5 anos.
```
select * from sales where order_date > current_date - (365 * 5)
```

|order_line|order_id|order_date|ship_date|ship_mode|customer_id|product_id|sales|quantity|discount|profit|
|----------|--------|----------|---------|---------|-----------|----------|-----|--------|--------|------|
|13|CA-2017-114412|2017-04-15|2017-04-20|Standard Class|AA-10480|OFF-PA-10002365|15.552|3|0.2|5.4432|
|24|US-2017-156909|2017-07-16|2017-07-18|Second Class|SF-20065|FUR-CH-10002774|71.372|2|0.3|-1.0196|
|35|CA-2017-107727|2017-10-19|2017-10-23|Second Class|MA-17560|OFF-PA-10000249|29.472|3|0.2|9.9468|
|...

Com a fun????o AGE ?? poss??vel calcular o tempo entre dois eventos. Nesse caso calculado quanto tempo desde o in??cio da coloniza????o do estado do Esp??rito Santo.
```
select age(current_date ,'1535-05-23')
```
|age|
|---|
|486 years 6 mons 18 days|

Para calcular quanto tempo levou para cada item ser enviado.
```
select order_id , product_id, age(ship_date, order_date) from sales
```
|order_id|product_id|age|
|--------|----------|---|
|CA-2016-152156|FUR-BO-10001798|3 days|
|CA-2016-152156|FUR-CH-10000454|3 days|
|CA-2016-138688|OFF-LA-10000240|4 days|
|...

?? poss??vel extrair elementos da timestamp usando a fun????o extract
```
select extract (day from current_timestamp) as day, extract (month from current_timestamp) as month, 
extract (year from current_timestamp) as year , extract (doy from current_timestamp) as doy , 
extract (week from current_timestamp) as week, extract (quarter from current_timestamp) as quarter
```
|day|month|year|doy|week|quarter|
|---|-----|----|---|----|-------|
|10|12|2021|344|49|4|


#### Exerc??cio

Calcular a idade do Batman considerando 6 de Abril de 1939 como data de nascimento.
```
select age(current_date, '1939-04-06')
```
|age|
|---|
|82 years 8 mons 7 days|


Analisar a venda de cadeiras em cada m??s. Percebe-se que as pessoas compram mais cadeiras entre Setembro e Dezembro, com uma pequena queda nas vendas em Outubro.
```
select month, sum(sales)::numeric(10,2) from (select order_id , sales, extract(month from order_date) as month_no, TO_CHAR(order_date, 'Month') AS "month"
from sales s left join product p on s.product_id = p.product_id where sub_category = 'Chairs') as foo 
group by month, month_no order by month_no
```

|month|sum|
|-----|---|
|January  |11285.17|
|February |7582.94|
|March    |21344.33|
|April    |18526.59|
|May      |25893.83|
|June     |21523.37|
|July     |23016.35|
|August   |18339.80|
|September|51577.22|
|October  |24170.45|
|November |47760.01|
|December |57429.05|


