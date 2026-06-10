# MTP

**MTP** (Multi-Thread Processor) is a command-line utility for executing commands from one or more command files in parallel.

It can be used to speed up batch processing, file conversion, compression tasks, and other workloads that can benefit from concurrent execution.

## Usage

```text
mtp.exe <options> [FILE...]
```

## Options

| Option                | Description                                                                                                |
| --------------------- | ---------------------------------------------------------------------------------------------------------- |
| `-alias=<name=value>` | Define a constant alias that can be used in command files (requested by Edison007)                         |
| `-ec=<code>`          | Expected process exit code (default: `0`)                                                                  |
| `-h`, `--help`        | Display help information                                                                                   |
| `-i=<mode>`           | Progress indicator level (`0`, `1`) (default: `0`)                                                         |
| `-log=<file>`         | Write execution time of each command to a log file                                                         |
| `-p=<priority>`       | Process priority: `idle`, `below_normal`, `normal`, `above_normal`, `high`, `realtime` (default: `normal`) |
| `-t=<count>`          | Number of worker threads                                                                                   |
| `-v=<level>`          | Verbosity level (`0`, `1`, `2`) (default: `1`)                                                             |
| `-w=<path>`           | Working directory                                                                                          |

## Example

```cmd
mtp.exe -t=4 -p=high -log="logs\log.txt" run1.cmd run2.cmd
```

## Command Files

Command files contain a list of commands to execute. Each non-empty line is treated as a separate command and may be processed concurrently depending on the configured thread count.

Example:

```cmd
arc.exe a -ep1 -dses --dirs -s; -lc- -di -i2 -r -m=tor:1 data1.arc packeddata\*
arc.exe a -ep1 -dses --dirs -s; -lc- -di -i2 -r -m=tor:2 data2.arc packeddata\*
arc.exe a -ep1 -dses --dirs -s; -lc- -di -i2 -r -m=tor:3 data3.arc packeddata\*
arc.exe a -ep1 -dses --dirs -s; -lc- -di -i2 -r -m=tor:4 data4.arc packeddata\*
arc.exe a -ep1 -dses --dirs -s; -lc- -di -i2 -r -m=tor:5 data5.arc packeddata\*
arc.exe a -ep1 -dses --dirs -s; -lc- -di -i2 -r -m=tor:6 data6.arc packeddata\*
arc.exe a -ep1 -dses --dirs -s; -lc- -di -i2 -r -m=tor:7 data7.arc packeddata\*
```

The example above creates seven archives that can be processed in parallel by MTP.

## Built-in Aliases

The following aliases are available in command files and alias definitions:

| Alias        | Description                                   |
| ------------ | --------------------------------------------- |
| `{index}`    | Current command index                         |
| `{time}`     | Current time (`HH:mm:ss`)                     |
| `{date}`     | Current date (`yyyy-MM-dd`)                   |
| `{datetime}` | Current date and time (`yyyy-MM-dd HH:mm:ss`) |
| `{appdata}`  | User AppData directory                        |
| `{temp}`     | System temporary directory                    |
| `{userdocs}` | User Documents directory                      |
| `{work_dir}` | Current working directory                     |

## Support the Project

[![Support on Patreon](https://c5.patreon.com/external/logo/become_a_patron_button.png)](https://www.patreon.com/Shegorat)

If you find this project useful, consider supporting development on Patreon.
