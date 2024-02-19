# Get a list of tests in Yandex Cloud Load Testing service using YC CLI.

In this example, it is shown how to list and filter tests created in Load Testing service using YC CLI tool.

NOTE: in snippets bellow, it is assumed that folder-id setting is already set in `yc`

```bash
yc config set folder-id 'my_folder_id'
```

NOTE2: to get test ids for further processing, use json output format and `jq` command-line tool:

```bash
yc loadtesting test list --filter $FILTER_QUERY | jq -r "[.[].id] | join(\" \")"
```

## 1. All tests in folder

```bash
yc loadtesting test list
```

## 2. All tests with name containing 'api-examples'

```bash
yc loadtesting test list --filter "details.name CONTAINS 'api-examples'"
```

## 3. All tests with tags 'issue:123' and 'type:release'

```bash
yc loadtesting test list --filter "details.tags.issue:123 and details.tags.type:release"
```

## 4. All tests created by account with id 'loadtester'

```bash
yc loadtesting test list --filter "summary.created_by = 'loadtester'"
```

## 5. All tests created at 29 Jan 2024

```bash
yc loadtesting test list --filter "summary.created_at >= 2024-01-29 AND summary.created_at < 2024-01-30"
```

## 6. All tests created in 2023 which are not finished yet

```bash
yc loadtesting test list --filter "summary.is_finished = false AND summary.created_at >= 2023-01-01 AND summary.created_at < 2024-01-01"
```
