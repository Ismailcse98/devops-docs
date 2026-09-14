# Package Management

## Ubuntu/Debian Package Management

```text
| Command               | Description                                    |
| --------------------- | ---------------------------------------------- |
|   apt update          | Updates package repository information.        |
|   apt upgrade         | Upgrades installed packages.                   |
|   apt install nginx   | Installs a package.                            |
|   apt remove nginx    | Removes a package.                             |
|   apt purge nginx     | Removes a package and its configuration files. |
|   apt autoremove      | Removes unused dependencies.                   |
|   apt search nginx    | Searches available packages.                   |
|   apt show nginx      | Displays package information.                  |
|   dpkg -l             | Lists installed Debian packages.               |
|   dpkg -i package.deb | Installs a `.deb` package manually.            |

```

## RHEL/CentOS/Amazon Linux

```text
| Command                | Description                   |
| ---------------------- | ----------------------------- |
|   dnf install nginx    | Installs a package.           |
|   dnf update           | Updates installed packages.   |
|   dnf remove nginx     | Removes a package.            |
|   dnf search nginx     | Searches for packages.        |
|   rpm -qa              | Lists installed RPM packages. |
|   rpm -ivh package.rpm | Installs an RPM package.      |

```
