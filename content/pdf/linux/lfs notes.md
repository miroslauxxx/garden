SysVinit vs SystemD

A **runlevel** in Linux is a mode of operation that determines what processes and services are active at a given time.

| Runlevel | Description                         |
| -------- | ----------------------------------- |
| 0        | Halt (Shutdown)                     |
| 1        | Single-user mode (Maintenance Mode) |
| 2        | Multi-user mode without network     |
| 3        | Full multi-user mode (CLI)          |
| 4        | Unused (customizable)               |
| 5        | Multi-user mode with GUI            |
| 6        | Reboot                              |

target - group of units
it just pulls in other units via Wants=/Requires=

- **Common targets**:
    
    1. multi-user.target: multi-user text mode (old runlevel 3).
        
    2. graphical.target: multi-user with GUI (runlevel 5), pulls in multi-user.target.
        
    3. rescue.target: single-user recovery (runlevel 1).
        
    4. emergency.target: minimal shell, root FS read-only, almost nothing started.
        
    5. reboot.target, poweroff.target: shutdown states.
        
- Switch or query them with systemctl isolate and systemctl set-default.

