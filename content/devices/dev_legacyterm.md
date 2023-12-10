---
title: "Legacy Terminal"
date: 2023-12-03T19:34:08+02:00
draft: false
---

![image](img/dev_legacyterm.png)


| ![image](dev_legacyterm_example.png)                             |
| ---------------------------------------------------------------- |
| Keyboard (KBD) and monitor (CRT) as they appear in the emulator. |

The legacy terminal is actually of two devices: a monitor, and a keyboard. They are quite limited in function, but the simplicity makes them very easy to use.

These two can only deal with numbers. They don't know letters or other characters.


{{% notice style="tip" %}}
The keyboard is a read-only device, and the monitor is a write-only device.  
Trying to output into the keyboard, or to take input from monitor will result in an error.
{{% /notice %}}

## Monitor
The monitor lives at port 0. The compiler constant `CRT` contains the number 0.

Example usage:
```
OUT R1, =CRT;   This will display the value in R1 on the screen
```

## Keyboard
The keyboard lives at port 1. The compiler constant `KBD` contains the number 1.

Example usage:
```
IN  R1, =KBD;   This will request input from the keyboard and then load it into R1
```

{{% notice style="info" %}}
When the TiTo CPU makes an I/O command, it will stop and wait for it to finish. With how the keyboard is directly connected to the CPU port, requesting input will lock the CPU, until the user presses the send button.
{{% /notice %}}
