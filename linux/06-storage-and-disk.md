# Storage & Disk

## Disk Management

```text
| Command            | Description                                              |
| ------------------ | -------------------------------------------------------- |
|   df -h            | Displays filesystem disk usage in human-readable format. |
|   du -sh directory | Displays the total disk usage of a directory.            |
|   du -sh *         | Displays the size of each item in the current directory. |
|   lsblk            | Displays block devices and disk/partition structure.     |
|   blkid            | Displays partition UUIDs and filesystem types.           |
|   fdisk -l         | Displays disk and partition information.                 |
|   mount            | Mounts a filesystem.                                     |
|   umount           | Unmounts a filesystem.                                   |
|   findmnt          | Displays mounted filesystem information.                 |
|   sync             | Flushes buffered filesystem data to disk.                |
```

## Filesystem & Archive

```text
| Command                         | Description                            |
| ------------------------------- | -------------------------------------- |
|   tar -cvf archive.tar dir/     | Creates a TAR archive.                 |
|   tar -xvf archive.tar          | Extracts a TAR archive.                |
|   tar -czvf archive.tar.gz dir/ | Creates a compressed TAR/GZIP archive. |
|   tar -xzvf archive.tar.gz      | Extracts a `.tar.gz` archive.          |
|   gzip file                     | Compresses a file using gzip.          |
|   gunzip file.gz                | Decompresses a gzip file.              |
|   zip archive.zip file          | Creates a ZIP archive.                 |
|   unzip archive.zip             | Extracts a ZIP archive.                |
|   bzip2 file                    | Compresses a file using bzip2.         |
|   xz file                       | Compresses a file using xz.            |

```
