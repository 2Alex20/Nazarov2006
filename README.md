14/10 добавлены задачи

- [ ] https://github.com/2Alex20/Nazarov-java-pizzaproject/issues/11
- [ ] https://github.com/2Alex20/Nazarov-java-pizzaproject/issues/4
- [x] Update README.md


13/10 добавлено описани REST API 
[wiki](https://github.com/2Alex20/Nazarov-java-pizzaproject/wiki/REST-API-details) or [wiki relative link](../../wiki/REST-API-details)

This site was built using [markdown](https://pages.github.com/).

---

Database scheeme:

```mermaid
graph TD;
    cafe-->id_cafe;
    cafe-->name_cafe;
    cafe-->address_cafe;
    pizza-->id;
    pizza-->id_cafe;
    pizza-->name;
    pizza-->size;
    pizza-->cafe;
    pizza-->key_ingredients;
    pizza-->price;
    key_ingredients-->blob;
```

---

Разработать приложение, построенное по принципу чистой архитектуры.

1 СЛОЙ - ДОМЕН.

Сущности слоя:
Товар (Идентификатор, Наименование, Цена).
Корзина (Список товаров). 
    Должна возвращать итоговую стоимость товаров, среднюю стоимость товара, 
    добавлять товар, удалять товар, полностью очищаться.
Клиент (Идентификатор, Имя, Корзина).
База данных (Список товаров, Список клиентов). 
При создании должна содержать пять товаров и трёх клиентов.
Не забываем про интерфейсы для сущностей.

БД должна принимать запросы вида:
"Select all customers" - такие запросы выполняет метод select
"Select customer where id = 1" - такие запросы выполняет метод select
"Add new customer name = Vasya" - такие запросы выполняет метод execute
"Delete customer where id = 1" - такие запросы выполняет метод execute
Если запрос начинается с неверного слова, выбрасывать SQLException.
То же самое по аналогии для товаров.
При создании новых сущностей БД автоматически должна присваивать им новый идентификатор.

Методы интерфейса БД:
void execute(String query) throws SQLException;
List<Object> select(String query) throws SQLException;

2 СЛОЙ - РЕПОЗИТОРИЙ.

Сущности слоя:
Репозиторий клиентов (База данных).
Репозиторий товаров (База данных).
Репозиторий продуктов должен предоставлять методы для выборки всех или одного продукта,
добавления нового продукта, удаления продукта. При этом репозиторий обращается в БД.
То же самое по аналогии для репозитория клиентов, плюс ещё три метода:
    добавить в корзину клиента товар (по ИД клиента и ИД товара),
    удалить товар из корзины (по ИД клиента и ИД товара),
    очистить корзину полностью (по ИД клиента)

3 СЛОЙ - СЕРВИС.

Сущности слоя:

Сервис товаров (Репозиторий товаров).
Функционал кроме получения, удаления и добавления:
Получить общее количество товаров.
Получить суммарную стоимость товаров.
Получить среднюю стоимость товаров.
Удалить товар по наименованию.
Итого 8 методов.

Сервис клиентов (Репозиторий клиентов, Сервис товаров).
Функционал кроме получения, удаления и добавления:
Получить общее количество покупателей.
Получить стоимость корзины покупателя по его идентификатору.
Получить среднюю стоимость товара в корзине покупателя по его идентификатору.
Удалить покупателя по имени.
Добавить в корзину покупателя товар по их идентификаторам.
Удалить товар из корзины покупателя по их идентификаторам.
Очистить корзину покупателя по его идентификатору.
Итого 11 методов.

Написать конфигурацию, которая регистрирует в контексте бины БД, обоих репозиториев и обоих сервисов.

4 СЛОЙ - КОНТРОЛЛЕРЫ.

Сущности слоя:
Контроллер клиентов (Сервис клиентов).
Контроллер товаров (Сервис товаров).

Подумать над реализацией контроллеров.
Контроллеры должны использовать все возможности соответствующих сервисов.

После реализации протестировать работу приложения при помощи Postman.
