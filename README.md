# Homework1

## Схема БД
![Описание изображения]()

Таблица была приведена к 3НФ форме (все атрибуты зависят только от ключа и ни от чего другого), поскольку соблюдались все условия как для 1НФ (все атрибуты атомарные), так и 2НФ (все неключевые атрибуты должны зависеть от всего составного ключа, а не от его части). Отмечу, что в нашей БД есть таблциа с составным ключом (product). Поскольку в зависимости от product_id и brand меняются остальные параметры.
## Проектирование БД

```
create table if not exists address (postcode int primary key,
state text,
country text
);

create table if not exists customers(customer_id int primary key,
first_name text,
last_name text,
gender varchar(1),
DOB timestamp,
job_title text,
job_industry_category text,
wealth_segment text,
deceased_indicator varchar(2),
owns_car bool,
property_valuation int,
address text,
postcode int,
foreign key (postcode) references address (postcode)
);

create table if not exists products(
product_id int,
brand_name text,
product_line text,
product_class text,
product_size text,
list_price float,
standard_cost float,
primary key (product_id,brand_name));

create table if not exists transactions (transaction_id int primary key,
product_id int,
brand_name text,
customer_id int,
transaction_date timestamp,
online_order bool,
order_status text,
foreign key (product_id,brand_name) references products(product_id,brand_name),
foreign key (customer_id) references customers(customer_id));

insert into address (postcode, state, country) values
(2016, 'New South Wales', 'Australia');

INSERT INTO customers (customer_id, first_name, last_name, gender, DOB, job_title, job_industry_category, wealth_segment, deceased_indicator, owns_car,property_valuation, address, postcode)
VALUES
(1, 'Laraine', 'Medendorff', 'F', '1953-10-12', 'Executive', 'Health', 'Mass Casual', 'N', TRUE, 10, '060 Mornir', 2016);

INSERT INTO products (product_id, brand_name, product_line, product_class, product_size, list_price, standard_cost)
VALUES
(86, 'OHM Cycle', 'Standard', 'Medium', 'Medium', 235.63, 125.07);

INSERT INTO transactions (transaction_id, product_id, brand_name, customer_id, transaction_date, online_order, order_status)
VALUES
(94, 86, 'OHM Cycle', 1, '2017-12-23', FALSE, 'Approved');








```
