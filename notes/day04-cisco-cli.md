# 🌐 Day 04 - Cisco IOS CLI

## 🎯 Objectives

After completing this topic, you should be able to:

- Explain what Cisco IOS and the CLI are.
- Describe how to connect to a Cisco device.
- Understand Cisco IOS CLI modes.
- Navigate between CLI modes.
- Configure basic security for privileged EXEC mode.
- Understand running-config and startup-config.
- Save configurations.
- Understand password encryption methods.
- Use common CLI shortcuts and help features.

---

# 📖 Cisco IOS

## 🔹 Cisco IOS

Cisco IOS (Internetwork Operating System) is the operating system used on Cisco networking devices such as routers and switches.

It provides the Command-Line Interface (CLI) used to configure, monitor, and troubleshoot devices.

> **Note:** Cisco IOS is different from Apple's iOS.

---

# 📖 Command-Line Interface (CLI)

## 🔹 CLI

A **Command-Line Interface (CLI)** allows administrators to configure devices by entering text commands.

Most network engineers prefer the CLI because it is faster, more flexible, and provides complete access to device configuration.

### Example

```text
Router> enable
```

---

## 🔹 GUI

A **Graphical User Interface (GUI)** allows configuration through windows, menus, and buttons.

Cisco devices may support GUIs, but the CCNA focuses primarily on the CLI.

---

# 📖 Connecting to a Cisco Device

## 🔹 Console Connection

The first-time configuration of a Cisco device is performed through the **console port**.

Common console ports include:

- RJ45 Console Port
- USB Mini-B Console Port

### Rollover Cable

A **rollover cable** is used to connect a computer to an RJ45 console port.

Modern laptops often require a **USB-to-Serial adapter** because they lack serial ports.

---

## 🔹 Terminal Emulator

A terminal emulator allows access to the Cisco CLI.

Common software:

- PuTTY
- Tera Term
- SecureCRT

Default Cisco serial settings:

| Setting | Value |
|----------|------|
| Speed (Baud Rate) | 9600 bps |
| Data Bits | 8 |
| Stop Bits | 1 |
| Parity | None |
| Flow Control | None |

---

# 📖 Cisco IOS CLI Modes

## 🔹 User EXEC Mode

Prompt:

```text
Router>
```

Purpose:

- Basic monitoring
- Limited commands
- No configuration changes

Enter by:

- Logging into the device

---

## 🔹 Privileged EXEC Mode

Prompt:

```text
Router#
```

Enter using:

```text
enable
```

Purpose:

- Full monitoring
- Save configurations
- Reload device
- Access configuration modes

---

## 🔹 Global Configuration Mode

Prompt:

```text
Router(config)#
```

Enter using:

```text
configure terminal
```

Shortcut:

```text
conf t
```

Purpose:

- Modify the device's configuration

---

# 📖 CLI Help & Shortcuts

## 🔹 Question Mark (?)

Displays available commands or command options.

Examples:

```text
?
```

Shows all available commands.

```text
show ?
```

Shows possible options after `show`.

```text
en?
```

Shows commands beginning with `en`.

---

## 🔹 Tab Key

Automatically completes commands.

Example:

```text
en + Tab
```

becomes

```text
enable
```

---

## 🔹 Command Abbreviations

Cisco IOS accepts shortened commands if they are unique.

Examples:

| Full Command | Shortcut |
|--------------|----------|
| enable | en |
| configure terminal | conf t |
| show running-config | sh run |

---

# 📖 Password Protection

## 🔹 enable password

Configures a password for Privileged EXEC mode.

```text
enable password CCNA
```

Characteristics:

- Case-sensitive
- Stored in plain text unless encrypted
- Less secure

---

## 🔹 service password-encryption

Encrypts passwords configured with commands such as `enable password`.

```text
service password-encryption
```

Characteristics:

- Cisco Type 7 encryption
- Better than plain text
- Easily reversible
- Does **not** affect `enable secret`

---

## 🔹 enable secret

Configures a more secure password for Privileged EXEC mode.

```text
enable secret Cisco
```

Characteristics:

- Always encrypted
- Uses MD5 (Type 5)
- More secure than `enable password`
- Takes precedence if both commands are configured

---

# 📖 Running Configuration vs Startup Configuration

## 🔹 running-config

The active configuration currently stored in RAM.

Changes take effect immediately.

View with:

```text
show running-config
```

Shortcut:

```text
sh run
```

---

## 🔹 startup-config

The saved configuration stored in NVRAM.

Loaded when the device boots.

View with:

```text
show startup-config
```

---

# 📖 Saving Configuration

The running configuration must be saved to become the startup configuration.

Methods:

```text
write
```

```text
write memory
```

```text
copy running-config startup-config
```

All three perform the same function.

---

# 📖 The `do` Command

The `do` command allows Privileged EXEC commands to be executed while in Configuration Mode.

Example:

```text
do show running-config
```

Useful when verifying configurations without leaving Global Configuration Mode.

---

# 📖 Removing Configuration

## 🔹 no Command

Removes a previously configured command.

Example:

```text
no service password-encryption
```

Important:

- Existing encrypted passwords remain encrypted.
- Future passwords are not automatically encrypted.

---

# 📖 Configuration Flow

```text
User EXEC
      │
      ▼
enable
      │
      ▼
Privileged EXEC
      │
      ▼
configure terminal
      │
      ▼
Global Configuration
```

---

# 📖 Command Summary

| Command | Purpose |
|----------|---------|
| enable | Enter Privileged EXEC mode |
| configure terminal | Enter Global Configuration mode |
| enable password | Configure basic privileged password |
| enable secret | Configure secure privileged password |
| service password-encryption | Encrypt configured passwords |
| show running-config | View active configuration |
| show startup-config | View saved configuration |
| write | Save configuration |
| write memory | Save configuration |
| copy running-config startup-config | Save configuration |
| do | Execute Privileged EXEC commands in Configuration Mode |
| no | Remove a configuration command |
| exit | Return to the previous mode |

---

# 🔗 Connections to Previous Lessons

- Cisco IOS CLI is used to configure networking devices introduced in Day 01.
- Routers and switches communicate using the TCP/IP model learned in Day 03.
- Configuration changes made through the CLI affect how devices process packets and frames.
- Understanding CLI navigation is essential for all future CCNA labs.

---

# 📝 Summary

- Cisco IOS is the operating system used on Cisco networking devices.
- The CLI is the primary method for configuring Cisco devices.
- User EXEC, Privileged EXEC, and Global Configuration are the three main CLI modes introduced in this lesson.
- The `enable` command enters Privileged EXEC mode, while `configure terminal` enters Global Configuration mode.
- Passwords can be protected using `enable password` or the more secure `enable secret`.
- `service password-encryption` encrypts most passwords but does not affect `enable secret`.
- The running configuration is the active configuration, while the startup configuration is loaded during boot.
- Save configurations using `write`, `write memory`, or `copy running-config startup-config`.
- CLI shortcuts, command abbreviations, and context-sensitive help make Cisco IOS faster and easier to use.