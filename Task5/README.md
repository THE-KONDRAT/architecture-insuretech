# Задание 5. Проектирование GraphQL API
Схема GraphQL является эквивалентом представленного REST API (три эндпоинта: `/clients/{id}`, `/clients/{id}/documents`, `/clients/{id}/relatives`).
Один query client(id) с гибким выбором полей покрывает все три операции.

[schema](schema.graphql)

## Запросы, покрывающие указанные операции REST API
1. Оформление страховки
```graphql
query {
  client(id: "123") {
    name
    documents { type number }
  }
}
```
Ранее это требовало двух запросов (`clients/{id}` и `/clients/{id}/documents`).
2. Карточка клиента в ЛК
```graphql
query {
  client(id: "123") {
    name age
    relatives { relationType name }
  }
}
```
Ранее это требовало двух запросов (`clients/{id}` и `/clients/{id}/relatives`).

Потребитель запрашивает только нужные поля, что исключает избыточную передачу данных при объёмной карточке клиента (до 500 атрибутов согласно тексту задания) и лишние RPS от множества отдельных ресурсов.