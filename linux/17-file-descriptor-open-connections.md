# File Descriptor & Open Connections

## lsof & Process Investigation

```text
| Command             | Description                                      |
| ------------------- | ------------------------------------------------ |
|   lsof              | Lists open files and resources.                  |
|   lsof -i :80       | Shows which process is using port 80.            |
|   lsof -i :443      | Shows which process is using port 443.           |
|   lsof -u username  | Displays files/processes associated with a user. |
|   lsof /path/file   | Shows which process is using a specific file.    |
|   fuser -v /path    | Displays processes using a specific resource.    |
|   fuser -k 8080/tcp | Terminates processes using TCP port 8080.        |

```
