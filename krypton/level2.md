# Krypton Level 2 → Level 3 Write-Up

## 🎯 Objective

Retrieve the password for the next level by breaking a **Caesar-cipher–encrypted file** using the provided **encrypt binary**.

---

## 🧠 Concepts Learned

### 1. Chosen-Plaintext Attack

Even if the encryption key is secret, an attacker can:

* Encrypt **known input**
* Observe **ciphertext output**
* Recover the **encryption shift/key**

This is called a **chosen-plaintext attack**.

---

### 2. Weakness of Classical Ciphers

The Caesar cipher:

* Uses a **single alphabet shift**
* Has only **25 possible keys**
* Is easily broken with:

  * Known plaintext
  * Frequency analysis
  * Brute force

So it provides **no real security**.

---

### 3. Linux Permissions & setuid Behavior

This level also teaches:

* Writable **temporary directories**
* **Symbolic links** to restricted files
* **setuid binaries** running as another user
* Permission control using `chmod`

These are important for **real privilege-escalation scenarios**.

---

## 🛠 Tools Used

* `mktemp` → create writable temporary directory
* `cd` → move into working directory
* `ln -s` → create symbolic link to keyfile
* `chmod` → allow setuid program access
* `encrypt` → oracle that encrypts chosen plaintext
* `cat` / `ls` → view files and outputs

---

## 🧩 Step-by-Step Solution

### Step 1 — Create a writable working directory

```bash
cd "$(mktemp -d)"
```

---

### Step 2 — Create plaintext to test encryption

```bash
echo "AAAAA" > input.txt
```

Using repeating letters helps reveal the **Caesar shift instantly**.

---

### Step 3 — Link the required keyfile

The encrypt program expects `keyfile.dat` in the **current directory**.

```bash
ln -s /krypton/krypton2/keyfile.dat
```

---

### Step 4 — Allow setuid user access

```bash
chmod 777 .
```

This lets the **setuid encrypt binary** enter the directory.

---

### Step 5 — Encrypt chosen plaintext

```bash
/krypton/krypton2/encrypt input.txt
```

This produces a file named:

```
ciphertext
```

---

### Step 6 — Determine Caesar shift

Compare:

* Plaintext: `AAAAA`
* Ciphertext: (example) `GGGGG`

Shift = **6**.

---

### Step 7 — Decrypt the target file

Apply the discovered shift in reverse to:

```
/krypton/krypton2/krypton3
```

This reveals the **next level password**.

---

## 🏁 Final Takeaways

* **Encryption access can break secrecy** (chosen-plaintext attack).
* **Classical ciphers are insecure** in modern security.
* **Linux permissions and setuid programs** are critical in exploitation.

This level is less about cryptography
and more about **attacker mindset + system manipulation**.

---

## 📚 Skills Gained

* Bash command chaining
* Temporary directory handling
* Symbolic link abuse
* Basic cryptanalysis logic
* Understanding encryption oracles

---

**Level Status:** ✔ Solved
**Key Lesson:**

> Security must remain strong even when attackers can encrypt chosen input.
