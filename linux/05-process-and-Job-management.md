# Process & Job Management

## Process Commands
```text
| Command           | Description                                                |
| ----------------- | ---------------------------------------------------------- |
|   ps              | Displays processes associated with the current shell.      |
|   ps aux          | Displays almost all running processes.                     |
|   ps -ef          | Displays detailed process information.                     |
|   top             | Provides live process, CPU, and memory monitoring.         |
|   htop            | Interactive and user-friendly process monitoring tool.     |
|   pgrep nginx     | Finds process IDs by process name.                         |
|   pidof nginx     | Displays the PID of a specific program.                    |
|   kill PID        | Sends a signal to a process.                               |
|   kill -9 PID     | Forcefully terminates a process.                           |
|   pkill nginx     | Terminates processes based on their name.                  |
|   killall nginx   | Terminates processes with a specific name.                 |
|   nice            | Starts a process with a specific CPU scheduling priority.  |
|   renice          | Changes the priority of a running process.                 |
|   jobs            | Displays background jobs of the current shell.             |
|   bg              | Runs a stopped job in the background.                      |
|   fg              | Brings a background job to the foreground.                 |
|   nohup command & | Keeps a process running after the terminal session closes. |
```

## System Resource Monitoring
```text
| Command         | Description                                                     |
| --------------- | --------------------------------------------------------------- |
|   uptime        | Displays system uptime and load average.                        |
|   free -h       | Displays RAM and Swap usage.                                    |
|   vmstat        | Displays CPU, memory, process, and I/O statistics.              |
|   iostat        | Displays CPU and disk I/O statistics.                           |
|   sar           | Collects and displays historical system performance statistics. |
|   mpstat        | Displays CPU/core performance statistics.                       |
|   lscpu         | Displays CPU architecture and processor information.            |
|   lsmem         | Displays memory information.                                    |
|   nproc         | Displays the number of available CPU processors.                |
|   watch command | Repeatedly executes a command and displays updated output.      |
|   dmesg         | Displays kernel and hardware-related messages.                  |
```