#programming #linux 

## `find` 

The `find` command searches for files and directories in a directory hierarchy. It's very flexible — you can search by name, type, size, modification time, and even perform actions on found items.

### Basic Syntax
```bash
find <path> <conditions> <actions>
```


### Common Examples

- **Find all `.py` files**
```bash
find . -name "*.py"
```

- **Find directories named `build`**
```bash
find . -type d -name "build"
```


- **Find files larger than 100 MB**
```bash
find . -size +100M
```

- **Find files modified in the last 24 hours**
```bash
find . -mtime -1
```


- **Find and delete all `.log` files**

```bash 
find . -name "*.log" -exec rm {} \;
```


### Notes

- `{}` → placeholder for the found file path.
- `\;` → ends the `-exec` command.
- Combine conditions with `-o` (OR) and `\( \)`.

### Advanced

- **Search inside files for a string**
```bash
find . -type f -exec grep -H "pattern" {} ;
```

### Quick Cheat Sheet

| Option              | Description                       |
| ------------------- | --------------------------------- |
| `-name "*.ext"`     | Search by name (case-sensitive)   |
| `-iname "*.ext"`    | Search by name (case-insensitive) |
| `-type f`           | Search for files                  |
| `-type d`           | Search for directories            |
| `-size +100M`       | Files larger than 100 MB          |
| `-mtime -1`         | Modified in the last 1 day        |
| `-exec <cmd> {} \;` | Run command on found items        |
| `! -name "*.txt"`   | Exclude `.txt` files              |
| `-maxdepth N`       | Limit search depth                |

# Kill 

The `kill` command in Linux is used to **send signals to processes**, primarily to stop (terminate) them.

> Despite the name, `kill` can send any signal, not just "kill".

It works by sending a signal to a process identified by its **PID** (Process ID).

Use top or bpytop to get PID and monitor processes and daemons. Alternatively use ``ps aux`` to get a list of running processes. 
## Basic Usage 
```bash 
kill <PID>
```
By default, `kill` sends **SIGTERM** (signal 15), which politely asks the process to terminate.

## Signals 

$$
\begin{array}{|c|c|l|l|}
\hline
\textbf{Signal Name} & \textbf{Number} & \textbf{Description} & \textbf{Use Case} \\
\hline
\text{SIGHUP} & 1 & \text{Hangup} & \text{Reload configs or restart daemons} \\
\hline
\text{SIGINT} & 2 & \text{Interrupt} & \text{Ctrl+C in terminal to stop foreground process} \\
\hline
\text{SIGQUIT} & 3 & \text{Quit} & \text{Quit and generate core dump for debugging} \\
\hline
\text{SIGILL} & 4 & \text{Illegal Instruction} & \text{Invalid CPU instruction} \\
\hline
\text{SIGABRT} & 6 & \text{Abort} & \text{Process abort signal} \\
\hline
\text{SIGFPE} & 8 & \text{Floating Point Exception} & \text{Divide by zero or invalid floating point} \\
\hline
\text{SIGKILL} & 9 & \text{Kill (force kill)} & \text{Immediate, cannot be caught or ignored} \\
\hline
\text{SIGSEGV} & 11 & \text{Segmentation Fault} & \text{Invalid memory access violation} \\
\hline
\text{SIGPIPE} & 13 & \text{Broken Pipe} & \text{Write to pipe with no reader} \\
\hline
\text{SIGALRM} & 14 & \text{Alarm Clock} & \text{Timer signal from alarm()} \\
\hline
\text{SIGTERM} & 15 & \text{Terminate} & \text{Graceful termination (default)} \\
\hline
\text{SIGUSR1} & 10 & \text{User-defined signal 1} & \text{Custom application use} \\
\hline
\text{SIGUSR2} & 12 & \text{User-defined signal 2} & \text{Custom application use} \\
\hline
\text{SIGCHLD} & 17 & \text{Child stopped or terminated} & \text{Notify parent process} \\
\hline
\text{SIGCONT} & 18 & \text{Continue} & \text{Resume a stopped process} \\
\hline
\text{SIGSTOP} & 19 & \text{Stop} & \text{Pause process execution (cannot be ignored)} \\
\hline
\text{SIGTSTP} & 20 & \text{Terminal Stop} & \text{Ctrl+Z to stop process} \\
\hline
\text{SIGTTIN} & 21 & \text{Background process input} & \text{Input request by background job} \\
\hline
\text{SIGTTOU} & 22 & \text{Background process output} & \text{Output request by background job} \\
\hline
\end{array}

$$

## Quick Cheat Sheet

```bash
ps aux | grep <name>        # Find process PID
kill <PID>                  # Graceful stop
kill -9 <PID>               # Force kill
pkill <name>                # Kill by name
kill -l                     # List all signals
```
