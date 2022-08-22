# Домашнее задание к занятию "8.4 Работа с Roles"

## Подготовка к выполнению
1. (Необязательно) Познакомтесь с [lighthouse](https://youtu.be/ymlrNlaHzIY?t=929)
2. Создайте два пустых публичных репозитория в любом своём проекте: vector-role и lighthouse-role.
3. Добавьте публичную часть своего ключа к своему профилю в github.

## Основная часть

Наша основная цель - разбить наш playbook на отдельные roles. Задача: сделать roles для clickhouse, vector и lighthouse и написать playbook для использования этих ролей. Ожидаемый результат: существуют три ваших репозитория: два с roles и один с playbook.

1. Создать в старой версии playbook файл `requirements.yml` и заполнить его следующим содержимым:

   ```yaml
   ---
     - src: git@github.com:AlexeySetevoi/ansible-clickhouse.git
       scm: git
       version: "1.11.0"
       name: clickhouse 
   ```

2. При помощи `ansible-galaxy` скачать себе эту роль.
3. Создать новый каталог с ролью при помощи `ansible-galaxy role init vector-role`.
4. На основе tasks из старого playbook заполните новую role. Разнесите переменные между `vars` и `default`. 
5. Перенести нужные шаблоны конфигов в `templates`.
6. Описать в `README.md` обе роли и их параметры.

Роли созданы на основе плейбука из предыдущего задания, кроме play потребовалось перенести шаблоны. Все переменные записал в defaults.
Обе роли слабо зависят от дистрибутива, поэтому использование vars не потребовалось.
Установленные программы должны взаимодействовать между собой, это обеспечивается установкой переменных в плейбуке, причем например роли vector требуется знать ip адрес clickhouse, если не установить переменную clickhouse_node_ip, в конфиге вектора будет установлено значение из defaults - clickhouse_node_ip: "127.0.0.1".


7. Повторите шаги 3-6 для lighthouse. Помните, что одна роль должна настраивать один продукт.
8. Выложите все roles в репозитории. Проставьте тэги, используя семантическую нумерацию Добавьте roles в `requirements.yml` в playbook.

```yaml
---
  - src: git@github.com:AlexeySetevoi/ansible-clickhouse.git
    scm: git
    version: "1.11.0"
    name: clickhouse
  - src: git@github.com:dmi3x3/vector-role.git
    scm: git
    version: "1.0.0"
    name: lighthouse-role
  - src: git@github.com:dmi3x3/lighthouse-role.git
    scm: git
    version: "1.0.0"
    name: lighthouse-role
```

9. Переработайте playbook на использование roles. Не забудьте про зависимости lighthouse и возможности совмещения `roles` с `tasks`.

Установку nginx оставил в playbook в виде play.

10. Выложите playbook в репозиторий.

    [Playbook](https://github.com/dmi3x3/08-ansible-04-role_vector)

11. В ответ приведите ссылки на оба репозитория с roles и одну ссылку на репозиторий с playbook.

[Репозиторий с Role vector](https://github.com/dmi3x3/vector-role/tree/1.0.0)

[[Репозиторий с Role lighthouse](https://github.com/dmi3x3/lighthouse-role/tree/1.0.0)

[[Репозиторий с Playbook](https://github.com/dmi3x3/08-ansible-04-role_vector)

---

### Как оформить ДЗ?

Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.

---