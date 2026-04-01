### 🐞 Interesting Story of an Account Takeover Vulnerability

- Type: Writeup  
- Author:  Deepanshu(golu369)

---

### 🔍 Summary
- Account takeover was found using host header injection in forgotten password flow. The attacker will achieve that by adding something like this Host:attacker.com:login.redacted.com then system will include the attacker domain in the password resent link where he will stole the token. 

### 🧠 Root Cause
- The system failed to validate the header appropriately even thought some techniques failed but this one bypass it.

---

### ⚙️ Exploitation Steps
1. Got the forgotten password page enter email and intercept the request  
2. Replace the Host:login.redacted.com with this Host:attacker.com:login.redacted.com
3. when the victim click the link, the attacker will see the forgetten password token in the server log

---

### 💡 Key Learning
-  Colon (:) can be used to bypass the header verification

---

### 🔗 Source Link
- https://medium.com/@deepanshudev369/interesting-story-of-an-account-takeover-vulnerability-140a45a058a3  


Stored in:
