# Operating Systems Introduction — TryHackMe

- **Platform:** TryHackMe
- **Room:** Operating Systems Introduction
- **Date Completed:** June 2026
- **Flag:** THM{new_pc_for_free!}
- **Medium Article:** [Read here](https://medium.com/@rajprashantwork)

---

## What is an Operating System?

The OS ties together all computing devices and physical components of a computer. It is the **core software that coordinates all functionality** inside the computer.

### The Computing Stack:
```
User
  ↓
Applications
  ↓
Operating System
  ↓
Hardware
```

### Why We Need an OS:
Without an OS, **each application would need direct control** over CPU, memory, files, devices, and security. This would quickly cause conflicts between applications fighting for the same resources.

**The OS solves this by acting as the central organizer** — arbitrating access to shared hardware resources.

---

## Kernel Space vs User Space

| | Kernel Space | User Space |
|---|-------------|------------|
| **Access Level** | Privileged, locked-down core | Limited permissions |
| **What runs here** | The kernel — directly manages hardware | Standard applications |
| **Hardware access** | Direct | Deliberately blocked |
| **Purpose** | System control & resource management | Safety & system stability |

**Why this separation matters:** If applications could directly access hardware, one buggy or malicious app could crash the entire system or access another app's data. This isolation is a **fundamental security boundary**.

**Quiz Answer:** Kernel Space has unrestricted access to computer's hardware ✅

---

## Core OS Functionality

1. **Process Management** — creating, scheduling, terminating processes
2. **Memory Management** — allocating/deallocating RAM to processes
3. **File System Management** — organizing and accessing data on storage
4. **User Management** — handling accounts, authentication, permissions
5. **Device Management** — controlling hardware peripherals

**Quiz Answer:** User Management handles user accounts, authentication, and permissions ✅

---

## OS as a Security Foundation

The OS isn't just about functionality — it's the **first line of security**:

| Security Function | Purpose |
|-------------------|---------|
| **Authentication** | Verifying who you are (login, passwords) |
| **Permissions** | Controlling what you can access |
| **Isolation** | Keeping processes/users separated from each other |
| **System Protection** | Preventing unauthorized access to critical resources |

---

## Interacting with the OS — Two Methods

### CLI — Command Line Interface
- Text-based commands to retrieve or manipulate information
- Precise and fast once learned
- Preferred by system administrators and security professionals

### GUI — Graphical User Interface
- Visual representation — windows, icons, menus
- Interact through clicking/tapping
- More intuitive for everyday users

---

## Types of Operating Systems

| Category | Examples |
|----------|----------|
| **Desktop** | Windows, Linux, macOS |
| **Mobile** | Android, iOS |
| **Server** | Windows Server, Linux, Unix |
| **Cloud** | Cloud-based OS instances |
| **Embedded** | OS built into devices (routers, IoT) |

---

## Practical Tasks Completed

1. Opened **File Systems** tab in System Monitor — checked `/dev/root` device type
2. Navigated **Home directory** on Desktop — counted user directories
3. Navigated to **Alex's home directory** → **Documents** folder
4. Found flag in `note.txt`:

**Flag captured:** `THM{new_pc_for_free!}` ✅

---


## Key Takeaways
1. OS sits between applications and hardware — the central resource coordinator
2. Kernel space = privileged + direct hardware access; User space = restricted, safe
3. 5 core OS functions: Process, Memory, File System, User, Device management
4. OS is fundamentally a security boundary — authentication, permissions, isolation
5. CLI = precision and speed; GUI = visual and intuitive
6. Every device category (desktop, mobile, server, cloud, embedded) runs some form of OS
