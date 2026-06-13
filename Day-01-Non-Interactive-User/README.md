# Day 1: Creating a Non-Interactive User in Linux

## 🎯 Task Objective
The system admin team at **xFusionCorp Industries** requires the creation of a user with a non-interactive shell.
* **Username:** `james`
* **Shell:** Non-interactive (`/sbin/nologin` or `/bin/false`)
* **Target Server:** App Server 1

---

## 🛠️ Infrastructure Details
* **Jump Host:** `thor`
* **Target Server:** `App Server 1` (`stapp01`)
* **User Account:** `tony`

---

## 🚀 Step-by-Step Implementation

### 1. Connect to App Server 1
From the jump host (`thor`), SSH into `stapp01` using the designated user account:

```bash
ssh tony@stapp01
```

### 2. Execute the User Creation Command
Run the `useradd` command with the `-s` flag to explicitly assign `/sbin/nologin` as the default shell. This prevents the user from opening an interactive terminal session. Because this modifies system accounts, prepend it with `sudo`:

```bash
sudo useradd -s /sbin/nologin james
```

### 3. Verification (Best Practice)
To ensure the user was created correctly and mapped to the right shell configuration, check the system's identity database:

```bash
grep james /etc/passwd
```

Expected output snippet: `james:x:...:...::/home/james:/sbin/nologin`

---

## 📸 Proof of Completion
Below is the execution capturing the active session on stapp01 and the successful command run:

![alt text](<Screenshot (460).png>)