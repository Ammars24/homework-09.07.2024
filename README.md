# homework-09.07.2024
-- Описание задания.
 -- 1 уровень сложности: 
 -- 1. Создать базу Shop, используя следующий скрипт: https://github.com/NelliEfr/MySQL_databases/blob/main/shop.txt
-- 2. Выведите имена всех продавцов. Предусмотрите также в выборке имена их боссов, сформировав атрибут bossname.
--  В выборке должно присутствовать два атрибута — sname, bossname.

-- Выведите имена покупателей, которые совершили покупку на сумму больше 1000 условных единиц.
-- В выборке должно присутствовать два атрибута — cname, amt.

-- Выведите имена покупателей, которые сделали заказ.
-- Предусмотрите в выборке также имена продавцов.
-- Примечание: покупатели и продавцы должны быть из разных городов.
-- В выборке должно присутствовать два атрибута — cname, sname.

-- Выведите пары покупателей и обслуживших их продавцов из одного города.
-- Вывести: sname, cname, city

-- 1. Создать базу Shop, используя следующий скрипт: https://github.com/NelliEfr/MySQL_databases/blob/main/shop.txt
create database shop;
use shop;
create table SELLERS(
       SELL_ID    INTEGER, 
       SNAME   VARCHAR(20), 
       CITY    VARCHAR(20), 
       COMM    NUMERIC(2, 2),
             BOSS_ID  INTEGER
);
create table CUSTOMERS(
       cust_id integer,
       cname varchar (20),
       city varchar (20),
       rating integer
       );
       create table ORDERS(
       ORDER_ID  INTEGER, 
       AMT     NUMERIC(7,2), 
       ODATE   DATE, 
       CUST_ID    INTEGER,
       SELL_ID    INTEGER 
);

INSERT INTO SELLERS VALUES(201,'Oleg','Moscow',0.12,202);
INSERT INTO SELLERS VALUES(202,'Lev','Sochi',0.13,204);
INSERT INTO SELLERS VALUES(203,'Arseney','Vladimir',0.10,204);
INSERT INTO SELLERS VALUES(204,'Ekaterina','Moscow',0.11,205);
INSERT INTO SELLERS VALUES(205,'Leonid ','Kazan',0.15,NULL);

INSERT INTO CUSTOMERS VALUES(301,'Andrey','Moscow',100);
INSERT INTO CUSTOMERS VALUES(302,'Mechael','Tula',200);
INSERT INTO CUSTOMERS VALUES(303,'Ivan','Sochi',200);
INSERT INTO CUSTOMERS VALUES(304,'Dmitrii','Yaroslavel',300);
INSERT INTO CUSTOMERS VALUES(305,'Ruslan','Moscow',100);
INSERT INTO CUSTOMERS VALUES(306,'Artem','Tula',100);
INSERT INTO CUSTOMERS VALUES(307,'Yuliya','Sochi',300);


INSERT INTO ORDERS VALUES(101,18.69,'2022-03-10',308,207);
INSERT INTO ORDERS VALUES(102,5900.1,'2022-03-10',307,204);
INSERT INTO ORDERS VALUES(103,767.19,'2022-03-10',301,201);
INSERT INTO ORDERS VALUES(104,5160.45,'2022-03-10',303,202);
INSERT INTO ORDERS VALUES(105,1098.16,'2022-03-10',308,207);
INSERT INTO ORDERS VALUES(106,75.75,'2022-04-10',304,202); 
INSERT INTO ORDERS VALUES(107,4723,'2022-05-10',306,201);
INSERT INTO ORDERS VALUES(108,1713.23,'2022-04-10',302,203);
INSERT INTO ORDERS VALUES(109,1309.95,'2022-06-10',304,203);
INSERT INTO ORDERS VALUES(110,9891.88,'2022-06-10',306,201);
       
 -- 2. Выведите имена всех продавцов. Предусмотрите также в выборке имена их боссов, сформировав атрибут bossname.
--  В выборке должно присутствовать два атрибута — sname, bossname.      
   
select* from sellers;
select t1.sname,t1. BOSS_ID as bossname
from sellers t1
left join sellers t2
on t1.BOSS_ID = t2.SELL_ID;

-- 3. Выведите имена покупателей, которые совершили покупку на сумму больше 1000 условных единиц.
-- В выборке должно присутствовать два атрибута — cname, amt.
select* from orders;
select* from customers;
select* from sellers;

select* from customers;
select* from orders;
select t1.cname,t2.amt
from orders t2
join customers t1
on t2.cust_id = t1.cust_id
where t2.atm > 1000;



-- 4. Выведите имена покупателей, которые сделали заказ.
-- Предусмотрите в выборке также имена продавцов.
-- Примечание: покупатели и продавцы должны быть из разных городов.
-- В выборке должно присутствовать два атрибута — cname, sname.

SELECT t1.cname, t2.sname
FROM 
    ORDERS t3
JOIN 
    CUSTOMERS t1
ON 
    t3.cust_id = t1.cust_id
JOIN 
    SELLERS t2
ON 
    t3.sell_id = t2.sell_id
WHERE 
    t1.city <> t2.city;
    
   -- 5. Выведите пары покупателей и обслуживших их продавцов из одного города.
   -- Вывести: sname, cname, city
   SELECT t1.sname, t2.cname, t1.city
FROM 
    ORDERS t3
JOIN 
    CUSTOMERS t2
ON 
    t3.cust_id = t2.cust_id
JOIN 
    SELLERS t1
ON 
    t3.sell_id = t1.sell_id
WHERE 
    t2.city = t1.city;
