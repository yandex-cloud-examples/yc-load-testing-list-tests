# Получение списка тестов в сервисе Yandex Cloud Load Testing с помощью YC CLI

В данном примере объясняется, как с помощью YC CLI выводить список созданных в Load Testing тестов, а также фильтровать их.

_Примечание 1._ В приведенных ниже фрагментах кода предполагается, что параметр `folder-id` уже задан в конфигурации `yc`:

```bash
yc config set folder-id 'my_folder_id'
```

_Примечание 2._ Для получения идентификаторов тестов, которые понадобятся для дальнейшей обработки, используйте формат вывода JSON и инструмент командной строки `jq`:

```bash
yc loadtesting test list --filter $FILTER_QUERY | jq -r "[.[].id] | join(\" \")"
```

## Все тесты в каталоге

```bash
yc loadtesting test list
```

## Все тесты, в названии которых присутствует `api-examples`

```bash
yc loadtesting test list --filter "details.name CONTAINS 'api-examples'"
```

## Все тесты с тегами `issue:123` и `type:release`

```bash
yc loadtesting test list --filter "details.tags.issue:123 and details.tags.type:release"
```

## Все тесты, созданные аккаунтом с идентификатором `loadtester`

```bash
yc loadtesting test list --filter "summary.created_by = 'loadtester'"
```

## Все тесты, созданные 29 января 2024 года

```bash
yc loadtesting test list --filter "summary.created_at >= 2024-01-29 AND summary.created_at < 2024-01-30"
```

## Все тесты, созданные в 2023 году, которые еще не завершены

```bash
yc loadtesting test list --filter "summary.is_finished = false AND summary.created_at >= 2023-01-01 AND summary.created_at < 2024-01-01"
```
