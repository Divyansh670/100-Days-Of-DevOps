# 🗓️ Day 2: Linux User Administration & Access Management

## 🎯 Task Overview

As part of a temporary assignment to the **Nautilus project**, a temporary user account was required for an external developer on the Stratos Datacenter infrastructure. The objective was to provision a temporary user account with a strict expiration deadline to ensure zero-maintenance access security compliance.

### 📋 Specifications

| Field | Value |
| :--- | :--- |
| **Target Server** | Application Server 3 (`stapp03`) |
| **Username** | `anita` (lowercase enforcement) |
| **Account Expiry Date** | `2027-03-28` |

---

## 🛠️ Infrastructure Environment Details

| Server Name | IP/Hostname | User | Purpose |
| :--- | :--- | :--- | :--- |
| **Application Server 3** | `stapp03` | `banner` | Hosts Nautilus Application 3 |
| **Jump Host Server** | `jump-host` | `thor` | Provides secure access to Stork DC |

---

## 💻 Implementation Steps

### Step 1: Target Server Authentication

Connected securely to **Application Server 3** from the jump host network environment using the system administrator (`banner`) credentials:

```bash
ssh banner@stapp03
```

> **Password used:** `BigGr33n`

---

### Step 2: User Provisioning with Lease Expiry

Executed the user creation process with the `-e` flag to pass the required account expiration string explicitly in `YYYY-MM-DD` format:

```bash
sudo useradd -e 2027-03-28 anita
```

**Flag Explanation:**

| Flag | Description |
| :--- | :--- |
| `-e 2027-03-28` | Sets the account expiration date in `YYYY-MM-DD` format |
| `anita` | The username to be created (lowercase enforced) |

---

### Step 3: Policy & Compliance Verification

Inspected the security policy properties of the newly created account using the `chage` (change age) command to confirm the aging restrictions were applied successfully:

```bash
sudo chage -l anita
```

**Verified Output Parameters:**

```
Last password change                                    : Jun 13, 2026
Password expires                                        : never
Password inactive                                       : never
Account expires                                         : Mar 28, 2027
Minimum number of days between password change          : 0
Maximum number of days between password change          : 99999
Number of days of warning before password expires       : 7
```

✅ **Key confirmation:** `Account expires : Mar 28, 2027` — matches the required specification.

---

## 🔑 Key Commands Reference

```bash
# SSH into target server
ssh banner@stapp03

# Create user with expiry date
sudo useradd -e 2027-03-28 anita

# Verify account aging/expiry details
sudo chage -l anita

# Alternative: check via /etc/shadow (last field = expiry in days since epoch)
sudo grep anita /etc/shadow
```

---

## 📚 Concepts Learned

- **`useradd -e`** — Sets an account expiration date at creation time (format: `YYYY-MM-DD`)
- **`chage -l`** — Lists all password aging and account expiry policies for a user
- **Temporary access provisioning** — Best practice for contractor/external developer access: always set an expiry to avoid stale accounts
- **Principle of Least Privilege** — Assigning time-bound accounts limits the blast radius if credentials are compromised

---

## 📸 Proof of Submission

> Screenshot showing successful user creation and `chage -l anita` verification output.

![Day 2 Verification Screenshot](Screenshot (468).png)

---

## ✅ Task Status: COMPLETED

| Check | Status |
| :--- | :--- |
| SSH into `stapp03` | ✅ Done |
| Created user `anita` | ✅ Done |
| Expiry set to `2027-03-28` | ✅ Done |
| Verified with `chage -l anita` | ✅ Done |