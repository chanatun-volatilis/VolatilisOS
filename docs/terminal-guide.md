# Terminal guide for VolatilisOS 2.1

Open **Terminal** from the Programs menu. You will see:

```
VolatilisOS terminal - try ls, help, date
root@volatilis:/#
```

Type a command and press Enter. `help` lists every command.

## Commands to try first

| Command | What it shows |
| --- | --- |
| `vfetch` | OS name, kernel, CPU, memory, screen size and more, next to the logo |
| `logo` | Draws the big VolatilisOS logo |
| `meminfo` | The memory map from the firmware and how many page frames are used |
| `mem` | How big the kernel heap is and how much is used |
| `heaptest` | Tests the heap: allocates, checks, frees and grows it |
| `ls` | Lists the files in the current folder |
| `date` | Shows the date and time |

## Working with files

| Command | What it does |
| --- | --- |
| `read <name>` | Show what is in a file |
| `write <name> <text>` | Write text to a file |
| `touch <name>` | Make an empty file |
| `mv <src> <dst>` | Rename a file |
| `rm <name>` | Delete a file |
| `stat <name>` | Show file info |
| `wc <name>` | Count lines, words and bytes |
| `tail <file>` | Show the last 10 lines |
| `more <file>` | Page through a long file |
| `ln [-s] <target> <newname>` | Make a hard or symbolic link |
| `xxd <file> [n]` | Show a file as hex |
| `usb <cmd> <file>` | Use the external drive: cp, mv, get, ls, rm, format |

The shell also supports `>` and `>>` (send output to a file) and `|` (send
output to another command), plus everyday tools such as `df`, `du`, `mount`,
`chmod`, `sort`, `uniq`, `cut`, `diff`, `free`, `id`, `which`, `kill` and
`dmesg`.

## Fun commands

`banner <text>`, `coin`, `dice`, `roll`, `flip`, `fizzbuzz`, `pick <items>`.

Next: [Known limits](known-limits.md)
