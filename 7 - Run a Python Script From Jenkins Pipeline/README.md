#  How Do I Run a Python Script From Jenkins Pipeline? 
```
https://www.youtube.com/watch?v=OB7fGZ32n-s
```

You’re not doing anything wrong 🙂 — this is a **Jenkins UI/version change issue**.

In **newer Jenkins versions**, **“Global Tool Configuration” is removed**, so Python won’t appear there anymore.

Here’s how to fix it 👇

---

## ✅ Why “Global Tool Configuration” is missing

From Jenkins **2.401+**, tool configuration was **moved** and partially **deprecated**.

So:

* ❌ No more **Manage Jenkins → Global Tool Configuration**
* ✅ Tools are now configured via **Manage Jenkins → Tools** or **Node configuration**

---

## ✅ Correct Way to Add Local Python Path (New Jenkins)

### **Option 1: Add Python via Jenkins Tools (Recommended)**

1. Go to **Jenkins Dashboard**
2. Click **Manage Jenkins**
3. Click **Tools**
4. Scroll down → **Python installations**

   * If Python is NOT visible → install the plugin (see Option 3)
5. Click **Add Python**
6. Set:

   ```
   Name: Python3
   Install automatically: ❌ unchecked
   Python executable: C:\Python311\python.exe
   ```
7. Click **Save**

Now you can use it in pipelines:

```groovy
tools {
    python 'Python3'
}
```

---

### **Option 2: Set Python Path at Node Level (Works Always)**

If “Python” tool is not available:

1. Go to **Manage Jenkins**
2. Click **Nodes**
3. Select your node (usually **Built-In Node**)
4. Click **Configure**
5. Under **Node Properties** → **Environment variables**
6. Add:

   ```
   Name: PATH
   Value: C:\Python311\;${PATH}
   ```
7. Save

Verify in job:

```bash
python --version
```

---

### **Option 3: Install Python Plugin (If Missing)**

If you **don’t see “Python installations”** at all:

1. Go to **Manage Jenkins**
2. Click **Plugins**
3. Search **Python**
4. Install **Python Plugin**
5. Restart Jenkins
6. Go back to **Manage Jenkins → Tools**

---

## ✅ Quick Test Job

Add a **Freestyle job** → Build Step → Execute Windows batch:

```bat
python --version
where python
```

If it prints version → ✅ success

---

## 🔑 Summary

| Jenkins Version | Where Python Is              |
| --------------- | ---------------------------- |
| Old Jenkins     | Global Tool Configuration    |
| New Jenkins     | Manage Jenkins → Tools       |
| Any Version     | Node → Environment Variables |

---

If you want, tell me:

* Jenkins version
* Windows / Linux
* Freestyle or Pipeline job

I’ll give you **exact commands** for your setup 🚀
