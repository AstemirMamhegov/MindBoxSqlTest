# MindBoxSqlTest

### 2 задача MindBox:

#### В базе данных MS SQL Server есть продукты и категории. Одному продукту может соответствовать много категорий, в одной категории может быть много продуктов. Напишите SQL запрос для выбора всех пар «Имя продукта – Имя категории». Если у продукта нет категорий, то его имя все равно должно выводиться:

##### Решение задачи:

###### Создаем таблицы.

CREATE TABLE [dbo].[Product](
	[ID] [int] IDENTITY(1,1) NOT NULL,
	[ProductName] [nvarchar](255) NULL,
 CONSTRAINT [PK_Product] PRIMARY KEY CLUSTERED 
([ID] ASC ) ) ON [PRIMARY]

CREATE TABLE [dbo].[Category](
	[ID] [int] IDENTITY(1,1) NOT NULL,
	[CategoryName] [nvarchar](255) NULL,
 CONSTRAINT [PK_Category] PRIMARY KEY CLUSTERED 
([ID] ASC) ) ON [PRIMARY]

CREATE TABLE [dbo].[ProductCategories] (
	[ProductID] [int] FOREIGN KEY REFERENCES Product(ID),
	[CategoryID] [int] FOREIGN KEY REFERENCES Category(ID),
	PRIMARY KEY (ProductId, CategoryId)
);

###### Вписываем данные
INSERT INTO [dbo].[Product]
           ([ProductName])
     VALUES
           ('Coca Cola'),
           ('Chicken'),
           ('Tuna'),
           ('Rainbow trout'),
           ('Soap')

INSERT INTO [dbo].[Category]
           ([CategoryName])
     VALUES
           ('Meat'),
           ('Seafood'),
           ('Drink')

INSERT INTO ProductCategories
VALUES
	(1, 3),
	(2, 1),
	(3, 2),
    (3, 1),
    (4, 2),
    (4, 1)
 
###### Собственно запрос 

SELECT ProductName, CategoryName 
FROM Product p
LEFT JOIN ProductCategories pc ON pc.ProductID = p.ID
LEFT JOIN Category c ON pc.CategoryID = c.ID
ORDER BY p.ProductName, c.CategoryName

 ###### Выводим результат
![result](https://github.com/AstemirMamhegov/MindBoxSqlTest/assets/64645245/10f13a8a-6abc-4f82-b63d-9e1b173e6623)
